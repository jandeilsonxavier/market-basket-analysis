# **Projeto de Análise Exploratória de Dados e Sistema de Recomendacão com Apriori**

## Índice
1. [Introdução](#-descrição)
2. [Objetivo](#-dataset)
3. [Dataset](#-dataset)
4. [Ferramentas Utilizadas](#-ferramentas-utilizadas)
5. [Metodologia](#-metodologia)
6. [Resultados](#resultados)
7. [Próximos Passos](#-próximos-passos)
8. [Como Usar](#-como-executar)

## 📋 Introdução

🛒**Market Basket Analysis** é uma técnica técnica de análise de dados que identifica padrões de compra de clientes. Essa análise busca combinações de produtos que frequentemente aparecem juntas em transações, permitindo que os varejistas compreendam os relacionamentos entre os itens adquiridos por seus clientes. Essa abordagem é viabilizada por meio de regras de associação.

As **regras de associação** têm como objetivo encontrar elementos que implicam na presença de outros em uma mesma transação. Em outras palavras, elas identificam padrões frequentes e relacionamentos entre os conjuntos de dados. Essa técnica é aplicada tanto em mineração de dados quanto em aprendizado de máquina.

Em termos práticos, as regras de associação ajudam a descobrir relações entre itens em um conjunto de dados. Por exemplo, elas podem responder a perguntas como: "Se um cliente compra o produto A, qual é a probabilidade de ele também adquirir o produto B?"

**Métricas Importantes:**  
1. **Suporte (Support)**  
    Representa a frequência relativa com que dois produtos aparecem juntos nas transações totais. É uma proporção do total de vendas. É útil para identificar pares de produtos com alta popularidade conjunta.  

    $\text{Suporte} = \frac{\text{Número de transações com A e B}}{\text{Número total de transações}}$  
   
    Um suporte baixo pode indicar que a combinação de produtos não é muito comum, mesmo que tenha alta confiança ou lift. Quando você deseja promover produtos que já têm um volume significativo de vendas juntos.

2. **Confiança (Confidence):**  
   Representa a probabilidade de um produto ser comprado, dado que o outro foi comprado. É uma métrica condicional, útil para medir a força da relação entre dois produtos. 

   $\text{Confiança} = \frac{\text{Número de transações com A e B}}{\text{Número de transações com  A}}$

    Alta confiança indica que os clientes que compram o produto A têm grande probabilidade de comprar o produto B. Ideal quando o foco é em relações fortes e previsíveis para sugerir produtos altamente correlacionados.

   **Exemplo:** Se a confiança de "Se comprar A, então comprar B" é 0.8, significa que 80% dos clientes que compraram A também compraram B.

3. **Lift:**  
   Compara a probabilidade de os produtos serem comprados juntos com a probabilidade de serem comprados separadamente. Ela mede a força da relação entre A e B comparada ao que seria esperado por acaso.

   $\text{Lift} = \frac{\text{Confiança de A} \to B}{\text{Suporte de B}}$ 

   **Lift > 1:** Os itens têm uma associação positiva (mais provável de serem comprados juntos).  
   **Lift = 1:** Não há associação.  
   **Lift < 1:** Os itens têm uma associação negativa (menos provável de serem comprados juntos).

    Ideal quando o objetivo é descobrir associações surpreendentes ou não óbvias para promover combinações de produtos que têm potencial de venda conjunto, mesmo que não sejam os mais populares.

    **Exemplo:** Se o lift de "A + B" é 2.5, significa que os dois produtos são comprados juntos 2,5 vezes mais frequentemente do que o esperado pelo acaso.

**Apriori:**  
O **Apriori** é um dos algoritmos mais usados para encontrar conjuntos de itens frequentes e gerar regras de associação. Ele segue o princípio de que:
Se um conjunto de itens é frequente, todos os seus subconjuntos também são frequentes.

**Etapas do Apriori:**
1. **Gerar Conjuntos de Itens Frequentes:**
   - Ele começa analisando os itens individuais (ex.: "Camiseta Azul") e verifica se atendem a um suporte mínimo.
   - Depois, combina os itens em pares (ex.: {"Camiseta Azul", "Calça Jeans"}) e analisa novamente.

2. **Prune (Poda):**
   - Remove combinações que não atendem ao suporte mínimo, economizando tempo e recursos computacionais.

3. **Gerar Regras de Associação:**
   - Para cada conjunto de itens frequentes, o algoritmo calcula as métricas de confiança e lift para gerar regras como:  
     {"Camiseta Azul"} → {"Calça Jeans"}  
  
**Exemplo Prático:**  
| Transação | Itens Comprados                 |
|-----------|---------------------------------|
| 1         | {Camiseta Azul, Calça Jeans}    |
| 2         | {Tênis Esportivo, Calça Jeans}  |
| 3         | {Camiseta Azul, Tênis Esportivo}|
| 4         | {Camiseta Azul, Calça Jeans}    |

**Suporte:**
   - "Camiseta Azul" aparece em 3 transações (75% de suporte).

**Confiança:**
   - Dado que "Camiseta Azul" foi comprada, em 2 de 3 transações também foi comprada "Calça Jeans" (66.7% de confiança).

**Lift:**
   - Se "Calça Jeans" aparece em 50% das transações, o lift seria:  

     $\text{Lift} = \frac{0.667}{0.5} = 1.33$  

     Isso indica uma associação positiva.

### 🎯 Objetivo
Este projeto tem como objetivo realizar uma **análise exploratória de dados (EDA)** e implementar um **sistema de recomendação** utilizando o **Algoritmo Apriori** para identificar padrões de compras em um conjunto de dados de comportamento do consumidor em e-commerce.

### 📁 Dataset
O dataset utilizado é o ECommerce_consumer behaviour, disponível no Kaggle ([link](https://www.kaggle.com/datasets/hunter0007/ecommerce-dataset-for-predictive-marketing-2023/data)). Ele contém 2.019.501 registros e 12 colunas, descritas abaixo:

- `order_id` - Identificador único do pedido.
- `user_id` - Identificador único do usuário.
- `order_number` - Número do pedido.
- `order_dow` - Dia da semana em que o pedido foi realizado.
- `order_hour_of_day` - Hora do dia em que o pedido foi realizado.
- `days_since_prior_order` - Tempo (em dias) desde o último pedido.
- `product_id` - Identificador do produto.
- `add_to_cart_order` - Pedido em que o produto foi adicionado ao carrinho.
- `reordered` - Indica se o produto foi recomprado.
- `department_id` - Identificador único do departamento.
- `department` - Nome do departamento.
- `product_name` - Nome do produto.

## 📊 Análise Exploratória de Dados (EDA)
A análise exploratória foi realizada para entender o comportamento de compra dos usuários. Todos os gráficos gerados estão presentes no arquivo notebook (.ipynb). As principais análises incluem:

- Distribuição de Pedidos por Dia da Semana
- Distribuição de Pedidos por Hora do Dia
- Mapa de Calor dos Pedidos por Dia e Hora
- Top 20 Produtos Mais Vendidos
- Distribuição de Produtos Recomprados
- Top 20 Produtos com Maior Número de Recompras
- Distribuição do Tempo Entre Pedidos
- Top 20 Usuários Mais Frequentes
- Quantidade de Produtos por Departamento
- Quantidade de Pedidos por Departamento

## 🛒 Sistema de Recomendacão com Apriori
### Estruturação dos Dados
Para aplicar o Apriori, os dados foram transformados em uma **matriz de transações**, onde:
- Cada linha representa um **pedido (`order_id`)**.
- Cada coluna representa um **produto (`product_name`)**.
- O valor é `1` se o produto foi comprado e `0` caso contrário.

### Implementação do Algoritmo Apriori
O Algoritmo Apriori foi aplicado com os seguintes parâmetros:
- `min_support = 0.01` (1% das transações contém esse conjunto de itens)
- `metric = "lift"`
- `min_threshold = 1.0`

As **regras de associação** foram geradas e ordenadas pelo **Lift**, indicando os produtos mais frequentemente comprados juntos.

## 📋 Conclusão
O projeto forneceu insights valiosos sobre o comportamento do consumidor e permitiu a criação de um **sistema de recomendação baseado em regras de associação**. As principais descobertas foram:
- Determinamos os **horários de pico** e **dias mais movimentados** para pedidos.
- Identificamos **padrões de recompra** entre clientes frequentes.
- Implementamos um modelo para **recomendar produtos frequentemente comprados juntos**.

Esse sistema pode ser utilizado para otimizar campanhas de marketing e melhorar a experiência do cliente em plataformas de e-commerce.

### **Conclusão para a Regra de Associação Obtida**  

A regra de associação número 191 **(fresh herbs) → (fresh fruits, fresh vegetables)** indica que clientes que compram **ervas frescas** têm uma forte tendência a comprar também **frutas frescas e vegetais frescos**.  

 **Interpretação dos Indicadores:**  
- **Suporte = 6,18%** → A combinação de ervas frescas com frutas e vegetais aparece em **6,18% de todas as transações** do dataset. Isso sugere que essa associação ocorre com frequência relevante.  
- **Confiança = 66,46%** → Quando um cliente compra **ervas frescas**, há **66,46% de chance** de que ele também compre frutas e vegetais frescos. Esse valor indica uma relação forte entre esses produtos.  
- **Lift = 2,09** → Esse valor mostra que a compra de ervas frescas **aumenta em 2,09 vezes a probabilidade** de o cliente comprar frutas e vegetais, comparado a compras aleatórias. Como o lift é maior que 1, isso confirma que há uma **associação positiva e significativa** entre esses produtos.   
---
**Aplicação Prática:**  
Esse insight pode ser utilizado para **estratégias de marketing e vendas**, como:  
- Criar promoções conjuntas para esses produtos.  
- Recomendar frutas e vegetais frescos para clientes que compram ervas frescas.  
- Posicionar esses produtos próximos no supermercado ou no site para incentivar compras combinadas.  

Esse tipo de análise ajuda a **otimizar vendas e melhorar a experiência do cliente**, oferecendo recomendações mais personalizadas. 

## 🛠️ Ferramentas Utilizadas
- **Linguagem:** `Python`
- **Bibliotecas:** `pandas`, `numpy`, `seaborn`, `matplotlib`, `mlxtend`
- **Plataforma:** `Google Colab`

---

## 🚀 Próximos Passos
- **Automatização do Fluxo de Dados:** Utilizar APIs que integrem o sistema diretamente com a loja virtual ou o ERP.
- **Monitoramento em Tempo Real:** Habilitar a atualização em tempo real dos dados para oferecer insights instantâneos sobre tendências de compra e desempenho de produtos.
- **Testes A/B de Sugestões:** Realizar experimentos controlados para avaliar o impacto das recomendações sobre as taxas de conversão e o ticket médio.

## 💻 Como Executar

1. **Clone este repositório**
```bash
git clone https://github.com/jandeilsonxavier/analise-regras-associacao.git
cd restaurants-service-repository
```
2. **Crie o ambiente virtual**
```bash
python -m venv venv
```
3. **Ative o ambiente virtual**
```bash
No Windows:
venv\Scripts\activate

No Mac/Linux:
source venv/bin/activate
```
4. **Instale as dependências**
```bash
pip install -r requirements.txt
```
5. **Execute o script principal**
```bash
streamlit run app.py
```