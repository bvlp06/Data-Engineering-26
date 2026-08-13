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
* **Correção Técnica e Performance:** Otimização de consultas para grandes volumes de dados.
* **Qualidade de Código:** Queries limpas, legíveis e estruturadas com o uso de CTEs (*Common Table Expressions*).
* **Tratamento de Dados:** Manipulação de valores nulos e prevenção de erros lógicos (como divisão por zero).
* **Funções de Janela:** Uso avançado de *Window Functions* para análises granulares.
* **Documentação:** Justificativa detalhada de cada premissa de negócio adotada.

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
git clone https://github.com
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
O arquivo principal de resolução está localizado em `notebook/modelo_teste.ipynb`. Você pode utilizá-lo via **Jupyter Notebook**, **JupyterLab** ou importá-lo no **Google Colab**.

---

## 📊 Desafios Resolvidos

| ID | Desafio | Foco Técnico | Regra de Negócio Aplicada |
| :--- | :--- | :--- | :--- |
| **1** | **Faturamento Mensal** | Agregações temporais e filtros de status | Métricas dos últimos 12 meses; apenas pedidos `completed` ou `delivered`. |
| **2** | **Crescimento de GMV** | Comparações trimestrais (*MoM/QoQ*) | Filtro de qualidade: mínimo de 50 pedidos por trimestre para evitar distorções de *sellers* novos. |
| **3** | **Descontos Abusivos** | Tratamento de nulos e proteção contra divisão por zero | Identificação de pedidos com desconto superior a 40% do valor bruto. Exclui cancelados. |
| **4** | **Comportamento de Produtos** | *Window Functions* complexas e análise de qualidade | Produtos com mais de 1.000 unidades que nunca foram o item de maior valor unitário no pedido. |

---

## 🧠 Organização e Metodologia

Cada desafio possui uma seção dedicada dentro do notebook contendo:
1. **Contextualização:** Entendimento macro do problema de negócio.
2. **Query SQL:** Código fonte formatado e comentado.
3. **Resultado:** Visualização dos dados retornados.
4. **Raciocínio Analítico:** Explicação detalhada da lógica e das decisões técnicas tomadas.

---

## 🔗 Link do Repositório
Conheça mais sobre o meu trabalho: [GitHub — Data-Engineering-26](https://github.com)
