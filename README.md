# 📊 Previsão de Consumo de Energia com Janela Deslizante e Detecção de Concept Drift

Este repositório contém o código desenvolvido no âmbito do meu **mestrado profissional em Computação Aplicada**, com foco em Ciência de Dados e previsão de consumo de energia elétrica.  
O projeto implementa um sistema de previsão em fluxo contínuo (*streaming*) utilizando:

- **Árvore de Decisão (Decision Tree Regressor)**  
- **Janela deslizante (lag) de 168 horas**  
- **Detecção de concept drift com ADWIN**  
- **Cenários de retreinamento automático**  
- **Simulação de chegada de dados em streaming**  
- **Treinamento inicial com o primeiro ano de dados**  
- **Avaliação mensal (RMSE)**  

O dataset utilizado é o arquivo `eletricidade.csv`.

---

## ⚙️ Funcionalidades Implementadas

### 🔹 1. Pré-processamento
- Leitura do arquivo `eletricidade.csv`.
- (Opcional) Leitura do arquivo `linearxx.csv` para implementar variações artificiais 
- Criação de timestamp data/hora.
- Criação do dataset com:
  - Lag de **168 horas**
  - Features de **hora**, **dia da semana** e **mês**

---

### 🔹 2. Treinamento Inicial
- O modelo é treinado apenas com os **dados do primeiro ano**.
- O restante dos dados é utilizado para simular streaming.

---

### 🔹 3. Simulação de Streaming
O sistema processa os dados **amostra por amostra**, executando:

- Previsão do próximo valor
- Inserção da nova observação no ADWIN
- Checagem por concept drift
- Retreinamento conforme o cenário escolhido

---


### 🔹 4. Previsão dos próximos 15 dias
O modelo prevê o consumo dos próximos 15 dias fazendo previsões de hora em hora, de modo que o valor previsto entra na previsão seguinte e assim por diante até fechar o ciclo de 15 dias. O consumo total previsto o período é consolidado. 

- Previsão do próximo valor
- Utilização do valor previsto para a próxima previsão até fechar o ciclo de 15 dias.
- Consolidação das previsões

---

### 🔹 5. Cenários Implementados

#### **Cenário 1 — Detecção de Concept Drift (ADWIN)**
Quando ocorre drift:
- O modelo é retreinado usando apenas o **último ano de dados**.

#### **Cenário 2 — Retreinamento Mensal**
Independente da ocorrência de drift:
- No início de cada mês o modelo é retreinado com 1 ano de dados recentes.

#### **Cenário 3 — Treinamento utilizando Hoeffding Adaptive Tree
O modelo aprende sozinho sem a neessidade de detectar deriva

#### **Cenário 4 — Previsão naive dos últimos 15 dias
Prevê os próximos 15 dias com o histórico dos 15 dias anteriores
- Serve como análise comparativa.

---

### 🔹 6. Avaliação
- O sistema calcula o **RMSE mensal**.
- Um relatório final consolida todos os cenários.
- Plotagem de gráficos
