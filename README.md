# 📊 Relatório de Faturamento por Data

Este projeto contém uma query SQL utilizada para gerar um relatório de faturamento com base em critérios específicos de pedidos. A consulta foi construída para retornar, por data de faturamento, o valor total vendido e a quantidade distinta de clientes atendidos.

---

## 🧩 Estrutura da Query

```sql
SELECT
    PD.DTFAT AS dt,
    SUM(PD.VLTOTAL) AS vltotal,
    COUNT(DISTINCT PD.codcli) AS qtcli
FROM
    PCPEDC PD
WHERE
    PD.DTFAT BETWEEN TO_DATE('01/10/2024', 'dd/mm/yyyy') AND TO_DATE('31/03/2025', 'dd/mm/yyyy')
    AND PD.POSICAO = 'F'
    AND PD.CONDVENDA = 7
    AND PD.NUMPED IN (SELECT NUMPED FROM PCPEDI WHERE TIPOENTREGA <> 'EN')
GROUP BY
    PD.DTFAT
ORDER BY
    PD.DTFAT;
```

---

## 📅 Objetivo

Gerar um relatório **diário** com os seguintes indicadores:
- **Data de Faturamento (`dt`)**
- **Valor Total Faturado no Dia (`vltotal`)**
- **Quantidade de Clientes Distintos Atendidos no Dia (`qtcli`)**

---

## 📌 Filtros Aplicados

- **Período:** de `01/10/2024` a `31/03/2025`
- **Status do Pedido:** apenas pedidos com `POSICAO = 'F'` (faturados)
- **Condição de Venda:** apenas pedidos com `CONDVENDA = 7`
- **Tipo de Entrega:** exclui pedidos com `TIPOENTREGA = 'EN'` (entrega normal)

---

## 📦 Tabelas Utilizadas

- `PCPEDC`: Cabeçalho de pedidos (contém informações gerais como data de faturamento, valor e cliente)
- `PCPEDI`: Itens do pedido (utilizado para filtrar tipos de entrega)

---

## 🗂️ Resultado Esperado

Um conjunto de registros com a seguinte estrutura:

| Data de Faturamento | Valor Total | Qtde de Clientes |
|---------------------|-------------|------------------|
| 01/10/2024          | 15000.00    | 12               |
| 02/10/2024          | 18900.50    | 17               |
| ...                 | ...         | ...              |

---

## ✅ Uso Sugerido

Ideal para relatórios financeiros, dashboards gerenciais ou análises de desempenho de vendas por período.

---

## 🛠️ Dependências

- Banco Oracle (uso de `TO_DATE`)
- Acesso às tabelas `PCPEDC` e `PCPEDI` com permissões de leitura

---

## 📬 Contato

Caso precise de ajuda para adaptar a consulta ou integrar em relatórios BI, entre em contato.
