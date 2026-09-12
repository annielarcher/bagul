# ADR-003 — Isolamento do Renderer

## Status
Aceita

## Contexto
O editor precisa desenhar notação musical com uma biblioteca especializada, mas o Music Model não pode depender da tecnologia usada para desenhá-lo.

## Decisão
Encapsular o renderer atrás de uma interface própria da aplicação. VexFlow é o candidato inicial, mas não será usado diretamente pelo domínio.

## Consequências
### Positivas
- troca futura de renderer;
- testes do Music Engine sem DOM;
- possibilidade de renderers diferentes;
- menor acoplamento.

### Negativas
- criação de uma camada de adaptação;
- algumas capacidades específicas do renderer precisam ser abstraídas.

## Regra
Nenhum objeto do domínio deve conter instâncias de VexFlow, SVG ou elementos DOM.