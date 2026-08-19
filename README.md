# Minha Coleção Hot Wheels — BMW · Porsche · Ferrari

App de checklist para a coleção de miniaturas Hot Wheels, gerado a partir da planilha
`data/hotwheels_bmw_porsche_ferrari_checklist.xlsx` (2.048 lançamentos/variações + 260 castings,
pesquisa fechada em 15/08/2026).

É **um único arquivo** (`index.html`): funciona offline, no celular e no computador, sem instalar nada.

## Como usar

**Opção 1 — GitHub Pages (recomendado para usar no celular):**
1. Neste repositório, vá em **Settings → Pages**.
2. Em *Build and deployment*, escolha **Deploy from a branch** e selecione a branch com o app (pasta `/root`).
3. Abra a URL gerada (algo como `https://ov3r-k1.github.io/hot-wheels-/`) e, no celular,
   use "Adicionar à tela inicial" para virar um app.

**Opção 2 — Arquivo local:** baixe o `index.html` e abra no navegador. Pronto.

## O que o app faz

- **Painel** com o progresso geral e por marca (tenho / a caminho / faltam) e atalhos:
  prioridade 1 em falta, itens a caminho, novidades 2026, itens fotografados.
- **Checklist**: em cada card, marque **✗ Falta · 🚚 A caminho · ✓ Tenho**. Salva sozinho.
- **Imagem da miniatura e do blister** em cada item:
  - **📷 Minha foto** — fotografe a miniatura solta e o blister (no celular abre a câmera).
    As fotos ficam guardadas no próprio navegador (IndexedDB), redimensionadas para economizar espaço.
  - **🌐 Wiki** — busca as fotos da página do casting na Hot Wheels Wiki (Fandom) e deixa você
    escolher; quando a linha da tabela tem o **mesmo Toy #**, ela vem marcada com ✓.
  - **Capas automáticas** — online, os cards sem foto recebem uma foto do casting **na cartela/blister**
    (ou a imagem principal da página, quando não há foto de cartela).
- **Busca** (casting, modelo, série, cor, Toy #, tampo, ano…) e **filtros** com contagem:
  status, ano, tipo, raridade, prioridade, escala/escopo, situação e com/sem foto.
- **Castings**: um card por molde com o range de anos, total de versões e seu progresso — toque
  para ver todas as versões daquele molde.
- **Tooned**: todo carro em estilo Tooned, de qualquer marca. Soma o que já existe na planilha
  (castings com "Tooned" no nome e os lançamentos da série Tooned) com **todos os outros castings
  Tooned da Hot Wheels Wiki**, buscados ao abrir a aba.
- **Kool Kombi**: todas as versões desse casting. Como ele é Volkswagen e a planilha cobre só
  BMW/Porsche/Ferrari, a lista vem inteira da Hot Wheels Wiki.

  Nas duas abas o conteúdo da wiki é lido no navegador (precisa de internet) e vira item normal:
  dá para marcar, fotografar, anotar e tudo entra no backup. As marcações são presas ao
  casting + ano + Toy # + cor, então sobrevivem a recarregamentos. Offline, a aba Tooned mostra
  só o que é da planilha e a Kool Kombi explica que precisa de conexão.
- **Detalhe completo** de cada item com todos os campos da planilha, links para as fontes e
  campo de **nota pessoal** (onde comprou, preço, estado…).
- **Backup**: exporte um `.json` com marcações, notas e fotos; importe em outro aparelho.
  Sem backup, os dados vivem só no navegador em que foram criados.

## Estrutura do repositório

| Caminho | O que é |
|---|---|
| `index.html` | O app pronto (gerado — não edite à mão) |
| `app/template.html` | Código-fonte do app (HTML/CSS/JS) |
| `tools/build.py` | Gera o `index.html` a partir da planilha + template |
| `data/…checklist.xlsx` | A planilha original com todos os dados |
| `manifest.webmanifest` + `icons/` | Nome e ícone do app na tela inicial do celular |

## Atualizar os dados

Editou a planilha (novos lançamentos de 2026, correções)? Regenere o app:

```bash
pip install openpyxl   # uma vez
python3 tools/build.py
```

O script lê as abas BMW / Porsche / Ferrari / Outras linhas / Castings / Guia / Fontes e
reconstrói o `index.html`. As marcações e fotos dos usuários não são afetadas — elas ficam
no navegador, fora do arquivo.
