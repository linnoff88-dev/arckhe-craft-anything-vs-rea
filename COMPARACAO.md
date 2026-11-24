# Craft Anything Ã— REA Ã— kits do ARCKHÉ

Fatos conferidos em **10/11/2026**, sÃ³ com fonte primÃ¡ria: o README e os docs de cada repositÃ³rio
e a API do GitHub. Craft Anything lido no commit `55aa8d3` (10/11/2026) e na versÃ£o 0.6.0 rodando
aqui; REA lido no README atual do `main` (10/11/2026).

## Em uma frase

- **Craft Anything** estuda o original, manda um agente de cÃ³digo construir a sua versÃ£o e
  **confere sozinho** se ficou parecida, num app de janela (e numa linha de comando).
- **REA** liga o **seu** agente a ferramentas de engenharia reversa; o agente estuda, explica com
  prova e, se vocÃª pedir, escreve e testa a sua versÃ£o. A conferÃªncia fica com vocÃª e o agente.

## Tabela

| | Craft Anything | REA (Reverse Engineer Anything) |
|---|---|---|
| RepositÃ³rio | `storytold/craft-anything` | `morluto/rea` |
| Criado no GitHub | 31/10/2026 | 14/04/2026 |
| Estrelas (10/11/2026) | ~26,2 mil | ~450 mil |
| Linguagem | Rust | TypeScript (Node.js) |
| LicenÃ§a | MIT **ou** Apache-2.0, Ã  sua escolha | MIT |
| VersÃ£o | 0.6.0 (09/11/2026), "early alpha" | `rea-agents` 6.8.0 (25/10/2026) |
| Como se usa | App de janela (modo simples e avanÃ§ado), CLI `craft-anything-cli` e servidor MCP | Servidor MCP + CLI `rea` para o seu agente; instala com `npx rea-agents setup` |
| Quem estuda | O prÃ³prio Craft Anything (320 ferramentas no README; a CLI 0.6.0 lista 322 comandos) | O seu agente, chamando as ferramentas do REA |
| Quem constrÃ³i | Um agente de cÃ³digo que ele chama: Claude Code primeiro; Copilot CLI e Grok por ACP; adaptador do Codex "ainda nÃ£o verificado" | O seu prÃ³prio agente (Claude Code, Codex, Cursor, Gemini CLI, Grok Build e outros) |
| Como confere | Sozinho: compara prints em 3 larguras (padrÃ£o 1440, 768 e 390 px) e refina atÃ© "Good enough" (padrÃ£o 90%) | NÃ£o tem etapa de conferÃªncia visual pronta; o agente testa o que escreveu |
| Sala limpa | **PadrÃ£o.** SÃ³ usa o que um visitante vÃª; ferramentas que olham por dentro sÃ£o recusadas | NÃ£o tem um modo com esse nome; o README pede uso sÃ³ em software seu ou que vocÃª pode examinar |
| Olhar por dentro | Modo **Deep**: lÃª cÃ³digo e arquivos com motores prÃ³prios e Ghidra, se instalado | Ã‰ o forte dele: Hopper, Ghidra, IDA ou Kuna; JS/Electron, .NET, Android, Go, Rust, firmware, sites e muito mais |
| Alvos | Sites, apps de computador, apps de celular, jogos e arquivos | BinÃ¡rios nativos, JS/Electron, .NET, Android, sites, capturas de rede, firmware, bancos SQLite, entre outros |
| Sistemas | Windows, macOS, Linux (inclusive ARM64), FreeBSD; visualizador web em WebAssembly | Onde roda Node.js 22/24/26; cada alvo tem seus requisitos |
| Ã‰ uma caixa isolada? | **NÃ£o.** O README avisa: sala limpa Ã© regra do que ele oferece, nÃ£o um sandbox; o agente age como vocÃª | NÃ£o. As anÃ¡lises rodam "com as permissÃµes do seu usuÃ¡rio" |
| Limites que eles mesmos declaram | NÃ£o contorna DRM, login nem anti-cheat; manda o agente nÃ£o copiar logo, fotos e textos | Uso ilegal ou nÃ£o autorizado nÃ£o Ã© aceito; ferramentas comerciais sÃ³ com licenÃ§a legal |

