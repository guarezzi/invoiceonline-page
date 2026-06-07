# Plano de Ação — Invoice Manager

## Premissa

O Invoice Manager não compete como "mais um gerador de invoice grátis" (mercado saturado).
O diferencial real é o **pipeline planilha → PDF**: um atalho pra quem já usa Excel/Google
Sheets pra registrar horas e fatura clientes internacionais.

Antes de qualquer investimento (domínio, marketing, anúncios), é preciso **validar o nicho e
construir retenção**.

---

## Plano (6-8 semanas)

### Passo 1 — Validar o nicho com a ferramenta atual

**Custo:** R$ 0  
**Prazo:** 1 semana

Ir até o público-alvo e medir reação real:

- Postar em comunidades BR: r/devbr, r/freelancebr, grupos de WhatsApp/Telegram de devs freelancers
- Mostrar o fluxo e o link do GitHub Pages
- Não pedir opinião — pedir pra testar
- Métrica de sucesso: quantas pessoas efetivamente usaram

Se ninguém se importar → resposta grátis antes de gastar R$ 50.

---

### Passo 2 — Implementar Registro Diário de Horas (Fase 4 do roadmap)

**Custo:** R$ 0 (esforço próprio de dev)  
**Prazo:** 3-4 semanas

Transformar a ferramenta de uso mensal (gerar invoice) em **uso diário** (registrar horas):

1. **Persistência de entradas** (`localStorage`)
   - Salvar entradas individualmente com data, horas, descrição, taskId
   - Funções: `saveEntry()`, `deleteEntry()`, `loadEntries()`, `loadEntriesByPeriod()`
   - Chave no storage: `timeEntries`

2. **Interface de Registro Diário**
   - Card "Registro de Horas" com campos: data, horas, descrição
   - Botão "Adicionar" que salva no storage e atualiza lista
   - Área expansível "Colar dados da planilha" para fluxo antigo
   - Tabela de histórico com entradas salvas (ordenadas por data)
   - Botão de excluir entrada individual
   - Summary mensal com total de horas

3. **Seleção de Período para Fatura**
   - Card "Gerar Fatura" substitui card atual "Entradas"
   - Filtro "De" e "Até" para selecionar período
   - Botão "Carregar" que busca entradas do período
   - Lista de tarefas agrupadas com checkbox (todas pré-selecionadas)
   - Barra de resumo com total de horas selecionadas e valor

4. **Geração Seletiva de PDF**
   - Gerar PDF apenas das entradas selecionadas
   - Preview reflete apenas itens selecionados
   - Manter compatibilidade com fluxo atual (colar e gerar direto)

---

### Passo 3 — Oferecer pra quem testou no Passo 1

**Custo:** R$ 0  
**Prazo:** 1 semana

- Voltar nos mesmos canais com a versão atualizada
- "Agora você pode registrar horas todo dia e gerar a fatura do mês com 2 cliques"
- Coletar feedback sobre o que falta

---

### Passo 4 — Avaliar investimento com base em dados reais

**Só depois dos passos 1-3** decidir:

| Ação | Quando |
|------|--------|
| Registrar domínio (ex: `horas.app`, `faturacerta.com`) | Se houver uso recorrente e feedback positivo |
| Plano Premium (R$ 9-19/mês) | Se houver retenção consistente |
| Conteúdo/SEO/blog | Se houver tração orgânica |
| Google AdSense / Carbon Ads | Se houver tráfego consistente |
| Abandonar projeto | Se ninguém usar |

---

## Modelo de Receita (futuro)

### Gratuito (sempre)
- 1 cliente
- Sem personalização de layout
- Sem histórico na nuvem

### Premium (R$ 9-19/mês) — *se houver demanda*
- Múltiplos clientes
- Logo e cores personalizadas no PDF
- Exportar dados
- Templates salvos

### Outras fontes
- Ko-fi / Buy Me a Coffee (já implementado)
- Links afiliados (já implementado, precisa cadastrar programas)

---

## Critérios de Sucesso

| Indicador | Como medir | Meta mínima |
|-----------|-----------|-------------|
| Uso após validação | Quem testou voltou a usar? | 5+ usuários reais |
| Retenção diária | Entradas sendo registradas fora do período de fatura | 3+ usuários registrando horas semanalmente |
| Engajamento | Feedback qualitativo | "Isso resolve um problema" vs "Tanto faz" |
| Conversão (futuro) | % dispostos a pagar por Premium | 5-10% dos ativos |

---

## Riscos

| Risco | Mitigação |
|-------|-----------|
| Ninguém se importa com o projeto | Passo 1 revela isso em 1 semana, sem custo |
| Concorrente copia a ideia | Nicho é pequeno, não atrai grandes players. Primeiro a se mover leva vantagem |
| Usam 1x e nunca mais | Resolvido pela Fase 4 (registro diário vira hábito) |
| Não conseguem pagar (público BR) | Modelo freemium com features avançadas; valor baixo (R$ 9-19) |
