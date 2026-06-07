# Estratégia de Conteúdo — Blog do Invoice Manager

## Objetivo

Gerar tráfego orgânico via Google para o Invoice Manager através de conteúdo informativo
direcionado a freelancers brasileiros que prestam serviço para clientes internacionais.

## Setup Técnico

- **Plataforma:** Jekyll (nativo do GitHub Pages)
- **Estrutura:** `_posts/` na raiz, renderizado em `/blog/`
- **URLs:** `/blog/:title/` (configurado em `_config.yml`)
- **Layouts:** `_layouts/default.html` (base) e `_layouts/post.html` (artigo + CTA)
- **Index:** `blog/index.html` lista todos os posts automaticamente
- **Deploy:** Zero configuração — push no main já publica

### Como adicionar um novo post

1. Criar arquivo em `_posts/` com formato `YYYY-MM-DD-titulo.md`
2. Adicionar front matter:
   ```yaml
   ---
   layout: post
   title: "Título do Post"
   description: "Meta description para SEO (aparece no Google)"
   ---
   ```
3. Escrever o conteúdo em markdown
4. A CTA pro app é inserida automaticamente pelo layout `post.html`

### Limitação conhecida

O GitHub Pages não suporta plugins Jekyll por segurança. O que vier nativo
(kramdown, liquid, sitemap.xml manual) é o que temos. Se precisar de plugins,
migrar pra Vercel ou Netlify.

---

## Calendário de Posts

### Fase 1 — Validação (3 posts iniciais)

| # | Título | Foco SEO | Data |
|---|--------|----------|------|
| 1 | Commercial Invoice para Freelancers Brasileiros: Guia Completo | "commercial invoice", "fatura comercial freelancer", "commercial invoice Brasil" | 07/06 |
| 2 | Como Receber Pagamento do Exterior como PF no Brasil | "receber pagamento exterior PF", "receber dinheiro de fora Brasil", "freelancer receber em dólar" | 14/06 |
| 3 | Planilha de Horas para Freelancer: Como Organizar e Transformar em Fatura | "planilha de horas freelancer", "transformar planilha em fatura", "gerar invoice de planilha" | 21/06 |

Publicação semanal (toda segunda-feira) durante 3 semanas.

### Fase 2 — Expansão (após validar)

| # | Título | Foco SEO |
|---|--------|----------|
| 4 | Tax ID / UID / VAT: O que é e Onde Colocar na Fatura Internacional | "tax id commercial invoice", "vat number fatura internacional" |
| 5 | Diferença entre Nota Fiscal (NF) e Commercial Invoice | "diferença nota fiscal commercial invoice", "NF para cliente exterior" |
| 6 | PIX como Método de Pagamento em Fatura Internacional | "pix pagamento exterior", "pix commercial invoice" |
| 7 | Guia de Impostos pra Freelancer BR com Cliente Gringo | "carnê leão freelancer exterior", "irpf renda exterior" |
| 8 | Invoice Bilingue PT/EN: Modelo e Campos Obrigatórios | "invoice bilingue portugues ingles", "fatura bilingue freelancer" |
| 9 | Como Embarcar como Freelancer para Empresa na Europa | "freelancer BR cliente Europa", "contrato prestação serviço exterior" |

---

## Diretrizes de Conteúdo

### Tom e Voz
- Direto, sem enrolação
- Tom de quem já passou pelo problema (nicho de dev freelancer)
- Português claro, jargão técnico quando necessário mas explicado

### Estrutura de Cada Post
1. Título com palavra-chave principal no início
2. Meta description com a palavra-chave e benefício claro
3. Introdução curta (2-3 frases) identificando o problema
4. Seções com subtítulos (H2, H3) para quebrar o texto
5. Tabelas comparativas quando relevante
6. Resumo no final
7. CTA suave pro app (inserida automaticamente pelo layout)

### SEO On-page
- URL amigável: `/blog/titulo-do-post/`
- Heading hierarchy: 1 H1, H2s para seções, H3s para subseções
- Internal link pro app no CTA
- Nenhum link externo que dispute o mesmo tema (evitar canibalização)

### Métricas de Acompanhamento
- Cliques no CTA do blog → app (via GitHub Pages tem logs)
- Contato de usuários via Ko-fi ou issues
- Manutenção: revisar a cada 3 meses se os posts ainda estão atuais

---

## Manutenção

### gitignore
Jekyll gera uma pasta `_site/` com os arquivos compilados. Já adicionar no
`.gitignore` se for fazer build local. No GitHub Pages isso é automático.

### Blog vs App
O app (`index.html`) não tem front matter Jekyll, então é tratado como arquivo
estático e servido normalmente. Não interfere com o blog.
