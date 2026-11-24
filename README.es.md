# craft-anything-vs-rea

[![Haz tu versiÃ³n â€” Craft Anything Ã— REA](guia/assets/banner-es.jpg)](https://linnoff88-dev.github.io/

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## ðŸŽ¬ Mira el video

**Craft Anything: apunta a una app y la IA hace tu versiÃ³n** (en portuguÃ©s): https://www.youtube.com/watch?v=Jx_lYjw6ioQ Â· versiÃ³n vertical: https://www.youtube.com/watch?v=0atFUnqDXv8

## QuÃ© es

**Craft Anything** es un programa abierto y gratuito que observa un sitio web, una app o un juego, le pide a un agente de IA (como Claude Code) que escriba su propia versiÃ³n desde cero y compara el resultado con el original. Este repositorio es una guÃ­a para instalarlo y usarlo de forma segura, una comparaciÃ³n con **REA** (otra herramienta abierta que muestra cÃ³mo funciona un programa por dentro) y una prueba real hecha aquÃ­. El kit incluye una regla para medir la similitud y una lista de funciones para revisar la copia con cualquier agente. Necesitas una computadora y una sesiÃ³n iniciada en un agente de cÃ³digo; el kit requiere Node.js y Python 3.

## ðŸ“– GuÃ­a de uso

GuÃ­a completa (pÃ¡gina de inicio + paso a paso): **https://linnoff88-dev.github.io/

## QuÃ© hay aquÃ­

| Archivo | Para quÃ© sirve |
|---|---|
| [`conferir/semelhanca.js`](conferir/semelhanca.js) | Compara el original con tu versiÃ³n en 1440, 820 y 390 px: puntuaciÃ³n de **estructura**, puntuaciÃ³n de **color**, capturas lado a lado y mapa de diferencias. Resultado 0/1/2. |
| [`conferir/funcoes.py`](conferir/funcoes.py) | Genera la lista de funciones para probar (modelos `quadro-branco` con 16 funciones y `generico`) y no aprueba mientras falten pruebas. |
| [`conferir/exemplos/funcoes-contador.js`](conferir/exemplos/funcoes-contador.js) | Prueba automÃ¡tica de funciones usada en la prueba real (modelo para copiar). |
| [`pedidos/`](pedidos/es/) | 5 pedidos listos: sala limpia, meta de similitud, cambio de marca, pruebas de funciones y prueba del tablero blanco (PT, EN y ES). |
| [`COMPARACAO.md`](COMPARACAO.md) (en portuguÃ©s) | Craft Anything Ã— REA Ã— nuestros kits, solo con datos de fuentes primarias (10/11/2026). |
| [`TESTE-AQUI.md`](TESTE-AQUI.md) (en portuguÃ©s) | La prueba real de Craft Anything 0.6.0 en esta computadora, con cifras y lo que lo bloqueÃ³. |
| [`tests/rodar.sh`](tests/rodar.sh) | Pruebas del kit (sin internet). |

## Uso rÃ¡pido

```bash
git clone https://github.com/linnoff88-dev/craft-anything-vs-rea && cd craft-anything-vs-rea
npm install -g playwright && npx playwright install chromium   # solo una vez

# 1) Â¿Se parece? (estructura en los 3 anchos; resultado 0 = aprobado)
node conferir/semelhanca.js https://original.exemplo minha-versao/index.html --meta 85 --saida conferencia

# 2) Â¿Funciona? (el agente marca [x] y escribe la prueba en cada lÃ­nea)
python3 conferir/funcoes.py gerar quadro-branco --nome "Rabisco" --saida checklist.md
python3 conferir/funcoes.py conferir checklist.md

# pruebas del kit
bash tests/rodar.sh
```

## El proceso, de principio a fin

QuiÃ©n lo hace: ðŸ§  tÃº (o una sesiÃ³n con Nei) Â· âš™ï¸ script Â· ðŸ¤– agente de cÃ³digo (Claude Code con la suscripciÃ³n).

1. ðŸ§  Elegir el original y confirmar que puedes estudiarlo (es tuyo, es abierto o solo observarÃ¡s lo que ve un visitante).
2. ðŸ§  Instalar Craft Anything desde la pÃ¡gina de versiones y comprobar el SHA256 (`sha256sum` Ã— `SHA256SUMS.txt`).
3. ðŸ§  Instalar Claude Code e iniciar sesiÃ³n (`claude auth status`); en la app, Settings â†’ AI â†’ Harnesses â†’ Detect.
4. ðŸ§  Settings â†’ Safety â†’ Auto mode **desactivado**; Settings â†’ General â†’ carpeta de proyectos.
5. ðŸ¤– Make â†’ Clean room â†’ pedido (`pedidos/1-sala-limpa.md` o `pedidos/5-teste-do-quadro-branco.md`) â†’ Start: Craft Anything estudia, el agente construye y luego se revisa el resultado.
6. âš™ï¸ `node conferir/semelhanca.js <original> <sua versÃ£o> --meta 85` â†’ tabla + `diferencas-*.png`.
7. âš™ï¸ `python3 conferir/funcoes.py gerar <modelo> --nome X --saida checklist.md`.
8. ðŸ¤– El agente prueba cada funciÃ³n y escribe la prueba (`pedidos/4-provas-de-funcao.md`).
9. âš™ï¸ `python3 conferir/funcoes.py conferir checklist.md` â†’ solo da 0 si todas tienen pruebas.
10. ðŸ¤– Cambio de marca (`pedidos/3-mudanca-de-marca.md`) y repetir los pasos 6 y 9.
11. âš™ï¸ Antes de cambiar el kit: `bash tests/rodar.sh` â†’ Â«TODO OKÂ».

## Craft Anything Ã— REA en 4 lÃ­neas

- **Craft Anything** (`storytold/craft-anything`, Rust, MIT o Apache-2.0, 0.6.0 "early alpha"): estudia, pide que lo construyan y **lo revisa por sÃ­ solo**; incluye sala limpia de fÃ¡brica.
- **REA** (`morluto/rea`, TypeScript, MIT): ofrece a **tu** agente herramientas de ingenierÃ­a inversa (Hopper, Ghidra, IDA, Kunaâ€¦); el agente estudia y puede escribir su versiÃ³n.
- REA naciÃ³ antes (14/04/2026 Ã— 31/10/2026): Craft Anything no es Â«el padre de REAÂ».
- Ninguno de los dos funciona de forma aislada: el agente actÃºa como tÃº. MÃ¡s detalles en [COMPARACAO.md](COMPARACAO.md) (en portuguÃ©s).

## Kits relacionados

[rea-engenharia-reversa](https://linnoff88-dev.github.io/ Â·
[rea-com-provas](https://linnoff88-dev.github.io/ Â·
[rea-sem-travas](https://linnoff88-dev.github.io/ (todo local: dsh + Ollama + REA) Â·
[caixa-do-agente](https://linnoff88-dev.github.io/ Â·
[site-inspirado](https://linnoff88-dev.github.io/ Â·
[site-que-vende](https://linnoff88-dev.github.io/

## Licencia

MIT. Craft Anything y REA son proyectos de terceros, cada uno con su propia licencia.
Hecho para la comunidad [ARCKHÉ AI](https://ARCKHÉ AI).