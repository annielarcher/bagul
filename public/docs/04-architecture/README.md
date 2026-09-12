# 04 — Architecture

```text
Entrada
  ↓
Music Engine
  ↓
Music Model
  ├── Renderer
  └── Audio Engine
```

Mouse, toque, teclado, MIDI e manuscrito devem convergir para o mesmo núcleo. A UI solicita operações ao Music Engine; ela não implementa regras musicais.