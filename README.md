# craft-anything-vs-rea

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![FaÃ§a a sua versÃ£o â€” Craft Anything Ã— REA](guia/assets/banner.jpg)](https://linnoff88-dev.github.io/

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## ðŸŽ¬ Assista ao vÃ­deo

**Craft Anything: aponte para um app e a IA faz a sua versÃ£o**: https://www.youtube.com/watch?v=Jx_lYjw6ioQ Â· versÃ£o vertical: https://www.youtube.com/watch?v=0atFUnqDXv8

## O que Ã©

O **Craft Anything** Ã© um programa aberto e gratuito que olha um site, app ou jogo, pede a um agente
de IA (como o Claude Code) para escrever a sua prÃ³pria versÃ£o do zero e compara o resultado com o
original. Este repositÃ³rio Ã© um guia para instalar e usar com seguranÃ§a, uma comparaÃ§Ã£o com o
**REA** (outra ferramenta aberta, que mostra como um programa funciona por dentro) e um teste real
feito aqui. O kit traz uma rÃ©gua de semelhanÃ§a e uma lista de funÃ§Ãµes para conferir a cÃ³pia com
qualquer agente. VocÃª precisa de um computador e de um agente de cÃ³digo logado; o kit pede
Node.js e Python 3.

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://linnoff88-dev.github.io/

## O que tem aqui

| Arquivo | Para quÃª |
|---|---|
| [`conferir/semelhanca.js`](conferir/semelhanca.js) | Compara o original com a sua versÃ£o em 1440, 820 e 390 px: nota de **estrutura**, nota de **cor**, prints lado a lado e mapa de diferenÃ§as. SaÃ­da 0/1/2. |
| [`conferir/funcoes.py`](conferir/funcoes.py) | Gera a lista de funÃ§Ãµes para testar (modelos `quadro-branco` com 16 funÃ§Ãµes e `generico`) e reprova enquanto faltar prova. |
| [`conferir/exemplos/funcoes-contador.js`](conferir/exemplos/funcoes-contador.js) | Teste de funÃ§Ã£o automÃ¡tico usado no teste real (modelo para copiar). |
| [`pedidos/`](pedidos/) | 5 pedidos prontos: sala limpa, meta de semelhanÃ§a, mudanÃ§a de marca, provas de funÃ§Ã£o, teste do quadro branco (PT, EN e ES). |
| [`COMPARACAO.md`](COMPARACAO.md) | Craft Anything Ã— REA Ã— nossos kits, sÃ³ com fatos de fonte primÃ¡ria (10/11/2026). |
| [`TESTE-AQUI.md`](TESTE-AQUI.md) | O teste real do Craft Anything 0.6.0 nesta mÃ¡quina, com nÃºmeros e o que barrou. |
| [`tests/rodar.sh`](tests/rodar.sh) | Testes do kit (sem internet). |

## Uso rÃ¡pido

```bash
git clone https://github.com/linnoff88-dev/craft-anything-vs-rea && cd craft-anything-vs-rea
npm install -g playwright && npx playwright install chromium   # uma vez sÃ³

# 1) ficou parecido? (estrutura nas 3 larguras; saÃ­da 0 = passou)
node conferir/semelhanca.js https://original.exemplo minha-versao/index.html --meta 85 --saida conferencia

# 2) funciona? (o agente marca [x] e escreve a prova em cada linha)
python3 conferir/funcoes.py gerar quadro-branco --nome "Rabisco" --saida checklist.md
python3 conferir/funcoes.py conferir checklist.md

# testes do kit
bash tests/rodar.sh
```

## O processo, do inÃ­cio ao fim

Quem faz: ðŸ§  vocÃª (ou sessÃ£o com o Nei) Â· âš™ï¸ script Â· ðŸ¤– agente de cÃ³digo (Claude Code pela assinatura).

1. ðŸ§  Escolher o original e conferir que pode estudÃ¡-lo (Ã© seu, Ã© aberto, ou sÃ³ o que um visitante vÃª).
2. ðŸ§  Instalar o Craft Anything da pÃ¡gina de versÃµes e conferir o SHA256 (`sha256sum` Ã— `SHA256SUMS.txt`).
3. ðŸ§  Instalar e logar o Claude Code (`claude auth status`); no app, Settings â†’ AI â†’ Harnesses â†’ Detect.
4. ðŸ§  Settings â†’ Safety â†’ Auto mode **desligado**; Settings â†’ General â†’ pasta dos projetos.
5. ðŸ¤– Make â†’ Clean room â†’ pedido (`pedidos/1-sala-limpa.md` ou `pedidos/5-teste-do-quadro-branco.md`) â†’ Start: o Craft Anything estuda, o agente constrÃ³i e ele confere.
6. âš™ï¸ `node conferir/semelhanca.js <original> <sua versÃ£o> --meta 85` â†’ tabela + `diferencas-*.png`.
7. âš™ï¸ `python3 conferir/funcoes.py gerar <modelo> --nome X --saida checklist.md`.
8. ðŸ¤– O agente testa cada funÃ§Ã£o e escreve a prova (`pedidos/4-provas-de-funcao.md`).
9. âš™ï¸ `python3 conferir/funcoes.py conferir checklist.md` â†’ 0 sÃ³ com todas provadas.
10. ðŸ¤– MudanÃ§a de marca (`pedidos/3-mudanca-de-marca.md`) e de novo os passos 6 e 9.
11. âš™ï¸ Antes de mudar o kit: `bash tests/rodar.sh` â†’ "TUDO OK".

## Craft Anything Ã— REA em 4 linhas

- **Craft Anything** (`storytold/craft-anything`, Rust, MIT ou Apache-2.0, 0.6.0 "early alpha"): estuda, manda construir e **confere sozinho**; sala limpa de fÃ¡brica.
- **REA** (`morluto/rea`, TypeScript, MIT): dÃ¡ ao **seu** agente ferramentas de engenharia reversa (Hopper, Ghidra, IDA, Kunaâ€¦); o agente estuda e pode escrever a sua versÃ£o.
- O REA nasceu antes (14/04/2026 Ã— 31/10/2026): o Craft Anything nÃ£o Ã© "o pai do REA".
- Nenhum dos dois Ã© caixa isolada: o agente age como vocÃª. Detalhes em [COMPARACAO.md](COMPARACAO.md).

## Kits relacionados

[rea-engenharia-reversa](https://linnoff88-dev.github.io/ Â·
[rea-com-provas](https://linnoff88-dev.github.io/ Â·
[rea-sem-travas](https://linnoff88-dev.github.io/ (tudo local: dsh + Ollama + REA) Â·
[caixa-do-agente](https://linnoff88-dev.github.io/ Â·
[site-inspirado](https://linnoff88-dev.github.io/ Â·
[site-que-vende](https://linnoff88-dev.github.io/

## LicenÃ§a

MIT. Craft Anything e REA sÃ£o projetos de terceiros, com as licenÃ§as deles.
Feito para a comunidade [ARCKHÉ AI](https://ARCKHÉ AI).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>