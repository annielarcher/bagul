# Princípios de API

## MVP

O primeiro protótipo não precisa de uma API de negócio nem de banco remoto. A partitura pode ser criada, editada e salva localmente.

Isso reduz infraestrutura e mantém o foco na experiência principal.

## Futuro

Quando houver contas e nuvem, a API deverá tratar a partitura como documento estruturado versionado.

Conceitualmente:

```text
Client
  ↓
Application API
  ↓
Music Document Service
  ↓
PostgreSQL
```

## Regras

- a API não deve duplicar regras musicais do Music Engine;
- validações estruturais podem ocorrer no servidor;
- o servidor nunca deve confiar apenas na validação feita pelo cliente;
- documentos devem possuir `schemaVersion`;
- alterações importantes devem ser rastreáveis;
- autorização deve ocorrer no servidor;
- colaboração futura exigirá estratégia própria de versionamento/conflito.

## Possíveis recursos futuros

```text
POST   /api/scores
GET    /api/scores/:id
PUT    /api/scores/:id
DELETE /api/scores/:id
POST   /api/scores/:id/versions
POST   /api/scores/:id/share
```

Esses endpoints são apenas uma direção arquitetural futura e não fazem parte do MVP.