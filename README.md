# Sistema de Vendas (Sale) e Vendedores (Seller)

Trata-se de um sistema de vendas (Sale) e vendedores (Seller). Cada venda está associada a um vendedor, e um vendedor pode ter várias vendas.

## Consultas

### Relatório de Vendas
1. **[IN]** O usuário informa, opcionalmente, data inicial, data final e um trecho do nome do vendedor.
2. **[OUT]** O sistema retorna uma listagem paginada contendo:
   - ID
   - Data
   - Quantia vendida
   - Nome do vendedor
   Das vendas que se enquadram nos dados informados.

**Informações complementares:**
- Se a data final não for informada, considera-se a data atual do sistema. Para instanciar a data atual, use o comando:
```java
LocalDate today = LocalDate.ofInstant(Instant.now(), ZoneId.systemDefault());
```
**Data Inicial Não Informada:**  
  Se a data inicial não for informada, considera-se a data de 1 ano antes da data final. Para instanciar uma data com um ano a menos, use a função `minusYears`:
  ```java
  LocalDate result = minhaData.minusYears(1L);
```
## Nome Não Informado

Se o nome não for informado, considera-se o texto vazio.

**Dica:** Receba todos os dados como `String` no controller e faça os tratamentos das datas no service, instanciando os objetos `LocalDate`.

---

## Sumário de Vendas por Vendedor

1. **[IN]** O usuário informa, opcionalmente, data inicial e data final.
2. **[OUT]** O sistema retorna uma listagem contendo:
   - Nome do vendedor
   - Soma das vendas deste vendedor no período informado.

**Informações complementares:**
- As mesmas condições do caso de uso "Relatório de Vendas".

---

## Competências:

### 1) Importação do Projeto

Simples clone do projeto no Github, importar e executar o mesmo na IDE, sem necessidade de configurações especiais.

### 2) Testes Manuais no Postman

#### 2.1) Sumário de Vendas por Vendedor (Teste 1)
**GET** `/sales/summary?minDate=2022-01-01&maxDate=2022-06-30`

Deverá retornar o sumário de vendas por vendedor no período informado:

```json
[
  {
    "sellerName": "Anakin",
    "total": 110571.0
  },
  {
    "sellerName": "Logan",
    "total": 83587.0
  },
  {
    "sellerName": "Loki Odinson",
    "total": 150597.0
  },
  {
    "sellerName": "Padme",
    "total": 135902.0
  },
  {
    "sellerName": "Thor Odinson",
    "total": 144896.0
  }
]
```
#### 2.2) Sumário de Vendas por Vendedor (Teste 2)
**GET** `/sales/summary`

Deverá retornar o sumário de vendas por vendedor dos últimos 12 meses.

---

#### 2.3) Relatório de Vendas (Teste 1)
**GET** `/sales/report`

Deverá retornar o relatório de vendas dos últimos 12 meses.

---

#### 2.4) Relatório de Vendas (Teste 2)
**GET** `/sales/report?minDate=2022-05-01&maxDate=2022-05-31&name=odinson`

Deverá retornar o relatório de vendas do período/vendedor informados:

```json
{
  "content": [
    {
      "id": 9,
      "date": "2022-05-22",
      "amount": 19476.0,
      "sellerName": "Loki Odinson"
    },
    {
      "id": 10,
      "date": "2022-05-18",
      "amount": 20530.0,
      "sellerName": "Thor Odinson"
    },
    {
      "id": 12,
      "date": "2022-05-06",
      "amount": 21753.0,
      "sellerName": "Loki Odinson"
    }
  ]
}
```
