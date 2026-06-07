# Invoice Manager

Gera faturas comerciais em PDF diretamente no navegador a partir de dados de horas trabalhadas. Substitui o fluxo manual de copiar dados da planilha → enviar para IA → converter para PDF.

## Como usar

1. Abra o `index.html` no navegador (ou acesse via GitHub Pages)
2. Preencha seus dados fixos (beneficiário, cliente, pagamento)
3. Cole os dados da planilha (tab-separados) no campo "Lançar Horas"
4. Clique em "Parsear" para processar
5. Confira o preview ao vivo e clique em "Gerar PDF"

## Deploy (GitHub Pages)

1. Crie um repositório no GitHub
2. Faça push deste projeto para o branch `main` (ou `gh-pages`)
3. No repositório, vá em Settings → Pages → selecione o branch
4. Pronto — o app estará disponível em `https://<user>.github.io/<repo>/`

O app é um único arquivo HTML (`index.html`) com zero dependências locais. Toda a persistência é via `localStorage`/`sessionStorage` do navegador.

## Stack

- HTML + CSS + JS puro (arquivo único, zero build)
- [pdfmake](https://pdfmake.org/) 0.2.12 (via CDN) para geração de PDF
- GitHub Pages para deploy
