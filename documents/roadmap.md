# Invoice Manager — Roadmap de Comercialização

## Modelo de Receita
**Gratuito para usar**, monetizado com anúncios e doações.

| Modelo | Fase | Receita | Esforço |
|--------|------|---------|---------|
| Ko-fi / Buy Me a Coffee | Fase 1 | Baixa | Mínimo |
| Links afiliados (ferramentas parceiras) | Fase 1 | Média | Baixo |
| Carbon Ads / EthicalAds | Fase 2 | Média-alta | Médio |
| Google AdSense (com conteúdo/blog) | Fase 3 | Alta | Alto |
| Assinatura Premium (opcional) | Fase 4 | Média | Alto |

---

## Fase 1 — Pronto para o Público

### 1.1 Privacidade e Dados do Usuário
- [x] Criar `user-data.json` com dados do desenvolvedor
- [x] Remover dados hardcoded do HTML (inputs começam vazios)
- [x] Auto-load do `user-data.json` quando rodar local (file://)
- [x] Botão "Carregar exemplo" com dados de demonstração
- [x] Exportar/Importar dados fixos em JSON

### 1.2 Transparência e Conteúdo
- [x] Modal "Como usar" com instruções
- [x] Modal "Privacidade" explicando localStorage
- [x] Meta tags (description, og:title, og:description)
- [x] Favicon

### 1.3 Monetização Inicial
- [x] Botão Ko-fi / Buy Me a Coffee
- [x] Links afiliados no footer (ferramentas para freelancers)
  - [ ] **Cadastrar** nos programas de afiliados (Notion, Toggl Track, Figma, Calendly, Canva, Hostinger) e gerar links próprios
  - [ ] **Trocar link do pdfmake** por uma ferramenta com programa de afiliados

### 1.4 UX
- [x] Responsividade mobile (split layout quebra para coluna única)
- [x] Placeholders nos inputs de dados fixos
- [x] Upload de CSV como alternativa ao colar texto (#20)
- [x] Configuração de idioma da fatura (PT/EN/ambos) (#21)

---

## Fase 2 — Crescimento

### 2.1 Infraestrutura
- [ ] Registrar domínio próprio (ex: gerafatura.com.br)
- [ ] Configurar DNS para GitHub Pages ou Vercel/Netlify
- [ ] SSL gratuito (já incluso em GitHub Pages / Vercel)
- [ ] Analytics (Plausible — gratuito e privacy-first)

### 2.2 Tráfego e Audiência
- [ ] Coletar feedback dos primeiros usuários
- [ ] Melhorar SEO
- [ ] Aplicar para Carbon Ads / EthicalAds (requer tráfego consistente)

### 2.3 Funcionalidades
- [ ] Templates de preset (salvar múltiplos clientes)
- [ ] Histórico de faturas geradas (localStorage)
- [ ] Personalização de layout do PDF (cores, logo)

---

## Fase 3 — Expansão

### 3.1 Conteúdo e SEO
- [ ] Blog / guias (como fazer invoice, dicas para freelancers)
- [ ] Landing page com mais conteúdo editorial
- [ ] Desbloquear Google AdSense (requer páginas com conteúdo)

### 3.2 Multilíngue
- [ ] i18n — toggle Português / Inglês na interface
- [ ] templates de fatura em outros idiomas

### 3.3 Contas e Backend (opcional)
- [ ] Sistema de cadastro (email + senha)
- [ ] Presets salvos no servidor (acessíveis de qualquer lugar)
- [ ] Histórico de faturas na nuvem
- [ ] API para integração com ferramentas de time tracking

---

## Fase 4 — Sistema de Gestão de Horas Freelancer

Transformar o app de um gerador de faturas avulso em um **sistema de registro diário de horas** com geração seletiva de faturas por período.

### 4.1 Persistência de Entradas
- [ ] Criar armazenamento persistente `timeEntries` no localStorage/sessionStorage
- [ ] Funções `saveEntry()`, `deleteEntry()`, `loadAllEntries()`, `loadFilteredEntries()`
- [ ] Migrar fluxo de "Lançar Horas" para salvar no armazenamento persistente

### 4.2 Interface de Registro Diário
- [ ] Card "Registro de Horas" com campos: data (datepicker), horas (time), descrição
- [ ] Botão "Adicionar" que salva entrada no storage e atualiza a lista
- [ ] Área expansível "Colar dados da planilha" para o fluxo antigo de copiar/colar
- [ ] Tabela de histórico com todas as entradas salvas (ordenadas por data)
- [ ] Botão de excluir entrada individual
- [ ] Summary mensal com total de horas registradas

### 4.3 Seleção de Período para Fatura
- [ ] Card "Gerar Fatura" substitui card atual "Entradas"
- [ ] Filtro de período: inputs "De" (data) e "Até" (data)
- [ ] Botão "Carregar" que busca entradas do período no storage persistente
- [ ] Lista de tarefas agrupadas com checkbox (todas pré-selecionadas)
- [ ] Botão "Marcar todos" / "Desmarcar todos"
- [ ] Barra de resumo com total de horas selecionadas e valor

### 4.4 Geração Seletiva de PDF
- [ ] Função `generateSelectedPDF(selectedIds)` que gera PDF apenas das entradas selecionadas
- [ ] Preview do preview (pré-visualização no painel direito) refletir apenas itens selecionados
- [ ] Manter compatibilidade com o fluxo atual (colar e gerar direto)

---

## Observações Técnicas

- **Stack atual**: HTML puro + CSS + JS (arquivo único)
- **PDF**: pdfmake 0.2.12 via CDN (cdnjs.cloudflare.com)
- **Input**: colar tab-separado ou upload CSV (delimitador `;`)
- **Persistência**: localStorage + sessionStorage (nada vai para servidor)
  - Chave `invoiceData` — dados fixos do usuário
  - Chave `timeEntries` — entradas de horas (Fase 4)
- **Deploy atual**: GitHub Pages (push do index.html)
- **Domínio sugerido**: gerafatura.com.br / invoicepdf.app / faturafacil.app
- **Custo domínio**: ~R$ 40-60/ano
- **Custo hosting**: R$ 0 (GitHub Pages / Vercel / Netlify)
