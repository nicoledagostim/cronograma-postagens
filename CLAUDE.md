# cronograma-postagens

## O que é
App pessoal pra organizar entregas de publicidade/posts — controle de prazos,
status e itens a publicar. Equivalente ao repositório `cronograma` que já está
no GitHub (`nicoledagostim/cronograma`), recriado aqui de forma organizada.

## Stack
- HTML/JS puro (sem build/framework)
- Supabase (banco de dados + login por link mágico)

## Comandos úteis
- Rodar localmente: abrir `index.html` direto no navegador (ou `python3 -m http.server`)
- Build: não tem (site estático)
- Deploy: GitHub Pages (ver seção Deploy)

## Convenções
- Estilo de código: manter tudo em `index.html` enquanto for pequeno; separar em
  arquivos (`style.css`, `app.js`) se crescer.
- Tabela principal no Supabase: `cards`

## Segredos e config
Projeto é HTML/JS puro (sem build/servidor), então o arquivo `.env` não é lido
automaticamente pelo navegador — ele serve só como **documentação** de quais
chaves o projeto usa (veja `.env.example`). As chaves reais de serviços como o
Supabase acabam ficando no próprio código JS, e isso é esperado *desde que seja
a chave certa*:

- **Chave anon/publishable do Supabase** → pode ficar no código, é feita pra
  ser pública. Mas só é segura se o **RLS (Row Level Security)** estiver
  ativado em todas as tabelas do projeto no Supabase — sem isso, qualquer
  pessoa com a URL do projeto lê/escreve os dados.
- **Chave service_role (ou qualquer "secret key")** → NUNCA pode ir pro
  código nem pro GitHub. Se um serviço pedir uma chave chamada "secret" ou
  "service_role", ela não pertence a um site estático — precisaria de um
  backend/função serverless.

Antes de deixar o repositório público no GitHub, confirmar RLS ativo em todas
as tabelas usadas (Authentication → Policies no painel do Supabase).

## Deploy
Site estático (HTML puro) → forma mais simples é GitHub Pages:
1. Repositório no GitHub com os arquivos na raiz (ou pasta `docs/`).
2. Settings → Pages → escolher a branch (`main`) e a pasta.
3. GitHub gera a URL pública (`https://<usuario>.github.io/<repo>/`).

## Notas
- Este projeto substitui o repositório antigo `nicoledagostim/cronograma`
  (mesma lógica, mesmo banco Supabase, código reorganizado). O antigo deve
  ser removido do GitHub manualmente após confirmar que este está no ar.
