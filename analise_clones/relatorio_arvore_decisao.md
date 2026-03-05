# War Analytics — Relatório da Velha República
## Estudo com Árvore de Decisão: Identificação de Clones Defeituosos

---

> *"A República luta por continuar existindo. Liderado pelos generais Jedi, o exército de clones enfrenta o exército separatista. Alguns soldados têm falhado em meio ao campo de batalha sem que se conheça a causa."*

O Alto Conselho Jedi exige da equipe de **War Analytics** insights capazes de estancar o sangramento e manter a galáxia sob o controle do Senado Galáctico. Pela nossa análise de dados baseada em uma Árvore de Decisão, mapeamos e identificamos os fatores que determinam se um clone será **Apto** ou **Defeituoso**.

---

## 1. Visão Geral dos Dados e Exploração

O relatório baseia-se em um vasto dataset militar contendo **1.048.719 registros** e 9 variáveis principais. Entre as variáveis analisadas constam atributos físicos dos clones como 'Massa', 'Estatura', 'Tamanho do crânio' e os 'Generais Jedi encarregados'. 

### 1.1 Distribuição da Variável Alvo (Status)
Observou-se de imediato que se trata de uma base de dados desbalanceada. Há aproximadamente **1 soldado defeituoso para cada 8 soldados aptos**.
- **Aptos:** ~89.5% dos soldados.
- **Defeituosos:** ~10.5% dos soldados.

![Distribuição da Variável Alvo](graph_1.png)

### 1.2 Análise Bivariada: General Jedi vs Status
A variável mais determinante identificada foi o **General Jedi encarregado**. Clones treinados sob o comando da **Shaak Ti** e **Yoda** exibem uma **taxa de defeito astronômica (aproximadamente 50%)**. Em contrapartida, clones comandados por Aayla Secura, Mace Windu e Obi-Wan Kenobi demonstraram um índice de defeito incrível de **0%**.

![Análise Bivariada - General Jedi](graph_2.png)

### 1.3 Distribuição de Características Físicas
Outras variáveis (Massa, Estatura, Tempo de existência) representam papéis secundários. Elas ditam variações mínimas em batalhões que já apresentaram vulnerabilidade. Abaixo observamos a distribuição dessas características físicas em relação ao Status:

![Características Físicas por Status](graph_3.png)

### 1.4 Correlação e Relação Múltipla (Pairplot)
A matriz de correlação e o Pairplot confirmam que não há forte multicolinearidade entre as variáveis físicas que sobreponha a importância do General Jedi encarregado.

![Matriz de Correlação](graph_4.png)
![Pairplot](graph_5.png)

---

## 2. Abordagem de Machine Learning

Para obter regras claras e de fácil interpretação pelos Generais da República, um modelo de **Árvore de Decisão (Decision Tree)** foi utilizado. Os dados foram divididos em **Treino (70%)** e **Teste (30%)** com estratificação para lidar com o desequilíbrio das classes.

### 2.1 Ajuste de Profundidade da Árvore
Para evitar um "superajuste" (overfitting) às características do treino e para manter as regras de negócio plenamente interpretáveis, foi realizada uma validação do hiperparâmetro de profundidade máxima. A profundidade ideal foi fixada em **5**.

![Análise de Profundidade](graph_6.png)

### 2.2 Performance do Modelo (ROC e Matriz de Confusão)
O modelo apresentou uma capacidade altíssima de separação, conforme demonstrado pela **Curva ROC** próxima à perfeição técnica na identificação da classe minoritária ("Defeituoso") e pela matriz de confusão.

![Curva ROC](graph_7.png)
![Matriz de Confusão](graph_8.png)

---

## 3. Insights Descobertos e Visualização da Árvore

As principais saídas do modelo demonstram claramente onde reside a fraqueza no exército da República. O algoritmo produziu a árvore de decisão abaixo, visualmente interpretável:

![Visualização da Árvore de Decisão](graph_9.png)

### Principais Regras Geradas pelo Sistema:
1. **Regra de Falha Crítica:** SE o General Jedi é Shaak Ti ou Yoda, as chances de o clone ser defeituoso sobem para 50%.
2. **Regra de Aptidão:** SE o General Jedi é Aayla Secura, Mace Windu ou Obi-Wan Kenobi, o clone será apto em 100% dos casos registrados.

---

## 4. Conclusões e Recomendações ao Comando Militar

| Prioridade | Recomendação Estratégica |
| :---: | :--- |
| 🔴 **Crítica** | **Investigar imediatamente** os processos de produção, gestação e treinamento dos contingentes subordinados a **Shaak Ti e Yoda**. |
| 🔴 **Crítica** | Transferir de imediato clones "suspeitos" destes batalhões para testes intensivos em Kamino antes da escalação e envio para as linhas de combate. |
| 🟡 **Alta** | Adotar em toda a República o novo protocolo em formato de "Regras da Árvore de Decisão" como métrica principal de triagem e QA de Clones. |
| 🟢 **Média** | Replicar e estudar práticas táticas e educacionais implementadas nos esquadrões de **Aayla Secura, Mace Windu e Obi-Wan Kenobi**. |

> **"Que a Força esteja com nossos dados."** - *Equipe War Analytics*
