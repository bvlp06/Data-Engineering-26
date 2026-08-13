# Teste Técnico — Engenharia de Dados

## Sobre o desafio

Este repositório contém a resolução do teste técnico para a posição de Engenheiro(a) de Dados.

O desafio consiste na resolução de problemas de negócio utilizando SQL, com foco em:

- Correção técnica;
- Qualidade e legibilidade das queries;
- Tratamento de dados;
- Performance;
- Uso de CTEs e window functions;
- Raciocínio analítico;
- Documentação das soluções.

## Estrutura do projeto

```text
.
├── notebook/
│   └── modelo_teste.ipynb
├── README.md
├── requirements.txt
└── .gitignore


Dados

Os arquivos CSV utilizados na resolução foram fornecidos juntamente com o teste técnico.

Por se tratarem de arquivos disponibilizados para a realização do desafio, eles não estão versionados neste repositório.

Para executar o notebook localmente, os arquivos devem estar disponíveis na pasta:

data/

O arquivo auxiliar utilizado durante o desenvolvimento também não está versionado no repositório (podendo disponibilizar posteriormente).

Como executar
1. Clonar o repositório

Após clonar o repositório:

git clone <URL_DO_REPOSITORIO>
cd FIEMG
2. Criar o ambiente virtual

No terminal:

python -m venv .venv
3. Ativar o ambiente virtual

No Windows:

.venv\Scripts\activate

No Linux/macOS:

source .venv/bin/activate
4. Instalar as dependências

Com o ambiente virtual ativado:

pip install -r requirements.txt
5. Disponibilizar os dados

Os arquivos CSV fornecidos para o teste devem ser disponibilizados na pasta:

data/
6. Executar o notebook

O notebook com as resoluções está localizado em:

notebook/teste_tecnico_engenharia_dados.ipynb

O notebook pode ser executado localmente utilizando Jupyter Notebook/JupyterLab ou pelo Google Colab.

Desafios
Desafio 1 — Faturamento mensal

O objetivo é calcular o faturamento bruto mensal dos últimos 12 meses, considerando apenas pedidos com status completed ou delivered.

O resultado apresenta:

Faturamento bruto mensal;
Quantidade de pedidos;
Ticket médio;
Período ordenado do mês mais recente para o mais antigo.

A análise considera apenas pedidos válidos para faturamento, excluindo pedidos cancelados e reembolsados.

Desafio 2 — Crescimento de GMV

O objetivo é identificar os 10 sellers com maior crescimento de GMV entre o trimestre atual e o trimestre anterior.

Para evitar distorções causadas por sellers novos ou com baixa atividade, são considerados apenas sellers que possuem pelo menos 50 pedidos em ambos os trimestres.

O resultado apresenta:

Nome do seller;
Estado;
GMV do trimestre anterior;
GMV do trimestre atual;
Percentual de crescimento.

Os resultados são ordenados pelo maior percentual de crescimento.

Desafio 3 — Descontos abusivos

O objetivo é identificar pedidos nos quais o desconto total aplicado aos itens representa mais de 40% do valor bruto do pedido.

Pedidos com status cancelled são excluídos da análise.

O resultado apresenta:

Identificação do pedido;
Seller responsável;
Data do pedido;
Valor bruto do pedido;
Valor total de desconto;
Percentual de desconto.

A análise também considera o tratamento de possíveis valores nulos e divisão por zero.

Desafio 4 — Comportamento dos produtos

O objetivo é identificar produtos que apresentam alto volume de vendas, mas que nunca aparecem como o item de maior valor unitário dentro de um pedido.

São considerados produtos que:

Possuem mais de 1.000 unidades vendidas;
Nunca foram o item de maior valor unitário em nenhum pedido.

Para identificar o item de maior valor unitário em cada pedido, são utilizadas Window Functions.

Em situações de empate no maior valor unitário, os produtos empatados são considerados como itens de maior valor unitário.

Além da consulta, são avaliadas possíveis limitações e questões relacionadas à qualidade e à viabilidade da análise.

Organização das soluções

Cada desafio está documentado diretamente no notebook, contendo:

Contextualização do problema;
Query SQL;
Resultado da consulta;
Explicação do raciocínio utilizado;
Considerações sobre regras de negócio;
Tratamento de possíveis problemas nos dados, quando aplicável.
Observações

As soluções foram desenvolvidas buscando equilibrar correção técnica, legibilidade, performance e clareza das regras de negócio.

As principais premissas, decisões e considerações sobre os resultados estão documentadas diretamente no notebook.