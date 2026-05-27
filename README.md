# Mission Control AI — Sistema de Alerta por Lógica Digital (Global Solution 2026)

**Curso:** Ciências da Computação — FIAP  
**Turma:** 1CCPX  
**Professor responsável:** Lucas Moreira  
**Repositório:** `gabrielbfurin/CS-Global_Soluction-2026`

## Sumário
- [1. Introdução](#1-introdução)
- [2. ODS 8 — Trabalho decente e crescimento econômico](#2-ods-8--trabalho-decente-e-crescimento-econômico)
- [3. Variáveis de entrada (mínimo 5)](#3-variáveis-de-entrada-mínimo-5)
- [4. Regras de acionamento do alerta](#4-regras-de-acionamento-do-alerta)
- [5. Expressão lógica booleana](#5-expressão-lógica-booleana)
  - [5.1 Expressão completa (antes da simplificação)](#51-expressão-completa-antes-da-simplificação)
  - [5.2 Expressão simplificada](#52-expressão-simplificada)
  - [5.3 Justificativa da simplificação](#53-justificativa-da-simplificação)
- [6. Tabela-verdade completa (32 combinações)](#6-tabela-verdade-completa-32-combinações)
- [7. Circuito lógico digital (Tinkercad + CIs 74HC)](#7-circuito-lógico-digital-tinkercad--cis-74hc)
  - [7.1 Componentes utilizados](#71-componentes-utilizados)
  - [7.2 Descrição do funcionamento](#72-descrição-do-funcionamento)
  - [7.3 Diagrama textual de ligações (alto nível)](#73-diagrama-textual-de-ligações-alto-nível)
  - [7.4 Evidência de simulação](#74-evidência-de-simulação)
- [8. Como testar (casos principais)](#8-como-testar-casos-principais)
- [9. Conclusão](#9-conclusão)

---

## 1. Introdução
Este projeto implementa um **Sistema de Alerta por Lógica Digital** para controle e monitoramento básico de uma **missão espacial experimental**, seguindo o desafio proposto na Global Solution 2026.

A ideia é representar condições críticas da missão por meio de **variáveis digitais (0/1)** e, a partir delas, acionar um **alerta principal** quando houver falhas, riscos operacionais ou condições anormais.

A saída do sistema é a variável **X**, onde:
- **X = 0**: missão em condição normal (sem alerta principal)
- **X = 1**: alerta principal acionado

---

## 2. ODS 8 — Trabalho decente e crescimento econômico
Este sistema se relaciona com a **ODS 8** ao propor um mecanismo de monitoramento e tomada de decisão que:
- melhora a **segurança operacional** e a **confiabilidade** (menos falhas e retrabalho);
- reduz tempo de diagnóstico e resposta (maior **eficiência** e produtividade);
- incentiva a formação de competências técnicas (lógica digital, eletrônica e decisão baseada em regras), contribuindo para **capacitação profissional** e trabalho qualificado.

---

## 3. Variáveis de entrada (mínimo 5)
As entradas foram definidas como variáveis binárias (0/1), onde:
- **0** = condição normal
- **1** = condição de risco / falha / alerta

### Entradas
- **A**: Falha de comunicação com a nave
- **B**: Temperatura interna crítica
- **C**: Baixo nível de energia
- **D**: Falha em módulo operacional essencial
- **E**: Alerta gerado por sistema inteligente (IA) de monitoramento

### Saída
- **X**: Alerta principal do sistema

---

## 4. Regras de acionamento do alerta
O alerta principal **X = 1** deve ser acionado quando ocorrer pelo menos uma das situações abaixo:

1. **Falha de comunicação e energia baixa:** se **A = 1** e **C = 1**, então **X = 1**.
2. **Temperatura crítica e falha de módulo:** se **B = 1** e **D = 1**, então **X = 1**.
3. **Alerta da IA com comunicação OK:** se **E = 1** e **A = 0**, então **X = 1**.
4. **Falha em módulo essencial:** se **D = 1**, então **X = 1**.

Observação importante: a regra (3) utiliza **NOT** (negação) e representa uma decisão de projeto: o alerta da IA só é considerado confiável quando **não existe falha de comunicação**.

---

## 5. Expressão lógica booleana
Convenções:
- AND = **·**
- OR = **+**
- NOT = **¬**

### 5.1 Expressão completa (antes da simplificação)
A partir das regras:

\[
X = (A\cdot C) + (B\cdot D) + (E\cdot \lnot A) + D
\]

### 5.2 Expressão simplificada
\[
X = D + (A\cdot C) + (E\cdot \lnot A)
\]

### 5.3 Justificativa da simplificação
A simplificação acontece por **absorção**:

- \(D + (B\cdot D) = D\)

Ou seja, se **D = 1** já aciona o alerta, então o termo **(B·D)** não altera o resultado e pode ser removido.

---

## 6. Tabela-verdade completa (32 combinações)
A tabela abaixo considera as entradas **A, B, C, D, E** e a saída **X**, calculada pela expressão simplificada:

\[
X = D + (A\cdot C) + (E\cdot \lnot A)
\]

Ordem binária utilizada: **A** como bit mais significativo e **E** como menos significativo (00000 → 11111).

```text
A B C D E | X
0 0 0 0 0 | 0
0 0 0 0 1 | 1
0 0 0 1 0 | 1
0 0 0 1 1 | 1
0 0 1 0 0 | 0
0 0 1 0 1 | 1
0 0 1 1 0 | 1
0 0 1 1 1 | 1
0 1 0 0 0 | 0
0 1 0 0 1 | 1
0 1 0 1 0 | 1
0 1 0 1 1 | 1
0 1 1 0 0 | 0
0 1 1 0 1 | 1
0 1 1 1 0 | 1
0 1 1 1 1 | 1
1 0 0 0 0 | 0
1 0 0 0 1 | 0
1 0 0 1 0 | 1
1 0 0 1 1 | 1
1 0 1 0 0 | 1
1 0 1 0 1 | 1
1 0 1 1 0 | 1
1 0 1 1 1 | 1
1 1 0 0 0 | 0
1 1 0 0 1 | 0
1 1 0 1 0 | 1
1 1 0 1 1 | 1
1 1 1 0 0 | 1
1 1 1 0 1 | 1
1 1 1 1 0 | 1
1 1 1 1 1 | 1
```

---

## 7. Circuito lógico digital (Tinkercad + CIs 74HC)
O circuito digital foi desenvolvido em simulador (Tinkercad) utilizando **circuitos integrados** de portas lógicas e um **LED** para indicar o alerta principal.

### 7.1 Componentes utilizados
- 1× **74HC04** (NOT)
- 1× **74HC08** (AND)
- 1× **74HC32** (OR)
- Chaves (A, B, C, D, E) para simular sensores/entradas digitais
- Resistores (recomendado: **pull-down** nas entradas para estabilizar nível lógico)
- 1× LED + 1× resistor (ex.: **220Ω** ou **330Ω**)
- Fonte de **5V** e **GND**

### 7.2 Descrição do funcionamento
O circuito implementa a expressão simplificada:

\[
X = D + (A\cdot C) + (E\cdot \lnot A)
\]

Assim:
- Se **D = 1**, o LED do alerta acende (falha crítica em módulo essencial).
- Se **A = 1** e **C = 1**, o alerta acende (falha de comunicação + energia baixa).
- Se **E = 1** e **A = 0**, o alerta acende (IA detecta risco com comunicação íntegra).

### 7.3 Diagrama textual de ligações (alto nível)
1. **Alimentação:** ligar **VCC** dos CIs em **5V** e **GND** em **terra (GND)**.
2. **Inversão de A:** usar o **74HC04** para gerar **¬A** a partir de **A**.
3. **Termo A·C:** usar uma AND do **74HC08** com entradas **A** e **C**.
4. **Termo E·¬A:** usar outra AND do **74HC08** com entradas **E** e **¬A**.
5. **OR intermediário:** usar uma OR do **74HC32** para somar **(A·C)** com **(E·¬A)**.
6. **OR final:** usar outra OR do **74HC32** para somar o resultado anterior com **D**, gerando **X**.
7. **Saída:** ligar **X** ao **LED** (com resistor) para indicar alerta quando **X=1**.

> Observação: a variável **B** é considerada na definição do sistema e na tabela-verdade completa, mas não é necessária no circuito após a simplificação (reduzindo hardware e complexidade).

### 7.4 Evidência de simulação
- <img width="1919" height="912" alt="Captura de tela 2026-05-27 151921" src="https://github.com/user-attachments/assets/83705aed-ae38-414d-9339-cefc0f4a363a" />

- **(https://www.tinkercad.com/things/fi1c2fXpnub-global-soluction-cs?sharecode=oegU1HcqJC2j9gUqpoPA9vDDvO43PAzV5fNIrbwan9Y)**

---

## 8. Como testar (casos principais)
Considere **D=0** quando não estiver citado.

1. **Tudo normal:** A=0, B=0, C=0, D=0, E=0 → X=0 (LED apagado)
2. **Falha de módulo:** D=1 → X=1 (LED aceso)
3. **Falha de comunicação + energia baixa:** A=1 e C=1 → X=1 (LED aceso)
4. **IA detecta risco com comunicação OK:** E=1 e A=0 → X=1 (LED aceso)
5. **IA com falha de comunicação (bloqueio):** E=1 e A=1 e C=0 → X=0 (LED apagado)

---

## 9. Conclusão
O sistema desenvolvido cumpre os requisitos do desafio ao:
- definir 5 variáveis de entrada binárias;
- propor regras de decisão;
- construir uma expressão booleana com **AND, OR e NOT**;
- apresentar a expressão completa e a versão simplificada;
- apresentar a **tabela-verdade completa (32 linhas)**;
- implementar o circuito lógico com **CIs 74HC** e LED indicador;
- conectar o projeto à **ODS 8** por eficiência, confiabilidade e desenvolvimento de competências.
