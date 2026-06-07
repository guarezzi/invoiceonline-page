# Invoice Manager — Knowledge Base

## Propósito
Gerar faturas comerciais em PDF a partir de dados de horas trabalhadas copiados de uma planilha. Substitui o fluxo manual de: copiar dados da planilha → enviar para IA gerar markdown → copiar markdown para site conversor → baixar PDF.

## Stack
- **Arquivo único**: `index.html` (zero build, zero dependências locais)
- **PDF**: `pdfmake` 0.2.12 via CDN (`cdnjs.cloudflare.com`)
- **Persistência**: `localStorage` para dados fixos do usuário
- **Deploy**: GitHub Pages (push do `index.html` direto)

## Arquitetura (tudo inline no index.html)

### Estrutura do Layout (split)
```
┌─────────────────────────────────────────────┐
│ Left Panel (form)      │ Right Panel (preview)│
│ ┌─────────────────────┐│ ┌─────────────────┐  │
│ │ Dados Fixos (details)││ │ Invoice Preview │  │
│ │ Lançar Horas        ││ │ (ao vivo)       │  │
│ │ Preview Tabela      ││ └─────────────────┘  │
│ │ Gerar PDF           ││                      │
│ └─────────────────────┘│                      │
└─────────────────────────────────────────────┘
```

### Fluxo de dados
1. **Input**: Texto tab-separado (data, horas, descrição) colado pelo usuário **ou** upload de CSV (`;`)
2. **Parse**: `parseEntries()` (textarea) ou `parseCSV(csvText)` (arquivo) → array de objetos `{date, hoursRaw, hoursDec, desc, taskId, cleanDesc}`
3. **Group**: `groupEntries()` → agrupa por `taskId` → `{taskId, totalDec, cleanDesc}`
4. **Render Preview**: `renderPreview()` → HTML injetado no preview panel
5. **Generate PDF**: `generatePDF()` → docDef pdfmake → download automático

## Dados Fixos do Usuário

### Beneficiário
| Campo | Valor |
|-------|-------|
| Nome | Luiz Ricardo Guarezzi |
| CPF | 068.754.809-80 |
| E-mail | lguarezzi@gmail.com |
| Telefone | +55 (48) 99651-2139 |
| País | Brasil (Brazil) |

### Cliente
| Campo | Valor |
|-------|-------|
| Razão Social | LELAK GmbH |
| Endereço | Drusbergstrasse 68, 8053 Zürich |
| País | Suíça (Switzerland) |
| Tax ID | CHE-020.4.072.557-3 |
| Contato | hello@lelak.co \| +41 79 422 84 73 |

### Pagamento
| Campo | Valor |
|-------|-------|
| Método | PIX (Brazil Local Bank Transfer) |
| Chave PIX | 48996512139 |
| Titular | Luiz Ricardo Guarezzi |
| Valor Hora | R$ 120,00 |

## Formato dos Dados de Entrada (Planilha)
Tab-separado, 3 colunas:
```
Data\tHoras\tDescrição
18/05/2026\t2:00:00\tMG-56  - Épico 2: Backend - Data Models & APIs
```

### Regras de Parsing
- Split por `\t` (fallback: 3+ espaços)
- **CSV**: delimitador `;`, pula linha de cabeçalho se contiver `Data;Horas;Descrição`
- Horas no formato `HH:MM:SS` → convertido para decimal
- Task ID extraído via regex: `/^([A-Za-z]+-\d+)\s*[-–]\s*(.+)/`
  - taskId = `MG-56`, cleanDesc = `Épico 2: Backend - Data Models & APIs`

### Agrupamento
- Entradas com mesmo `taskId` são agrupadas em uma linha na fatura
- Total de horas por grupo é somado (decimal)
- Display: `MG-56: cleanDesc (Xh YYmin)`

## Estrutura do PDF (seções numeradas)
```
COMMERCIAL INVOICE
─────────────────────
Invoice Number: ...   |   Issue Date: ...

1. PRESTADOR / BENEFICIARY
2. TOMADOR / CUSTOMER
3. DESCRIÇÃO DOS SERVIÇOS / VALUATION  (tabela única combinada)
4. INFORMAÇÕES DE PAGAMENTO / PAYMENT DETAILS
─────────────────────
```

