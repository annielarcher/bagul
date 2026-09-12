# Estratégia de Testes

## Objetivo

Garantir que a velocidade da interface não comprometa a correção musical.

A prioridade de testes será o **Music Engine**, porque ele concentra as regras que não podem depender da interface.

## Pirâmide

```text
             E2E
          Playwright
             /\
            /  \
      Integration
        Engine + UI
          /      \
         /        \
       Unit Tests
     Music Engine
```

## Testes unitários

Cobrir principalmente:

- duração em ticks;
- capacidade de compasso;
- inserção de notas;
- inserção de pausas;
- acordes;
- overflow;
- cursor temporal;
- fórmulas simples e compostas;
- agrupamento rítmico;
- pitch e acidentes;
- claves;
- vozes;
- ligaduras;
- articulações;
- undo/redo.

## Exemplos essenciais do MVP

### 4/4

```text
quarter + quarter + quarter + quarter
→ compasso completo
```

### Overflow

```text
quarter + quarter + quarter + quarter + quarter
→ não inserir silenciosamente além da capacidade
```

### 3/4

```text
quarter + quarter + quarter
→ compasso completo
```

### 6/8

```text
6 eighths = capacidade temporal correta
agrupamento ≠ simples lista de seis elementos
```

## Testes de integração

Verificar que uma ação da interface produz a operação correta no Music Engine e que o renderer reflete o Music Model atualizado.

O teste não deve validar detalhes internos do VexFlow quando isso não for necessário; deve validar o comportamento observável do editor.

## E2E

Fluxo principal:

```text
abrir editor
→ partitura pronta
→ selecionar duração
→ clicar no pentagrama
→ nota aparece
→ cursor avança
→ inserir novas notas
→ reproduzir
→ salvar
→ recarregar
→ partitura permanece correta
```

## Regra de regressão

Toda falha musical corrigida no Engine deve, sempre que possível, gerar um teste automatizado que impeça a regressão.