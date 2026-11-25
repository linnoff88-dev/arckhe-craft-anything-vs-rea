# craft-anything-vs-rea

[![Haz tu versiêÂ³n ê¢â¬â Craft Anything êâ REA](guia/assets/banner-es.jpg)](https://linnoff88-dev.github.io/

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## ê°Å¸Å½Â¬ Mira el video

**Craft Anything: apunta a una app y la IA hace tu versiêÂ³n** (en portuguêÂ©s): https://www.youtube.com/watch?v=Jx_lYjw6ioQ êÂ· versiêÂ³n vertical: https://www.youtube.com/watch?v=0atFUnqDXv8

## QuêÂ© es

**Craft Anything** es un programa abierto y gratuito que observa un sitio web, una app o un juego, le pide a un agente de IA (como Claude Code) que escriba su propia versiêÂ³n desde cero y compara el resultado con el original. Este repositorio es una guêÂ­a para instalarlo y usarlo de forma segura, una comparaciêÂ³n con **REA** (otra herramienta abierta que muestra cêÂ³mo funciona un programa por dentro) y una prueba real hecha aquêÂ­. El kit incluye una regla para medir la similitud y una lista de funciones para revisar la copia con cualquier agente. Necesitas una computadora y una sesiêÂ³n iniciada en un agente de cêÂ³digo; el kit requiere Node.js y Python 3.

## ê°Å¸ââ GuêÂ­a de uso

GuêÂ­a completa (pêÂ¡gina de inicio + paso a paso): **https://linnoff88-dev.github.io/

## QuêÂ© hay aquêÂ­

| Archivo | Para quêÂ© sirve |
|---|---|
| [`conferir/semelhanca.js`](conferir/semelhanca.js) | Compara el original con tu versiêÂ³n en 1440, 820 y 390 px: puntuaciêÂ³n de **estructura**, puntuaciêÂ³n de **color**, capturas lado a lado y mapa de diferencias. Resultado 0/1/2. |
| [`conferir/funcoes.py`](conferir/funcoes.py) | Genera la lista de funciones para probar (modelos `quadro-branco` con 16 funciones y `generico`) y no aprueba mientras falten pruebas. |
| [`conferir/exemplos/funcoes-contador.js`](conferir/exemplos/funcoes-contador.js) | Prueba automêÂ¡tica de funciones usada en la prueba real (modelo para copiar). |
| [`pedidos/`](pedidos/es/) | 5 pedidos listos: sala limpia, meta de similitud, cambio de marca, pruebas de funciones y prueba del tablero blanco (PT, EN y ES). |
| [`COMPARACAO.md`](COMPARACAO.md) (en portuguêÂ©s) | Craft Anything êâ REA êâ nuestros kits, solo con datos de fuentes primarias (10/11/2026). |
| [`TESTE-AQUI.md`](TESTE-AQUI.md) (en portuguêÂ©s) | La prueba real de Craft Anything 0.6.0 en esta computadora, con cifras y lo que lo bloqueêÂ³. |
| [`tests/rodar.sh`](tests/rodar.sh) | Pruebas del kit (sin internet). |

## Uso rêÂ¡pido

```bash
git clone https://github.com/linnoff88-dev/craft-anything-vs-rea && cd craft-anything-vs-rea
npm install -g playwright && npx playwright install chromium   # solo una vez

# 1) êÂ¿Se parece? (estructura en los 3 anchos; resultado 0 = aprobado)
node conferir/semelhanca.js https://original.exemplo minha-versao/index.html --meta 85 --saida conferencia

# 2) êÂ¿Funciona? (el agente marca [x] y escribe la prueba en cada lêÂ­nea)
python3 conferir/funcoes.py gerar quadro-branco --nome "Rabisco" --saida checklist.md
python3 conferir/funcoes.py conferir checklist.md

# pruebas del kit
bash tests/rodar.sh
```

## El proceso, de principio a fin

QuiêÂ©n lo hace: ê°Å¸Â§Â  têÂº (o una sesiêÂ³n con Nei) êÂ· ê¢Å¡â¢ê¯Â¸Â script êÂ· ê°Å¸Â¤â agente de cêÂ³digo (Claude Code con la suscripciêÂ³n).

1. ê°Å¸Â§Â  Elegir el original y confirmar que puedes estudiarlo (es tuyo, es abierto o solo observarêÂ¡s lo que ve un visitante).
2. ê°Å¸Â§Â  Instalar Craft Anything desde la pêÂ¡gina de versiones y comprobar el SHA256 (`sha256sum` êâ `SHA256SUMS.txt`).
3. ê°Å¸Â§Â  Instalar Claude Code e iniciar sesiêÂ³n (`claude auth status`); en la app, Settings ê¢â â AI ê¢â â Harnesses ê¢â â Detect.
4. ê°Å¸Â§Â  Settings ê¢â â Safety ê¢â â Auto mode **desactivado**; Settings ê¢â â General ê¢â â carpeta de proyectos.
5. ê°Å¸Â¤â Make ê¢â â Clean room ê¢â â pedido (`pedidos/1-sala-limpa.md` o `pedidos/5-teste-do-quadro-branco.md`) ê¢â â Start: Craft Anything estudia, el agente construye y luego se revisa el resultado.
6. ê¢Å¡â¢ê¯Â¸Â `node conferir/semelhanca.js <original> <sua versêÂ£o> --meta 85` ê¢â â tabla + `diferencas-*.png`.
7. ê¢Å¡â¢ê¯Â¸Â `python3 conferir/funcoes.py gerar <modelo> --nome X --saida checklist.md`.
8. ê°Å¸Â¤â El agente prueba cada funciêÂ³n y escribe la prueba (`pedidos/4-provas-de-funcao.md`).
9. ê¢Å¡â¢ê¯Â¸Â `python3 conferir/funcoes.py conferir checklist.md` ê¢â â solo da 0 si todas tienen pruebas.
10. ê°Å¸Â¤â Cambio de marca (`pedidos/3-mudanca-de-marca.md`) y repetir los pasos 6 y 9.
11. ê¢Å¡â¢ê¯Â¸Â Antes de cambiar el kit: `bash tests/rodar.sh` ê¢â â êÂ«TODO OKêÂ».

## Craft Anything êâ REA en 4 lêÂ­neas

- **Craft Anything** (`storytold/craft-anything`, Rust, MIT o Apache-2.0, 0.6.0 "early alpha"): estudia, pide que lo construyan y **lo revisa por sêÂ­ solo**; incluye sala limpia de fêÂ¡brica.
- **REA** (`morluto/rea`, TypeScript, MIT): ofrece a **tu** agente herramientas de ingenierêÂ­a inversa (Hopper, Ghidra, IDA, Kunaê¢â¬Â¦); el agente estudia y puede escribir su versiêÂ³n.
- REA naciêÂ³ antes (14/04/2026 êâ 31/10/2026): Craft Anything no es êÂ«el padre de REAêÂ».
- Ninguno de los dos funciona de forma aislada: el agente actêÂºa como têÂº. MêÂ¡s detalles en [COMPARACAO.md](COMPARACAO.md) (en portuguêÂ©s).

## Kits relacionados

[rea-engenharia-reversa](https://linnoff88-dev.github.io/ êÂ·
[rea-com-provas](https://linnoff88-dev.github.io/ êÂ·
[rea-sem-travas](https://linnoff88-dev.github.io/ (todo local: dsh + Ollama + REA) êÂ·
[caixa-do-agente](https://linnoff88-dev.github.io/ êÂ·
[site-inspirado](https://linnoff88-dev.github.io/ êÂ·
[site-que-vende](https://linnoff88-dev.github.io/

## Licencia

MIT. Craft Anything y REA son proyectos de terceros, cada uno con su propia licencia.
Hecho para la comunidad [ARCKHê AI](https://ARCKHê AI).