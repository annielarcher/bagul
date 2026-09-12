# Architecture Overview

## Camadas

### Presentation
Interface, ferramentas, seleção, feedback e adaptação aos dispositivos.

### Music Engine
Regras musicais, validação, posicionamento e preenchimento de compassos.

### Music Model
Representação estruturada da partitura.

### Rendering
Transforma o modelo em notação visual.

### Audio
Transforma o modelo em execução sonora.

### Persistence
Salva e recupera o modelo.

**Regra:** SVG/canvas nunca é a fonte de verdade da partitura.