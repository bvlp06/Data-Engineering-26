# Case Técnico — Engenharia de Dados

<div align="center">
  <img src="https://hermes.dio.me/articles/cover/75ce44d7-3f12-449f-bc8c-fc13f28781a2.jpg" alt="SQL" height="60" />
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Python-logo-notext.svg/1280px-Python-logo-notext.svg.png" alt="Python" height="60" />
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Jupyter_logo.svg/1280px-Jupyter_logo.svg.png" alt="Jupyter" height="60" />
  <img src="https://aster.cloud/wp-content/uploads/2019/10/python-pandas-install-cover.jpg" alt="Pandas" height="60" />
</div>


## 📌 Sobre o Desafio

Este repositório contém a resolução de um case técnico focado em **Engenharia de Dados**. O objetivo principal é solucionar problemas complexos de negócio utilizando **SQL**, demonstrando maturidade analítica e boas práticas de desenvolvimento.

As soluções foram desenhadas sob os seguintes pilares:
* **Correção Técnica e Performance:** Construção de consultas eficientes, considerando cenários de maior volume de dados.
* **Qualidade de Código:** Queries organizadas, legíveis e estruturadas com uso de CTEs (*Common Table Expressions*) quando aplicável.
* **Tratamento de Dados:** Tratamento de valores nulos quando suportado por uma regra de negócio, preservando `NULL` quando não houver informação suficiente para imputação, além da prevenção de erros lógicos, como divisão por zero.
* **Funções de Janela:** Utilização de *Window Functions* para análises temporais, rankings, comparações e controle de granularidade.
* **Documentação:** Explicação das premissas de negócio e das decisões técnicas adotadas em cada desafio.

---

## 📂 Estrutura do Projeto

```text
.
├── data/
│   ├── buyers.csv
│   ├── order_items.csv
│   ├── orders.csv
│   ├── payments.csv
│   ├── products.csv
│   └── sellers.csv
├── notebook/
│   └── modelo_teste.ipynb
├── .gitignore
├── FIEMG-LayoutsValidations-v1.xlsx
├── README.md
└── requirements.txt
```

> ⚠️ **Nota sobre os dados:** Por motivos de conformidade e privacidade, os arquivos CSV originais fornecidos para o teste não foram integrados ao repositório padrão. Para executar o projeto localmente, certifique-se de que eles estejam inseridos na pasta `data/`.

---

## 🛠️ Como Executar o Projeto

Siga os passos abaixo para configurar o ambiente virtual e rodar as análises:

### 1. Clonar o Repositório
```bash
git clone https://github.com/bvlp06/Data-Engineering-26
cd Data-Engineering-26
```

### 2. Criar e Ativar o Ambiente Virtual
* **Linux/macOS:**
  ```bash
  python -m venv .venv
  source .venv/bin/activate
  ```
* **Windows:**
  ```bash
  python -m venv .venv
  .venv\Scripts\activate
  ```

### 3. Instalar as Dependências
```bash
pip install -r requirements.txt
```

### 4. Executar o Notebook
O arquivo principal de resolução está localizado em `notebook/modelo_teste.ipynb`.

O notebook pode ser executado utilizando as seguintes ferramentas:
* **VS Code** (com a extensão *Jupyter* instalada)
* **Jupyter Notebook**
* **JupyterLab**
* **Google Colab**

> 📂 **Lembrete:** Certifique-se de que os arquivos CSV utilizados nas análises estejam devidamente salvos e disponíveis na pasta `data/` antes de iniciar a execução.

---

## 📊 Desafios Resolvidos

|    ID | Desafio                       | Foco Técnico                                                       | Regra de Negócio Aplicada                                                                                                         |
| ----: | ----------------------------- | ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| **1** | **Faturamento Mensal**        | Agregações temporais, filtros e métricas                           | Análise dos últimos **12 meses**, considerando apenas pedidos `completed` ou `delivered`.                                         |
| **2** | **Crescimento de GMV**        | Comparação trimestral e *Window Functions*                         | Comparação do GMV entre trimestres, considerando sellers com no mínimo 50 pedidos por trimestre.                                  |
| **3** | **Descontos Abusivos**        | Agregações, tratamento de dados e proteção contra divisão por zero | Identificação de pedidos em que o desconto representa mais de 40% do valor bruto. Pedidos cancelados são excluídos.               |
| **4** | **Comportamento de Produtos** | *Window Functions*, ranking e análise de granularidade             | Identificação de produtos com mais de 1.000 unidades vendidas que nunca foram o item de maior preço unitário dentro de um pedido. |



---

## 🧠 Organização e Metodologia

Cada desafio possui uma seção dedicada dentro do notebook, seguindo uma estrutura padronizada:

* **Contextualização:** Entendimento do problema e da regra de negócio.
* **Premissas:** Definição das regras utilizadas para construção da análise.
* **Query SQL:** Código-fonte estruturado e comentado.
* **Resultado:** Apresentação dos dados retornados pela consulta.
* **Raciocínio Analítico:** Explicação da lógica utilizada e das decisões técnicas adotadas.
* **Considerações Técnicas:** Observações relacionadas à granularidade, qualidade dos dados e possíveis impactos de performance.

---
## 🧹 Qualidade e Tratamento dos Dados

O tratamento de dados no projeto segue uma premissa fundamental de governança:

> **Valores nulos não devem ser tratados automaticamente.** O tratamento deve existir apenas quando houver uma regra de negócio clara que determine qual valor deve substituir o `NULL`.

