# Teste A/B de Taxa de Conversão com Python

## Visão geral

Este projeto apresenta um **estudo simulado de experimentação A/B** para comparar a taxa de conversão de duas variantes (A e B). O notebook percorre o planejamento amostral, a atribuição aleatória de grupos, a simulação de conversões, a aplicação de um teste estatístico e a interpretação dos resultados para apoiar decisões de produto e negócio.

> **Natureza dos dados:** as conversões são geradas artificialmente em Python. Os resultados não correspondem a uma campanha real nem demonstram impacto financeiro observado.

## Objetivo

Avaliar se existe diferença estatisticamente significativa entre as taxas de conversão de dois grupos, com **nível de significância de 5%**, e discutir critérios para uma implementação gradual da variante com melhor desempenho.

## Tecnologias

- **Python** — implementação da simulação e dos cálculos;
- **NumPy** — geração aleatória e simulação de conversões;
- **Pandas** — organização dos dados e consolidação das métricas;
- **Statsmodels** — cálculo do tamanho de amostra e teste z para duas proporções;
- **Jupyter Notebook** — documentação e execução da análise.

## Metodologia

### 1. Planejamento amostral

O notebook calcula o tamanho mínimo de amostra para comparar duas proporções, considerando:

| Parâmetro | Valor |
|---|---:|
| Taxa de referência (A) | 12% |
| Taxa-alvo (B) | 13% |
| Efeito mínimo detectável (MDE) | 1 ponto percentual |
| Significância (α) | 5% |
| Poder estatístico | 80% |
| Tamanho estimado | 17.163,03 por grupo |

Arredondando para cima, seriam necessários **17.164 usuários por grupo** no cenário de planejamento.

### 2. Simulação e randomização

Com semente aleatória definida (`np.random.seed(42)`), o estudo gera **36.000 observações** e distribui os rótulos A e B aleatoriamente. As probabilidades de conversão usadas nessa etapa são **10% para A e 12% para B**, distintas do cenário usado no cálculo amostral.

A atribuição por sorteio não força uma divisão exatamente igual entre os grupos. O notebook obtém **17.928 observações em A** e **18.072 em B**.

### 3. Medição das conversões

O indicador principal é a taxa de conversão, calculada pela razão entre conversões e observações de cada variante.

| Indicador | Grupo A | Grupo B |
|---|---:|---:|
| Observações | 17.928 | 18.072 |
| Conversões | 1.872 | 2.119 |
| Taxa de conversão | 10,44% | 11,73% |

A diferença observada foi de aproximadamente **+1,28 ponto percentual** para a variante B, o equivalente a cerca de **+12,3% de aumento relativo** sobre a taxa de A.

### 4. Teste de hipóteses

Foi utilizado o **teste z bilateral para comparação de duas proporções**, com as hipóteses:

- **H₀:** as taxas de conversão de A e B são iguais;
- **H₁:** as taxas de conversão são diferentes.

**Resultados registrados no notebook:**

- Estatística z: **−3,8784**;
- Valor-p: **0,0001051**;
- Significância adotada: **0,05**.

Como o valor-p é inferior a 0,05, rejeita-se a hipótese de igualdade entre as proporções. **Na simulação analisada**, a variante B apresentou taxa observada maior que A. O teste bilateral sustenta a existência de diferença; a direção favorável a B decorre das taxas observadas.

### 5. Possível implementação

O notebook discute um rollout gradual (**20% → 50% → 100%**) e o monitoramento de métricas secundárias, como NPS e reclamações. Essa etapa é **proposta metodológica**, não uma implantação executada.

## Como executar

1. Tenha Python e Jupyter Notebook instalados.
2. Instale as bibliotecas necessárias:

   ```bash
   pip install numpy pandas statsmodels notebook
   ```

3. Abra o arquivo `Aula 5.ipynb` no Jupyter Notebook ou no VS Code.
4. Execute as células na ordem para reproduzir a simulação e os resultados.

