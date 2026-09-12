# ADR-005 — Stack do Primeiro Protótipo

**Status:** Accepted
**Data:** 2026-09-12

## Contexto

O produto é um editor de notação musical web orientado à captura rápida de ideias: **Abra → escreva → ouça → salve**.

A stack precisa permitir um primeiro protótipo funcional sem criar dependências desnecessárias, mantendo o domínio musical independente da interface e do mecanismo de renderização.

## Decisão

A stack inicial será:

- **React** — camada de interface;
- **TypeScript** — linguagem principal da aplicação;
- **Vite** — ferramenta de desenvolvimento/build do frontend;
- **Music Engine próprio em TypeScript** — regras musicais e operações do domínio;
- **VexFlow** — renderização da partitura;
- **Web Audio API** — reprodução inicial;
- **Tone.js** — evolução posterior do sistema de áudio, quando necessário;
- **Zustand** — estado da aplicação, mantendo o Music Model como fonte canônica;
- **IndexedDB** — persistência local das partituras;
- **Vitest + Testing Library** — testes unitários e de interface;
- **Playwright** — testes end-to-end;
- **OpenSheetMusicDisplay** — integração futura para MusicXML;
- **Backend/PostgreSQL** — somente quando contas, sincronização em nuvem, compartilhamento ou colaboração justificarem sua introdução.

## Princípio de isolamento

Nenhum componente de domínio poderá depender diretamente de React, VexFlow, DOM, SVG, Canvas ou Web Audio.

O fluxo principal será:

```text
Entrada do usuário
      ↓
Application Command
      ↓
Music Engine
      ↓
Music Model
      ↓
┌───────────────┬──────────────┐
│               │              │
Renderer       Audio        Persistence
│               │              │
VexFlow       Web Audio     IndexedDB
```

## Consequências positivas

- O mesmo `insertNote()` poderá ser acionado por mouse, touch, teclado, MIDI ou reconhecimento de escrita no futuro.
- O renderer poderá ser substituído sem reescrever as regras musicais.
- O áudio poderá evoluir independentemente da notação visual.
- A partitura poderá ser salva como estrutura musical real, e não como imagem ou SVG.
- O MVP permanece pequeno e testável.
- Recursos de nuvem não entram antes de haver necessidade real.

## Consequências negativas

- Precisaremos criar adapters próprios entre o Music Model e bibliotecas externas.
- Algumas funcionalidades avançadas de notação precisarão ser implementadas no Music Engine.
- O primeiro protótipo terá menos recursos que editores profissionais estabelecidos.

## Regra de evolução

Uma biblioteca externa só deve entrar no núcleo do produto quando resolver um problema concreto sem transferir para ela a responsabilidade pelas regras do domínio.