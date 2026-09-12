# Padrões de Código

## Objetivo

Manter o código legível, previsível e adequado para evolução do editor musical.

## Linguagem

TypeScript será a linguagem principal do frontend e do Music Engine.

JavaScript poderá existir apenas em pontos exigidos pela infraestrutura ou por integrações específicas.

## Princípios

1. **Domínio primeiro:** regras musicais pertencem ao Music Engine.
2. **UI sem regra musical:** componentes React não decidem validade rítmica, pitch, capacidade de compasso ou relações musicais.
3. **Funções pequenas:** cada função deve ter uma responsabilidade clara.
4. **Tipos explícitos no domínio:** evitar `any` em estruturas musicais.
5. **Dados imutáveis quando isso simplificar undo/redo e previsibilidade.**
6. **IDs estáveis:** eventos, compassos, vozes e demais entidades persistíveis devem possuir identificadores estáveis.
7. **Sem estado duplicado:** o Music Model é a fonte canônica da partitura.
8. **Erros explícitos:** operações inválidas devem produzir resultado de erro compreensível, nunca alterar silenciosamente a partitura.

## Organização conceitual

```text
src/
├── app/
├── components/
├── features/
├── music/
│   ├── domain/
│   ├── engine/
│   ├── model/
│   └── notation/
├── renderer/
├── audio/
├── persistence/
└── shared/
```

## Convenções de domínio

Preferir verbos de operação claros:

- `createScore()`
- `insertNote()`
- `insertRest()`
- `insertChord()`
- `deleteEvent()`
- `changeDuration()`
- `changeClef()`
- `changeTimeSignature()`

Evitar nomes que revelem implementação gráfica, como `drawNote()` no domínio.

## Regra de dependências

```text
UI → Application → Domain
UI → Adapters → Infrastructure

Domain ✕ React
Domain ✕ VexFlow
Domain ✕ DOM
Domain ✕ Web Audio
```

## Comentários

Comentar decisões e motivos, não código óbvio.

Quando uma regra musical for contraintuitiva, documentar o raciocínio junto ao domínio e, quando relevante, adicionar teste que funcione como exemplo executável.