## "O Craft Anything Ã© o pai do REA?"

**NÃ£o, pelas fontes.** O REA nasceu seis meses e meio antes (abril Ã— outubro de 2026), Ã© de outro
dono, em outra linguagem, e nenhum dos dois READMEs cita o outro. TambÃ©m nÃ£o Ã© verdade que o REA
"sÃ³ mostra como funciona": o README dele diz que o agente pode "construir uma versÃ£o para o seu
projeto". A diferenÃ§a real Ã© de **pacote**: o Craft Anything junta estudar + construir + conferir
num app sÃ³, com a sala limpa ligada de fÃ¡brica; o REA Ã© a caixa de ferramentas de estudo mais
funda, e a construÃ§Ã£o fica com o agente que vocÃª jÃ¡ usa.

## Quando usar cada um

- **Quer refazer um site, app simples ou jogo do seu jeito, sem programar e sem ler cÃ³digo de
  ninguÃ©m:** Craft Anything em sala limpa, com o modo automÃ¡tico desligado (ele pergunta antes de
  rodar comandos). Confira depois com `conferir/funcoes.py`: a nota visual nÃ£o prova que funciona.
- **Quer entender COMO uma funÃ§Ã£o de um programa funciona por dentro** (um algoritmo, um formato
  de arquivo, um app instalado que Ã© seu): REA. Guia testado:
  [rea-engenharia-reversa](https://linnoff88-dev.github.io/
- **Quer que o agente prove o que diz que entendeu:** [rea-com-provas](https://linnoff88-dev.github.io/
  (conferidor em Python) e, para funÃ§Ãµes da cÃ³pia, o `conferir/funcoes.py` deste kit.
- **Quer tudo local, sem nuvem e sem recusa do modelo:** [rea-sem-travas](https://linnoff88-dev.github.io/
  (harness dsh + modelo aberto no Ollama + REA). O Craft Anything usa servidores locais sÃ³ para
  perguntas e anÃ¡lise; para construir, ele precisa de um agente de cÃ³digo instalado.
- **Quer que o agente trabalhe numa caixa de verdade:** [caixa-do-agente](https://linnoff88-dev.github.io/
  (Docker descartÃ¡vel, sem rede e sem os seus `.env`). Vale para os dois, jÃ¡ que nenhum Ã© sandbox.
- **Qualquer agente, qualquer ferramenta:** a etapa "Conferir" deste kit (`conferir/semelhanca.js`)
  nÃ£o depende do Craft Anything nem do REA.

## Outros fatos do Craft Anything usados no guia (README e docs/claude-code.md, 10/11/2026)

- O Claude Code roda como processo filho, `claude -p â€¦ --output-format stream-json`, com o seu login;
  o Craft Anything "nunca vÃª" a sua conta.
- Com o modo automÃ¡tico desligado, cada tipo de aÃ§Ã£o nova mostra um cartÃ£o
  "Allow once / Always for this project / Don't allow"; com ele ligado (padrÃ£o), "commands: allow"
  confia no construtor. No nosso teste (ligado) ele rodou `npm install` sem perguntar.
- O Flatpak "nÃ£o consegue abrir um navegador", e estudar sites precisa disso.
- O AppImage traz a CLI tambÃ©m: `<AppImage> --cli <comando>` (nÃ£o testado aqui; usamos o `.tar.gz`).
- "Good enough" (Settings) = quÃ£o parecido tem que ficar antes de parar de refinar; padrÃ£o 90%, de 50 a 100%.
- Pasta de projetos padrÃ£o: `Documents/Craft Anything`, com `craft.json`, `capture/`, `app/`, `checks/`,
  `investigation.cany/` e `inbox/`.

## Fontes

- Craft Anything: README.md, docs/claude-code.md e saÃ­da da CLI 0.6.0 (`doctor`, `commands`,
  `settings-show`), em https://github.com/storytold/craft-anything (10/11/2026).
- REA: README.md do `main` em https://github.com/morluto/rea (10/11/2026).
- Datas de criaÃ§Ã£o, estrelas e versÃµes: API do GitHub (`gh api repos/<dono>/<repo>` e `/releases/latest`), 10/11/2026.
