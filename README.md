# Mission Control AI — Sistema de Alerta por Lógica Digital (Global Solution 2026)

**Curso:** Ciências da Computação — FIAP  
**Turma:** 1CCPX  
**Professor responsável:** Lucas Moreira  
**Repositório:** `gabrielbfurin/CS-Global_Solution-2026`

**Integrantes:**  
- Gabriel Barbosa Furin — RM: 572941  
- Lucas Kiodi Moraca — RM: 571004  
- Renan Fracalossi Mano da Silva — RM: 569610

> **Resumo:** Este projeto implementa um **sistema de alerta por lógica digital** para monitoramento de uma missão espacial experimental. Condições críticas são representadas por entradas binárias (0/1) e combinadas por uma **expressão booleana** que aciona a saída **X**.

---

## Sumário
1. [Introdução](#1-introdução)
2. [ODS 8 — Trabalho decente e crescimento econômico](#2-ods-8--trabalho-decente-e-crescimento-econômico)
3. [Variáveis de entrada (mínimo 5)](#3-variáveis-de-entrada-mínimo-5)
4. [Regras de acionamento do alerta](#4-regras-de-acionamento-do-alerta)
5. [Expressão lógica booleana](#5-expressão-lógica-booleana)
   - [Expressão completa (antes da simplificação)](#51-expressão-completa-antes-da-simplificação)
   - [Expressão simplificada](#52-expressão-simplificada)
   - [Justificativa da simplificação](#53-justificativa-da-simplificação)
6. [Tabela‑verdade completa (32 combinações)](#6-tabela-verdade-completa-32-combinações)
7. [Circuito lógico digital (Tinkercad + CIs 74HC)](#7-circuito-lógico-digital-tinkercad--cis-74hc)
   - [Componentes utilizados](#71-componentes-utilizados)
   - [Saída X e LED indicador](#72-saída-x-e-led-indicador)
   - [Descrição do funcionamento](#73-descrição-do-funcionamento)
   - [Diagrama textual de ligações (alto nível)](#74-diagrama-textual-de-ligações-alto-nível)
   - [Simulação no Tinkercad](#75-simulação-no-tinkercad)
8. [Como testar (casos principais)](#8-como-testar-casos-principais)
9. [Conclusão](#9-conclusão)

---

## 1. Introdução
Este projeto implementa um **Sistema de Alerta por Lógica Digital** para controle e monitoramento básico de uma **missão espacial experimental**, conforme o desafio da Global Solution 2026.

As condições críticas da missão são modeladas por **variáveis digitais (0/1)** e combinadas por portas lógicas (AND, OR, NOT) para acionar o **alerta principal**.

- **X = 0:** condição normal (alerta principal desligado)
- **X = 1:** condição crítica detectada (alerta principal ligado)

---

## 2. ODS 8 — Trabalho decente e crescimento econômico
A proposta se relaciona com a **ODS 8** ao demonstrar uma solução de monitoramento e tomada de decisão que:

- aumenta a **segurança** e a **confiabilidade** operacional (redução de falhas e retrabalho);
- reduz o tempo de diagnóstico/resposta (maior **eficiência** e produtividade);
- fortalece competências técnicas (lógica digital e decisão baseada em regras), contribuindo para **formação profissional** e trabalho qualificado.

---

## 3. Variáveis de entrada (mínimo 5)
Cada variável é binária, onde:

- **0** = condição normal
- **1** = condição de risco, falha ou alerta

### Entradas
- **A:** Falha de comunicação com a nave
- **B:** Temperatura interna crítica
- **C:** Baixo nível de energia
- **D:** Falha em módulo operacional essencial
- **E:** Alerta gerado por sistema inteligente (IA) de monitoramento

### Saída
- **X:** Alerta principal do sistema

---

## 4. Regras de acionamento do alerta
O alerta principal **X = 1** é acionado quando ocorrer **pelo menos uma** das situações abaixo:

1. **Falha de comunicação + energia baixa:** se **A = 1** e **C = 1**, então **X = 1**.
2. **Temperatura crítica + falha de módulo:** se **B = 1** e **D = 1**, então **X = 1**.
3. **Alerta da IA com comunicação OK:** se **E = 1** e **A = 0**, então **X = 1**.
4. **Falha em módulo essencial:** se **D = 1**, então **X = 1**.

> Observação técnica: a regra (3) usa **NOT** (negação) e representa uma decisão de projeto: o alerta da IA só é considerado confiável quando **não existe falha de comunicação**.

---

## 5. Expressão lógica booleana
Convenções adotadas:

- **AND** = `·`
- **OR** = `+`
- **NOT** = `¬`

### 5.1 Expressão completa (antes da simplificação)
A partir das regras:

**X = (A · C) + (B · D) + (E · ¬A) + D**

### 5.2 Expressão simplificada
**X = D + (A · C) + (E · ¬A)**

### 5.3 Justificativa da simplificação
A simplificação ocorre por **absorção**:

- **D + (B · D) = D**

Ou seja: se **D = 1** já aciona o alerta, o termo **(B · D)** não altera a saída e pode ser removido.

---

## 6. Tabela‑verdade completa (32 combinações)
A tabela abaixo considera as entradas **A, B, C, D, E** e a saída **X**, calculada pela expressão simplificada:

**X = D + (A · C) + (E · ¬A)**

Ordem binária utilizada: **A** como bit mais significativo e **E** como menos significativo (00000 → 11111).

> Dica de leitura: quando **D = 1**, a saída **X** é 1 independentemente das outras entradas.

| A | B | C | D | E | X |
|---:|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 0 | 0 | 1 | 1 |
| 0 | 0 | 0 | 1 | 0 | 1 |
| 0 | 0 | 0 | 1 | 1 | 1 |
| 0 | 0 | 1 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 | 1 | 1 |
| 0 | 0 | 1 | 1 | 0 | 1 |
| 0 | 0 | 1 | 1 | 1 | 1 |
| 0 | 1 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 1 | 0 | 1 |
| 0 | 1 | 0 | 1 | 1 | 1 |
| 0 | 1 | 1 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 | 1 | 1 |
| 0 | 1 | 1 | 1 | 0 | 1 |
| 0 | 1 | 1 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 0 | 1 | 0 |
| 1 | 0 | 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 1 | 1 |
| 1 | 0 | 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 1 | 1 | 1 | 1 |
| 1 | 1 | 0 | 0 | 0 | 0 |
| 1 | 1 | 0 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 1 | 1 | 1 |
| 1 | 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 | 1 |

---

## 7. Circuito lógico digital (Tinkercad + CIs 74HC)
O circuito foi desenvolvido em simulador (Tinkercad) utilizando **circuitos integrados (CIs)** de portas lógicas e um **LED** para indicar o alerta principal.

### 7.1 Componentes utilizados
- 1× **74HC04** (NOT)
- 1× **74HC08** (AND)
- 1× **74HC32** (OR)
- Chaves (A, B, C, D, E) para simular sensores/entradas digitais
- Resistores (recomendado: **pull‑down** nas entradas para estabilizar nível lógico)
- 1× LED + 1× resistor (ex.: **220 Ω** ou **330 Ω**)
- Arduino utilizado como fonte de alimentação (**5 V** e **GND**)

### 7.2 Saída X e LED indicador
O **LED** representa fisicamente a **saída lógica X** do sistema:

- Quando **X = 1**, o LED **acende** (alerta principal acionado).
- Quando **X = 0**, o LED permanece **apagado** (condição normal).

### 7.3 Descrição do funcionamento
O circuito implementa a expressão simplificada:

**X = D + (A · C) + (E · ¬A)**

Interpretação operacional:
- Se **D = 1**, o alerta acende (falha crítica em módulo essencial).
- Se **A = 1** e **C = 1**, o alerta acende (falha de comunicação + energia baixa).
- Se **E = 1** e **A = 0**, o alerta acende (IA detecta risco com comunicação íntegra).

### 7.4 Diagrama textual de ligações (alto nível)
1. **Alimentação:** ligar VCC dos CIs em **5 V** e GND em **terra (GND)**.
2. **Inversão de A:** usar o **74HC04** para gerar **¬A** a partir de **A**.
3. **Termo (A · C):** usar uma AND do **74HC08** com entradas **A** e **C**.
4. **Termo (E · ¬A):** usar outra AND do **74HC08** com entradas **E** e **¬A**.
5. **OR intermediário:** usar uma OR do **74HC32** para somar **(A · C)** com **(E · ¬A)**.
6. **OR final:** usar outra OR do **74HC32** para somar o resultado anterior com **D**, gerando **X**.
7. **Saída:** ligar **X** ao LED (com resistor) para indicar alerta quando **X = 1**.

> Nota: a variável **B** é considerada no sistema (e aparece na tabela‑verdade completa), porém **não é necessária no circuito** após a simplificação, reduzindo a complexidade de hardware.

### 7.5 Simulação no Tinkercad
**Imagem do circuito:**

<p align="center">
  <img src="https://github.com/user-attachments/assets/67b329a6-9d95-453d-bf8f-4288960a0723" width="900"/>
</p>

**Link da simulação no Tinkercad:**

- [Visualizar simulação no Tinkercad](https://www.tinkercad.com/things/fi1c2fXpnub-global-soluction-cs?sharecode=oegU1HcqJC2j9gUqpoPA9vDDvO43PAzV5fNIrbwan9Y)

---

## 8. Como testar (casos principais)
Considere **D = 0** quando não estiver citado.

1. **Tudo normal:** A=0, B=0, C=0, D=0, E=0 → **X=0** (LED apagado)
2. **Falha de módulo:** D=1 → **X=1** (LED aceso)
3. **Falha de comunicação + energia baixa:** A=1 e C=1 → **X=1** (LED aceso)
4. **IA detecta risco com comunicação OK:** E=1 e A=0 → **X=1** (LED aceso)
5. **IA com falha de comunicação (bloqueio):** E=1 e A=1 e C=0 → **X=0** (LED apagado)

---

## 9. Conclusão
O sistema desenvolvido atende aos requisitos do desafio ao:

- definir 5 variáveis de entrada binárias e seus significados;
- propor regras de decisão e representar o alerta por **X**;
- construir uma expressão booleana com **AND**, **OR** e **NOT**;
- apresentar expressão completa e expressão simplificada (com justificativa);
- construir a tabela‑verdade completa (32 combinações);
- implementar o circuito lógico com CIs **74HC** e LED indicador;
- contextualizar a aplicação dentro da **ODS 8**, destacando eficiência e formação técnica.

O projeto demonstra, na prática, a aplicação de lógica digital no desenvolvimento de sistemas de monitoramento e tomada de decisão para cenários críticos.
