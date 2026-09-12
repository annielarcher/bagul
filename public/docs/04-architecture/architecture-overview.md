# Arquitetura — Visão Geral

## Objetivo
Definir uma arquitetura que preserve o Music Model como fonte de verdade e permita evolução de editor simples para um produto musical multiplataforma.

## Princípio central

```text
                    ┌──────────────────────┐
                    │       UI / UX         │
                    └──────────┬───────────┘
                               │ comandos
                    ┌──────────▼───────────┐
                    │    Music Engine      │
                    │ regras + operações   │
                    └──────────┬───────────┘
                               │
                    ┌──────────▼───────────┐
                    │     Music Model      │
                    │ fonte de verdade     │
                    └──────┬─────┬─────┬───┘
                           │     │     │
                    ┌──────▼┐ ┌──▼───┐ ┌▼────────┐
                    │Render │ │Audio │ │Persist. │
                    └───────┘ └──────┘ └─────────┘
```

## Camadas

### 1. Presentation
Responsável por:
- interface;
- ferramentas;
- seleção;
- mouse/touch/keyboard;
- feedback visual;
- acessibilidade.

Não contém regras musicais.

### 2. Application
Orquestra casos de uso:
- criar partitura;
- inserir nota;
- apagar evento;
- reproduzir;
- salvar;
- exportar.

### 3. Domain
Contém:
- Music Model;
- Music Engine;
- regras de duração;
- métrica;
- pitch;
- claves;
- acidentes;
- vozes;
- relações musicais.

Esta é a camada mais protegida contra dependências de UI.

### 4. Infrastructure
Implementa detalhes externos:
- armazenamento;
- importação/exportação;
- renderer;
- áudio;
- browser APIs;
- backend futuro.

## Fluxo de edição

```text
Usuário
  ↓
Input Adapter
  ↓
Command / Use Case
  ↓
Music Engine
  ↓
Music Model
  ↓
Estado atualizado
  ├── Renderer
  ├── Playback
  └── Persistence
```

## Estado canônico
O documento musical estruturado é a fonte de verdade. SVG, Canvas, áudio e JSON serializado são representações ou projeções.

## Frontend
A implementação inicial pode utilizar React + TypeScript. Essa escolha fica registrada como direção técnica inicial, sujeita à validação do primeiro protótipo.

## Renderização
VexFlow é candidato para renderização de notação. O produto deve encapsular essa dependência atrás de uma interface própria para evitar acoplamento do domínio ao renderer.

## Áudio
Web Audio API e/ou Tone.js são candidatos. Playback recebe uma representação musical normalizada e não acessa elementos visuais.

## Persistência
Primeira versão pode trabalhar localmente com IndexedDB/localStorage. O modelo deve ser serializável e versionável para permitir sincronização em nuvem posteriormente.

## Futuro
A arquitetura suporta:
- MIDI;
- manuscrito;
- colaboração;
- cloud sync;
- importação/exportação;
- múltiplos renderers;
- plugins/extensões.

## Regra de dependência
Dependências devem apontar para dentro:

```text
UI → Application → Domain
Infrastructure → Application/Domain interfaces
```

O Domain não conhece React, VexFlow, DOM, Canvas ou Web Audio.