# Segurança e Deploy

## MVP

O produto será prioritariamente local-first:

- dados musicais salvos no dispositivo;
- nenhuma conta obrigatória;
- nenhum backend necessário para editar uma partitura;
- nenhuma informação musical precisa sair do navegador para o fluxo básico.

## Segurança de aplicação

- validar toda entrada externa;
- não executar conteúdo importado como código;
- tratar arquivos MusicXML como dados não confiáveis;
- evitar inserir conteúdo de partituras diretamente como HTML sem sanitização;
- separar claramente dados musicais de conteúdo de interface;
- limitar recursos consumidos por arquivos/importações excessivamente grandes.

## Privacidade

A arquitetura local-first reduz coleta de dados no MVP.

Se sincronização em nuvem for adicionada posteriormente, a política de dados deverá ser definida antes do lançamento do recurso.

## Deploy

A aplicação poderá ser publicada como frontend web estático no início.

Backend e banco serão introduzidos apenas quando funcionalidades que realmente exigirem persistência remota forem priorizadas.

## Observabilidade futura

Quando houver backend, adicionar:

- logs estruturados;
- monitoramento de erros;
- métricas de disponibilidade;
- rastreamento de falhas de importação/exportação;
- monitoramento de performance.