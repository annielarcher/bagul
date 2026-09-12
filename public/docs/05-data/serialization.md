# Serialização e Versionamento

## Objetivo
Garantir que uma partitura salva hoje continue podendo ser aberta no futuro.

## Princípio
Nunca persistir apenas a aparência da partitura.

Persistir:
- estrutura musical;
- posições temporais;
- durações;
- pitches;
- claves;
- métricas;
- vozes;
- relações musicais;
- metadados necessários.

## Schema version
Todo documento possui:

```json
{ "schemaVersion": 1 }
```

## Compatibilidade
O leitor deve:
1. identificar a versão;
2. validar a estrutura;
3. migrar versões antigas quando suportadas;
4. rejeitar formatos desconhecidos de maneira clara.

## Segurança
Dados importados nunca devem ser considerados confiáveis apenas porque possuem estrutura JSON. O parser deve validar tipos, limites e relações antes de entregá-los ao Music Engine.

## Exportações
A partir do Music Model podem ser produzidos:
- MusicXML;
- MIDI;
- PDF;
- SVG;
- PNG.

Cada exportador é uma projeção independente.