### Tabela Combinada (seção 3)
| Task | Description of Services | Hours | Rate (Valor/h) | Total (BRL) |
|------|------------------------|-------|----------------|-------------|
| MG-56 | Épico 2: Backend... | 3.0000 | R$ 120,00 | R$ 360,00 |
| **TOTAL** | | **21.9167** | | **R$ 2.630,00** |

### Formatação Moeda (BRL)
```javascript
function fmtBRL(v) {
  var parts = v.toFixed(2).split('.');
  var intPart = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, '.');
  return 'R$ ' + intPart + ',' + parts[1];
}
```
Ex: `2630.00` → `R$ 2.630,00`

## Funções Principais (escopo global)

| Função | Descrição |
|--------|-----------|
| `parseEntries()` | Lê textarea, faz parse, atualiza `entries[]`, chama `renderEntries()` + `renderPreview()` |
| `parseCSV(csvText)` | Faz parse de texto CSV (`;`), pula cabeçalho se existir, atualiza `entries[]` |
| `renderEntries()` | Renderiza tabela de entradas + summary bar no left panel |
| `renderPreview()` | Constrói HTML do preview da fatura no right panel |
| `groupEntries(entries)` | Agrupa entradas por taskId → array de grupos com total |
| `generatePDF()` | Monta docDef do pdfmake e dispara download |
| `collectFixedData()` | Lê valores dos inputs de dados fixos |
| `saveFixedData()` | Persiste dados fixos no localStorage |
| `loadFixedData()` | Carrega dados fixos do localStorage |
| `fmtBRL(v)` | Formata número como moeda BRL |
| `fmtHours(dec)` | Converte decimal → "Xh YYmin" |
| `fmtHoursTotal(dec)` | Converte decimal → "X Hours and Y Minutes." |
| `escHtml(s)` | Escapa HTML entities |

## Auto-save
- Dados fixos salvos automaticamente 300ms após qualquer alteração
- Preview atualiza automaticamente 300ms após qualquer alteração
- Chave no localStorage: `invoiceData`

## Estilos Visuais
- Paleta: Slate (`#f8fafc` fundo, `#0f172a` texto primário, `#334155` secundário)
- Acento: Blue-600 (`#2563eb`)
- Cards: borda sutil (`rgba(0,0,0,0.04)`) + sombra dupla
- Preview: sombra de documento flutuante, padding interno 32px 36px
- Títulos de seção (`.section-label`): barra vertical `#2563eb` à esquerda, fundo `#f8fafc`, texto slate escuro uppercase bold 700, padding 5px 0 5px 10px, border-radius 0 4px 4px 0

## Deploy (GitHub Pages)
- Único arquivo: `index.html`
- Dependências externas (CDN): pdfmake, vfs_fonts
- localStorage funciona em GitHub Pages sem configuração adicional
- Subir direto no branch `main` ou `gh-pages`

## Segurança
- **Nunca** colocar tokens, senhas, secrets ou dados sensíveis em comentários de issues, PRs ou commits
- Revisar sempre antes de publicar qualquer conteúdo em repositórios públicos

## Commits e Issues
- **Nunca** commitar sem permissão explícita do usuário. Só execute `git commit` quando o usuário disser "commita", "commit", "pode commitar" ou equivalente.
- Sempre referenciar o número da issue na mensagem do commit (ex: `#15`)
- Formato: `#<numero> - <mensagem>` (o `#` com o número da issue no início, seguido de espaço, traço, espaço e a mensagem)
- Se não souber qual a issue relacionada, perguntar ao usuário antes de commitar

## Observações
- Invoice Number gerado automaticamente: `<prefixo><YYYYMMDD>`
- O prefixo da NF é opcional (configurável nos dados fixos)
- Preview e PDF compartilham a mesma lógica de formatação
- pdfmake usa `Roboto` como fonte padrão (vfs_fonts via CDN)
- Navegadores modernos (Chrome, Firefox, Edge, Safari)
