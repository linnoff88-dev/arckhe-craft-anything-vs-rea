# Craft Anything êâ REA êâ kits do ARCKHê

Fatos conferidos em **10/11/2026**, sêÂ³ com fonte primêÂ¡ria: o README e os docs de cada repositêÂ³rio
e a API do GitHub. Craft Anything lido no commit `55aa8d3` (10/11/2026) e na versêÂ£o 0.6.0 rodando
aqui; REA lido no README atual do `main` (10/11/2026).

## Em uma frase

- **Craft Anything** estuda o original, manda um agente de cêÂ³digo construir a sua versêÂ£o e
  **confere sozinho** se ficou parecida, num app de janela (e numa linha de comando).
- **REA** liga o **seu** agente a ferramentas de engenharia reversa; o agente estuda, explica com
  prova e, se vocêÂª pedir, escreve e testa a sua versêÂ£o. A conferêÂªncia fica com vocêÂª e o agente.

## Tabela

| | Craft Anything | REA (Reverse Engineer Anything) |
|---|---|---|
| RepositêÂ³rio | `storytold/craft-anything` | `morluto/rea` |
| Criado no GitHub | 31/10/2026 | 14/04/2026 |
| Estrelas (10/11/2026) | ~26,2 mil | ~450 mil |
| Linguagem | Rust | TypeScript (Node.js) |
| LicenêÂ§a | MIT **ou** Apache-2.0, êÂ  sua escolha | MIT |
| VersêÂ£o | 0.6.0 (09/11/2026), "early alpha" | `rea-agents` 6.8.0 (25/10/2026) |
| Como se usa | App de janela (modo simples e avanêÂ§ado), CLI `craft-anything-cli` e servidor MCP | Servidor MCP + CLI `rea` para o seu agente; instala com `npx rea-agents setup` |
| Quem estuda | O prêÂ³prio Craft Anything (320 ferramentas no README; a CLI 0.6.0 lista 322 comandos) | O seu agente, chamando as ferramentas do REA |
| Quem constrêÂ³i | Um agente de cêÂ³digo que ele chama: Claude Code primeiro; Copilot CLI e Grok por ACP; adaptador do Codex "ainda nêÂ£o verificado" | O seu prêÂ³prio agente (Claude Code, Codex, Cursor, Gemini CLI, Grok Build e outros) |
| Como confere | Sozinho: compara prints em 3 larguras (padrêÂ£o 1440, 768 e 390 px) e refina atêÂ© "Good enough" (padrêÂ£o 90%) | NêÂ£o tem etapa de conferêÂªncia visual pronta; o agente testa o que escreveu |
| Sala limpa | **PadrêÂ£o.** SêÂ³ usa o que um visitante vêÂª; ferramentas que olham por dentro sêÂ£o recusadas | NêÂ£o tem um modo com esse nome; o README pede uso sêÂ³ em software seu ou que vocêÂª pode examinar |
| Olhar por dentro | Modo **Deep**: lêÂª cêÂ³digo e arquivos com motores prêÂ³prios e Ghidra, se instalado | êâ° o forte dele: Hopper, Ghidra, IDA ou Kuna; JS/Electron, .NET, Android, Go, Rust, firmware, sites e muito mais |
| Alvos | Sites, apps de computador, apps de celular, jogos e arquivos | BinêÂ¡rios nativos, JS/Electron, .NET, Android, sites, capturas de rede, firmware, bancos SQLite, entre outros |
| Sistemas | Windows, macOS, Linux (inclusive ARM64), FreeBSD; visualizador web em WebAssembly | Onde roda Node.js 22/24/26; cada alvo tem seus requisitos |
| êâ° uma caixa isolada? | **NêÂ£o.** O README avisa: sala limpa êÂ© regra do que ele oferece, nêÂ£o um sandbox; o agente age como vocêÂª | NêÂ£o. As anêÂ¡lises rodam "com as permissêÂµes do seu usuêÂ¡rio" |
| Limites que eles mesmos declaram | NêÂ£o contorna DRM, login nem anti-cheat; manda o agente nêÂ£o copiar logo, fotos e textos | Uso ilegal ou nêÂ£o autorizado nêÂ£o êÂ© aceito; ferramentas comerciais sêÂ³ com licenêÂ§a legal |

