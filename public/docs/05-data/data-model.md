# Modelo de Dados

## Objetivo
Definir a representação persistente mínima do documento musical.

## Entidade raiz

```text
Score
├── metadata
├── parts[]
└── settings
```

## Estrutura inicial

```json
{
  "schemaVersion": 1,
  "id": "score-01",
  "metadata": {
    "title": "",
    "composer": ""
  },
  "parts": [
    {
      "id": "part-01",
      "name": "Piano",
      "staves": [
        {
          "id": "staff-01",
          "clef": { "sign": "G", "line": 2, "octaveChange": 0 },
          "measures": []
        }
      ]
    }
  ]
}
```

## Compasso

```json
{
  "number": 1,
  "timeSignature": {
    "numerator": 4,
    "denominator": 4,
    "grouping": [2, 2]
  },
  "voices": []
}
```

## Evento

```json
{
  "id": "event-01",
  "type": "note",
  "position": 0,
  "duration": {
    "base": "quarter",
    "dots": 0,
    "tuplet": null
  },
  "pitch": {
    "step": "C",
    "alter": 0,
    "octave": 4
  }
}
```

## Identificadores
IDs devem ser estáveis durante a vida do documento para permitir:
- seleção;
- undo/redo;
- relações entre eventos;
- colaboração futura;
- referências de tie/slur.

## Versionamento
Todo documento persistido deve possuir `schemaVersion`.

Mudanças incompatíveis deverão ter migradores explícitos.

```text
schema v1 → migration → schema v2
```

## Separação de projeções
O JSON persistido representa o modelo musical. SVG, PNG, PDF e MIDI são derivados.

## Persistência local
A primeira versão pode armazenar o documento localmente. O formato deve ser independente do banco para permitir futura persistência em servidor.

## Integridade
O documento persistido deve passar por validação estrutural e musical antes de ser considerado válido.