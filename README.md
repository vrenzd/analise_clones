# War Analytics — Relatório da Velha República
## Estudo com Árvore de Decisão: Identificação de Clones Defeituosos

---

> *"A República luta por continuar existindo. Liderado pelos generais Jedi, o exército de clones enfrenta o exército separatista. Alguns soldados têm falhado em meio ao campo de batalha sem que se conheça a causa."*

O Alto Conselho Jedi exige da equipe de **War Analytics** insights capazes de estancar o sangramento e manter a galáxia sob o controle do Senado Galáctico. Pela nossa análise de dados baseada em uma Árvore de Decisão, mapeamos e identificamos os fatores que determinam se um clone será **Apto** ou **Defeituoso**.

---

## 📋 Visão Geral do Projeto

Este projeto realiza uma análise de dados para identificação de clones defeituosos utilizando técnicas de Machine Learning (Árvore de Decisão). O dataset contém **1.048.719 registros** de clones com informações sobre seus atributos físicos e o General Jedi responsável por seu treinamento.

### Tecnologias Utilizadas
- **Python** 3.12.10
- **Pandas** - Manipulação e análise de dados
- **NumPy** - Operações numéricas
- **Scikit-learn** - Algoritmo de Árvore de Decisão
- **Matplotlib** - Visualização de gráficos
- **Seaborn** - Visualizações estatísticas avançadas
- **Scipy** - Cálculos estatísticos
- **Pillow** - Processamento de imagens
- **PyArrow** - Trabalho com dados em formato arrow
- **Jinja2** - Renderização de templates

---

## 🚀 Como Instalar e Usar

### Pré-requisitos
- Python 3.12.10 instalado no seu sistema
- pip (gerenciador de pacotes do Python)

### Passo 1: Clonar o Repositório
```bash
git clone https://github.com/vrenzd/analise_clones.git
cd analise_clones
```

### Passo 2: Criar um Ambiente Virtual (Recomendado)
```bash
# No Windows
python -m venv venv
venv\Scripts\activate

# No macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### Passo 3: Instalar as Dependências
```bash
pip install -r analise_clones/requirements.txt
```

### Passo 4: Executar a Análise
```bash
# Dentro do diretório do projeto
python main.py
```

Ou, se o script principal estiver em outro local:
```bash
python analise_clones/seu_script.py
```

---

## 📊 Estrutura do Projeto

```
analise_clones/
├── requirements.txt          # Dependências do projeto
├── main.py                   # Script principal de execução
├── dados/                    # Dataset com os clones
├── modelos/                  # Modelos de ML treinados
└── graficos/                 # Visualizações geradas
```

---

## 1. Visão Geral dos Dados e Exploração

O relatório baseia-se em um vasto dataset militar contendo **1.048.719 registros** e 9 variáveis principais. Entre as variáveis analisadas constam atributos físicos dos clones como 'Massa', 'Estatura', 'Tamanho do crânio' e os 'Generais Jedi encarregados'. 

### 1.1 Distribuição da Variável Alvo (Status)
Observou-se de imediato que se trata de uma base de dados desbalanceada. Há aproximadamente **1 soldado defeituoso para cada 8 soldados aptos**.
- **Aptos:** ~89.5% dos soldados.
- **Defeituosos:** ~10.5% dos soldados.

<img width="700" height="700" alt="graph_1" src="https://github.com/user-attachments/assets/4cce1ca0-b3a8-41e2-bf93-4dd94ea8fb30" />


### 1.2 Análise Bivariada: General Jedi vs Status
A variável mais determinante identificada foi o **General Jedi encarregado**. Clones treinados sob o comando da **Shaak Ti** e **Yoda** exibem uma **taxa de defeito astronômica (aproximadamente 50%)**. Em contrapartida, clones comandados por Aayla Secura, Mace Windu e Obi-Wan Kenobi demonstraram um índice de defeito incrível de **0%**.

<img width="750" height="750" alt="graph_2" src="https://github.com/user-attachments/assets/7d54308d-f7eb-48b7-ae79-fb347b0a42cf" />


### 1.3 Distribuição de Características Físicas
Outras variáveis (Massa, Estatura, Tempo de existência) representam papéis secundários. Elas ditam variações mínimas em batalhões que já apresentaram vulnerabilidade. Abaixo observamos a distribuição dessas características físicas em relação ao Status:

<img width="1784" height="512" alt="graph_3" src="https://github.com/user-attachments/assets/027d20c7-713d-4470-b606-c69d595b47ec" />


### 1.4 Correlação e Relação Múltipla (Pairplot)
A matriz de correlação e o Pairplot confirmam que não há forte multicolinearidade entre as variáveis físicas que sobreponha a importância do General Jedi encarregado.

<img width="500" height="500" alt="graph_4" src="https://github.com/user-attachments/assets/3031deb6-84cc-4547-be28-dabfae24d727" />
<img width="500" height="500" alt="graph_5" src="https://github.com/user-attachments/assets/fba8e6b9-45a0-46ab-88ce-5c3958728dce" />


---

## 2. Abordagem de Machine Learning

Para obter regras claras e de fácil interpretação pelos Generais da República, um modelo de **Árvore de Decisão (Decision Tree)** foi utilizado. Os dados foram divididos em **Treino (70%)** e **Teste (30%)** com estratificação para lidar com o desequilíbrio das classes.

### 2.1 Ajuste de Profundidade da Árvore
Para evitar um "superajuste" (overfitting) às características do treino e para manter as regras de negócio plenamente interpretáveis, foi realizada uma validação do hiperparâmetro de profundidade máxima. A profundidade ideal foi fixada em **5**.

<img width="600" height="600" alt="graph_6" src="https://github.com/user-attachments/assets/adceea9d-09a5-434a-ba8a-237daecbd63b" />

### 2.2 Performance do Modelo (ROC e Matriz de Confusão)
O modelo apresentou uma capacidade altíssima de separação, conforme demonstrado pela **Curva ROC** próxima à perfeição técnica na identificação da classe minoritária ("Defeituoso") e pela matriz de confusão.


<img width="400" height="400" alt="graph_8" src="https://github.com/user-attachments/assets/c276eee8-436e-494a-9d54-e0d04baf999f" />


---

## 3. Insights Descobertos e Visualização da Árvore

As principais saídas do modelo demonstram claramente onde reside a fraqueza no exército da República. O algoritmo produziu a árvore de decisão abaixo, visualmente interpretável:

<img width="900" height="900" alt="graph_9" src="https://github.com/user-attachments/assets/4850bb3b-8368-4af9-bfab-f52572269285" />


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