## "O Craft Anything êÂ© o pai do REA?"

**NêÂ£o, pelas fontes.** O REA nasceu seis meses e meio antes (abril êâ outubro de 2026), êÂ© de outro
dono, em outra linguagem, e nenhum dos dois READMEs cita o outro. TambêÂ©m nêÂ£o êÂ© verdade que o REA
"sêÂ³ mostra como funciona": o README dele diz que o agente pode "construir uma versêÂ£o para o seu
projeto". A diferenêÂ§a real êÂ© de **pacote**: o Craft Anything junta estudar + construir + conferir
num app sêÂ³, com a sala limpa ligada de fêÂ¡brica; o REA êÂ© a caixa de ferramentas de estudo mais
funda, e a construêÂ§êÂ£o fica com o agente que vocêÂª jêÂ¡ usa.

## Quando usar cada um

- **Quer refazer um site, app simples ou jogo do seu jeito, sem programar e sem ler cêÂ³digo de
  ninguêÂ©m:** Craft Anything em sala limpa, com o modo automêÂ¡tico desligado (ele pergunta antes de
  rodar comandos). Confira depois com `conferir/funcoes.py`: a nota visual nêÂ£o prova que funciona.
- **Quer entender COMO uma funêÂ§êÂ£o de um programa funciona por dentro** (um algoritmo, um formato
  de arquivo, um app instalado que êÂ© seu): REA. Guia testado:
  [rea-engenharia-reversa](https://linnoff88-dev.github.io/
- **Quer que o agente prove o que diz que entendeu:** [rea-com-provas](https://linnoff88-dev.github.io/
  (conferidor em Python) e, para funêÂ§êÂµes da cêÂ³pia, o `conferir/funcoes.py` deste kit.
- **Quer tudo local, sem nuvem e sem recusa do modelo:** [rea-sem-travas](https://linnoff88-dev.github.io/
  (harness dsh + modelo aberto no Ollama + REA). O Craft Anything usa servidores locais sêÂ³ para
  perguntas e anêÂ¡lise; para construir, ele precisa de um agente de cêÂ³digo instalado.
- **Quer que o agente trabalhe numa caixa de verdade:** [caixa-do-agente](https://linnoff88-dev.github.io/
  (Docker descartêÂ¡vel, sem rede e sem os seus `.env`). Vale para os dois, jêÂ¡ que nenhum êÂ© sandbox.
- **Qualquer agente, qualquer ferramenta:** a etapa "Conferir" deste kit (`conferir/semelhanca.js`)
  nêÂ£o depende do Craft Anything nem do REA.

## Outros fatos do Craft Anything usados no guia (README e docs/claude-code.md, 10/11/2026)

- O Claude Code roda como processo filho, `claude -p ê¢â¬Â¦ --output-format stream-json`, com o seu login;
  o Craft Anything "nunca vêÂª" a sua conta.
- Com o modo automêÂ¡tico desligado, cada tipo de aêÂ§êÂ£o nova mostra um cartêÂ£o
  "Allow once / Always for this project / Don't allow"; com ele ligado (padrêÂ£o), "commands: allow"
  confia no construtor. No nosso teste (ligado) ele rodou `npm install` sem perguntar.
- O Flatpak "nêÂ£o consegue abrir um navegador", e estudar sites precisa disso.
- O AppImage traz a CLI tambêÂ©m: `<AppImage> --cli <comando>` (nêÂ£o testado aqui; usamos o `.tar.gz`).
- "Good enough" (Settings) = quêÂ£o parecido tem que ficar antes de parar de refinar; padrêÂ£o 90%, de 50 a 100%.
- Pasta de projetos padrêÂ£o: `Documents/Craft Anything`, com `craft.json`, `capture/`, `app/`, `checks/`,
  `investigation.cany/` e `inbox/`.

## Fontes

- Craft Anything: README.md, docs/claude-code.md e saêÂ­da da CLI 0.6.0 (`doctor`, `commands`,
  `settings-show`), em https://github.com/storytold/craft-anything (10/11/2026).
- REA: README.md do `main` em https://github.com/morluto/rea (10/11/2026).
- Datas de criaêÂ§êÂ£o, estrelas e versêÂµes: API do GitHub (`gh api repos/<dono>/<repo>` e `/releases/latest`), 10/11/2026.
