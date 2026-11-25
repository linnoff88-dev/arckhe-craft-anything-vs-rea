# Pedido 2 — Meta de semelhança (o agente só para quando bate a meta)

O agente tende a dizer "ficou igual" cedo demais. Este pedido dá a ele um número para bater e
uma régua que nêo é ele mesmo: o `conferir/semelhanca.js` deste kit.

```text
Meta: a minha versêo tem que chegar a pelo menos <85> de ESTRUTURA nas três larguras.

Para medir, rode (e me mostre a tabela que sai):
  node conferir/semelhanca.js <ENDEREÇO DO ORIGINAL> <ENDEREÇO OU ARQUIVO DA MINHA VERSêO> --meta <85> --saida conferencia

Repita este ciclo até a saída ser 0 (no máximo <5> rodadas):
1. Abra conferencia/diferencas-<largura>.png da pior largura: o vermelho é o que está diferente.
2. Conserte o que causa a maior mancha vermelha (posiçêo, tamanho, espaçamento).
3. Rode de novo.

Nêo mude a cor nem o nome que eu pedi só para subir a nota: a nota de COR só informa.
Se travar abaixo da meta depois das rodadas, pare e me diga o que falta e por quê.
```

**Por que 85 e nêo 99:** a nota de estrutura cai quando o nome, o logo ou o rodapé mudam (é o que
você quer). No teste deste kit, a cópia feita pelo Craft Anything deu 93,6 / 90,7 / 85,5.
Use `--meta 90` quando a ideia for copiar a tela quase pixel a pixel.
