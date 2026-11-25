# craft-anything-vs-rea

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![FaêÂ§a a sua versêÂ£o ê¢â¬â Craft Anything êâ REA](guia/assets/banner.jpg)](https://linnoff88-dev.github.io/

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## ê°Å¸Å½Â¬ Assista ao vêÂ­deo

**Craft Anything: aponte para um app e a IA faz a sua versêÂ£o**: https://www.youtube.com/watch?v=Jx_lYjw6ioQ êÂ· versêÂ£o vertical: https://www.youtube.com/watch?v=0atFUnqDXv8

## O que êÂ©

O **Craft Anything** êÂ© um programa aberto e gratuito que olha um site, app ou jogo, pede a um agente
de IA (como o Claude Code) para escrever a sua prêÂ³pria versêÂ£o do zero e compara o resultado com o
original. Este repositêÂ³rio êÂ© um guia para instalar e usar com seguranêÂ§a, uma comparaêÂ§êÂ£o com o
**REA** (outra ferramenta aberta, que mostra como um programa funciona por dentro) e um teste real
feito aqui. O kit traz uma rêÂ©gua de semelhanêÂ§a e uma lista de funêÂ§êÂµes para conferir a cêÂ³pia com
qualquer agente. VocêÂª precisa de um computador e de um agente de cêÂ³digo logado; o kit pede
Node.js e Python 3.

## ê°Å¸ââ Guia de uso

Guia completo (landing + passo a passo): **https://linnoff88-dev.github.io/

## O que tem aqui

| Arquivo | Para quêÂª |
|---|---|
| [`conferir/semelhanca.js`](conferir/semelhanca.js) | Compara o original com a sua versêÂ£o em 1440, 820 e 390 px: nota de **estrutura**, nota de **cor**, prints lado a lado e mapa de diferenêÂ§as. SaêÂ­da 0/1/2. |
| [`conferir/funcoes.py`](conferir/funcoes.py) | Gera a lista de funêÂ§êÂµes para testar (modelos `quadro-branco` com 16 funêÂ§êÂµes e `generico`) e reprova enquanto faltar prova. |
| [`conferir/exemplos/funcoes-contador.js`](conferir/exemplos/funcoes-contador.js) | Teste de funêÂ§êÂ£o automêÂ¡tico usado no teste real (modelo para copiar). |
| [`pedidos/`](pedidos/) | 5 pedidos prontos: sala limpa, meta de semelhanêÂ§a, mudanêÂ§a de marca, provas de funêÂ§êÂ£o, teste do quadro branco (PT, EN e ES). |
| [`COMPARACAO.md`](COMPARACAO.md) | Craft Anything êâ REA êâ nossos kits, sêÂ³ com fatos de fonte primêÂ¡ria (10/11/2026). |
| [`TESTE-AQUI.md`](TESTE-AQUI.md) | O teste real do Craft Anything 0.6.0 nesta mêÂ¡quina, com nêÂºmeros e o que barrou. |
| [`tests/rodar.sh`](tests/rodar.sh) | Testes do kit (sem internet). |

## Uso rêÂ¡pido

```bash
git clone https://github.com/linnoff88-dev/craft-anything-vs-rea && cd craft-anything-vs-rea
npm install -g playwright && npx playwright install chromium   # uma vez sêÂ³

# 1) ficou parecido? (estrutura nas 3 larguras; saêÂ­da 0 = passou)
node conferir/semelhanca.js https://original.exemplo minha-versao/index.html --meta 85 --saida conferencia

# 2) funciona? (o agente marca [x] e escreve a prova em cada linha)
python3 conferir/funcoes.py gerar quadro-branco --nome "Rabisco" --saida checklist.md
python3 conferir/funcoes.py conferir checklist.md

# testes do kit
bash tests/rodar.sh
```

## O processo, do inêÂ­cio ao fim

Quem faz: ê°Å¸Â§Â  vocêÂª (ou sessêÂ£o com o Nei) êÂ· ê¢Å¡â¢ê¯Â¸Â script êÂ· ê°Å¸Â¤â agente de cêÂ³digo (Claude Code pela assinatura).

1. ê°Å¸Â§Â  Escolher o original e conferir que pode estudêÂ¡-lo (êÂ© seu, êÂ© aberto, ou sêÂ³ o que um visitante vêÂª).
2. ê°Å¸Â§Â  Instalar o Craft Anything da pêÂ¡gina de versêÂµes e conferir o SHA256 (`sha256sum` êâ `SHA256SUMS.txt`).
3. ê°Å¸Â§Â  Instalar e logar o Claude Code (`claude auth status`); no app, Settings ê¢â â AI ê¢â â Harnesses ê¢â â Detect.
4. ê°Å¸Â§Â  Settings ê¢â â Safety ê¢â â Auto mode **desligado**; Settings ê¢â â General ê¢â â pasta dos projetos.
5. ê°Å¸Â¤â Make ê¢â â Clean room ê¢â â pedido (`pedidos/1-sala-limpa.md` ou `pedidos/5-teste-do-quadro-branco.md`) ê¢â â Start: o Craft Anything estuda, o agente constrêÂ³i e ele confere.
6. ê¢Å¡â¢ê¯Â¸Â `node conferir/semelhanca.js <original> <sua versêÂ£o> --meta 85` ê¢â â tabela + `diferencas-*.png`.
7. ê¢Å¡â¢ê¯Â¸Â `python3 conferir/funcoes.py gerar <modelo> --nome X --saida checklist.md`.
8. ê°Å¸Â¤â O agente testa cada funêÂ§êÂ£o e escreve a prova (`pedidos/4-provas-de-funcao.md`).
9. ê¢Å¡â¢ê¯Â¸Â `python3 conferir/funcoes.py conferir checklist.md` ê¢â â 0 sêÂ³ com todas provadas.
10. ê°Å¸Â¤â MudanêÂ§a de marca (`pedidos/3-mudanca-de-marca.md`) e de novo os passos 6 e 9.
11. ê¢Å¡â¢ê¯Â¸Â Antes de mudar o kit: `bash tests/rodar.sh` ê¢â â "TUDO OK".

## Craft Anything êâ REA em 4 linhas

- **Craft Anything** (`storytold/craft-anything`, Rust, MIT ou Apache-2.0, 0.6.0 "early alpha"): estuda, manda construir e **confere sozinho**; sala limpa de fêÂ¡brica.
- **REA** (`morluto/rea`, TypeScript, MIT): dêÂ¡ ao **seu** agente ferramentas de engenharia reversa (Hopper, Ghidra, IDA, Kunaê¢â¬Â¦); o agente estuda e pode escrever a sua versêÂ£o.
- O REA nasceu antes (14/04/2026 êâ 31/10/2026): o Craft Anything nêÂ£o êÂ© "o pai do REA".
- Nenhum dos dois êÂ© caixa isolada: o agente age como vocêÂª. Detalhes em [COMPARACAO.md](COMPARACAO.md).

## Kits relacionados

[rea-engenharia-reversa](https://linnoff88-dev.github.io/ êÂ·
[rea-com-provas](https://linnoff88-dev.github.io/ êÂ·
[rea-sem-travas](https://linnoff88-dev.github.io/ (tudo local: dsh + Ollama + REA) êÂ·
[caixa-do-agente](https://linnoff88-dev.github.io/ êÂ·
[site-inspirado](https://linnoff88-dev.github.io/ êÂ·
[site-que-vende](https://linnoff88-dev.github.io/

## LicenêÂ§a

MIT. Craft Anything e REA sêÂ£o projetos de terceiros, com as licenêÂ§as deles.
Feito para a comunidade [ARCKHê AI](https://ARCKHê AI).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>