Quando não existe informação suficiente para determinar o valor correto, o comportamento mais adequado é **preservar o NULL**. Isso evita a introdução artificial de informações inexistentes na fonte.

### Exemplos Práticos:
* Um `NULL` em `total_value` **não** deve ser automaticamente convertido para `0`, pois não há evidência de que o valor da venda tenha sido zero.
* Não é adequado atribuir valores de forma arbitrária para campos sensíveis como:
  * Quantidade
  * Preço
  * Valor da venda
  * Identificadores (`IDs`)

### Aplicação de Regras de Negócio:
Quando a regra de negócio estabelece que um `NULL` possui um significado específico, o tratamento é devidamente aplicado. 

* **Exemplo:** Caso a regra determine que `NULL` em `discount` significa a ausência de desconto, utiliza-se:
  ```sql
  COALESCE(discount, 0)
  ```
---
## 🔎 Granularidade

Um dos principais cuidados durante a resolução foi controlar a granularidade dos dados em cada etapa.

### `orders`
```text
1 linha = 1 pedido
```

### `order_items`
```text
1 linha = 1 item de pedido
```

### Agregação mensal
```text
1 linha = 1 mês
```

### Agregação por seller e trimestre
```text
1 linha = 1 seller + 1 trimestre
```

### Agregação por produto
```text
1 linha = 1 produto
```

>  O controle explícito do *grain* evita problemas como duplicação de faturamento, contagem incorreta de pedidos e distorção das métricas.

---

## ⚙️ Decisões Técnicas

### CTEs
CTEs foram utilizadas para separar etapas lógicas das consultas e facilitar a leitura e manutenção do código. A utilização de CTEs também permite deixar explícitas as mudanças de granularidade ao longo das consultas.

### Window Functions
As *Window Functions* são utilizadas nos desafios em que é necessário realizar análises mantendo o contexto das linhas.

Entre as funções utilizadas estão:
* `LAG()` para comparação entre períodos.
* `RANK()` para identificação de maiores preços preservando empates.
* `ROW_NUMBER()` para controle de registros quando necessário.

#### `LAG()`
No Desafio 2, `LAG()` permite acessar o valor do trimestre anterior dentro do contexto de cada *seller*, possibilitando o cálculo da variação de GMV.

#### `RANK()`
No Desafio 4, `RANK()` é utilizado para identificar o maior preço unitário dentro de cada pedido. A escolha de `RANK()` permite preservar situações de empate: caso dois produtos possuam o mesmo maior preço, ambos são considerados como maiores preços do pedido.

### Divisão por Zero
Cálculos de crescimento percentual são protegidos contra situações em que o período anterior possua valor zero. Nesses casos, evita-se produzir uma taxa de crescimento matematicamente inválida.

---

## 🚀 Performance e Escalabilidade

Embora o case seja executado em ambiente local, as consultas foram construídas considerando princípios aplicáveis a cenários de maior volume de dados.

Entre os principais pontos considerados estão:
* Redução do volume de dados antes de agregações.
* Controle da cardinalidade dos `JOINs`.
* Definição adequada da granularidade.
* Utilização criteriosa de *Window Functions*.
* Separação das etapas por meio de CTEs.
* Eliminação de operações desnecessárias.

Em um ambiente produtivo, a performance das consultas deveria ser validada utilizando o plano de execução (*Query Plan*) da engine SQL, considerando:
* Volume de dados.
* Cardinalidade.
* Seletividade dos filtros.
* Custo das ordenações e agregações.
* Estratégia de `JOIN`.
* Índices e particionamento.

> Não é assumido que uma determinada estratégia seja necessariamente mais performática sem validação direta no ambiente de execução oficial.

---
## 📌 Considerações sobre os Desafios

### Desafio 1 — Faturamento Mensal
O faturamento é calculado utilizando `orders.total_value`, que representa o valor final pago pelo cliente após os descontos. A análise considera uma janela de exatamente 12 meses e apenas pedidos com status `completed` ou `delivered`.

As métricas apresentadas são:
* Faturamento mensal
* Quantidade de pedidos
* Ticket médio

### Desafio 2 — Crescimento de GMV
A análise compara o GMV dos *sellers* entre trimestres. 
* Para reduzir distorções causadas por *sellers* com baixo volume de pedidos, foi estabelecido o critério mínimo de **50 pedidos por trimestre**.
* A variação percentual é calculada em relação ao trimestre anterior.

### Desafio 3 — Descontos Abusivos
O **Valor Bruto**  dos itens é calculado a partir de: 
$$\text{quantidade} \times \text{unit\_price}$$

O desconto total é então comparado com o valor bruto do pedido através da regra:
$$\text{Desconto Total} > 40\% \times \text{Valor Bruto}$$

> ⚠️ Pedidos cancelados são explicitamente excluídos desta análise.

### Desafio 4 — Comportamento de Produtos
São considerados produtos que atendam simultaneamente aos seguintes critérios:
* Possuem **mais de 1.000 unidades** vendidas.
* **Nunca** foram o produto de maior preço unitário dentro de um pedido.

A utilização de `RANK()` permite tratar corretamente situações em que mais de um produto possui o maior preço unitário no mesmo pedido (cenários de empate).

---
## 📎 Arquivos de Apoio

O arquivo abaixo faz parte dos materiais de apoio utilizados no desenvolvimento e validação do case:

* `FIEMG-LayoutsValidations-v1.xlsx`

---
## 🔗 Link do Repositório
Conheça mais sobre o meu trabalho: [GitHub — Data-Engineering-26](https://github.com/bvlp06/Data-Engineering-26)
