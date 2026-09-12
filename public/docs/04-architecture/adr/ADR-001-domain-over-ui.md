# ADR-001 — Separar interação do modelo musical

## Contexto
O produto terá múltiplos métodos de entrada.

## Decisão
Todas as entradas convergem para operações do domínio musical. A UI não manipula a representação gráfica como fonte de verdade.

## Consequência
Mouse, toque, teclado, MIDI e manuscrito podem compartilhar as mesmas regras.