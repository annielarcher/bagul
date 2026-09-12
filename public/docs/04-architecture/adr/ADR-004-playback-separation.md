# ADR-004 — Separação do Playback

## Status
Aceita

## Contexto
O produto precisa ouvir a partitura, mas áudio e representação gráfica têm necessidades diferentes.

## Decisão
Playback será um consumidor do Music Model, separado do Renderer.

## Consequências
- o áudio pode evoluir independentemente da interface;
- testes de duração e andamento podem ocorrer sem renderização;
- MIDI futuro pode compartilhar uma representação musical normalizada;
- o áudio não dependerá de scraping do SVG.

## Regra
A fonte do playback é o Music Model validado.