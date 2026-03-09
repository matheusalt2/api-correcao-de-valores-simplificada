# API Correção de Valores (Calculadora Cidadão)

Esta API pública permite calcular valores corrigidos por índices financeiros brasileiros, utilizando a Calculadora do Cidadão do Banco Central como fonte oficial. Ideal para aplicações, planilhas, sistemas financeiros e qualquer cenário que exija atualização monetária automática e confiável.

## Objetivo

- Oferecer uma API REST aberta, gratuita e sem autenticação para correção de valores monetários.
- Tornar acessível, via internet, os mesmos cálculos disponíveis na Calculadora do Cidadão do Banco Central.
- Permitir integração fácil com qualquer linguagem, sistema ou planilha.

## Endpoint principal

```
https://api-correcaodevalores.vercel.app/
```

## Endpoints disponíveis

- `/corrigir_selic` — Corrige valor pela taxa SELIC
- `/corrigir_cdi` — Corrige valor pelo CDI
- `/corrigir_tr` — Corrige valor pela TR
- `/corrigir_poupanca` — Corrige valor pela remuneração da poupança
- `/corrigir_indice_de_preco` — Corrige valor por índices de preço (IGP-M, IPCA, INPC, etc)

Consulte a documentação visual em `/documentacao` ou a documentação interativa em `/docs`.

## Exemplo de uso (PowerShell)

```
Invoke-RestMethod -Uri https://api-correcaodevalores.vercel.app/corrigir_selic -Method POST -Body '{"data_inicial": "2019-12-02", "data_final": "2020-01-02", "valor": 100}' -ContentType "application/json"
```

## Parâmetros de entrada

- Datas: formato `YYYY-MM-DD` (ex: "2020-01-02")
- Valores: número decimal (ex: 100.50)
- Índices: string (ex: "IGP-M", "IPCA")

## Resposta

- Sucesso:
```json
{
  "input": { ... },
  "valor_corrigido": 123.45
}
```
- Erro:
```json
{
  "error_code": "BCB_BUSINESS_ERROR",
  "error_message": "Valor do índice não disponível para o período solicitado"
}
```

## Exemplos de endpoints

- Corrigir SELIC:
  - POST `/corrigir_selic` com `{ "data_inicial": "2019-12-02", "data_final": "2020-01-02", "valor": 100 }`
- Corrigir CDI:
  - POST `/corrigir_cdi` com `{ "data_inicial": "2019-12-02", "data_final": "2020-01-02", "valor": 100, "cdi": 100 }`
- Corrigir TR:
  - POST `/corrigir_tr` com `{ "data_inicio_serie": "2008-12-02", "data_vencimento_serie": "2020-01-02", "valor": 100, "data_efetivo_pagamento": "2020-01-03" }`
- Corrigir Poupança:
  - POST `/corrigir_poupanca` com `{ "data_inicial": "2019-12-02", "data_final": "2020-01-02", "valor": 100, "regra_nova": true }`
- Corrigir Índice de Preço:
  - POST `/corrigir_indice_de_preco` com `{ "mes_inicial": "2019-12", "mes_final": "2020-01", "valor": 100, "indice_de_preco": "IGP-M" }`
  - Possíveis valores para `indice_de_preco`: "IGP-M", "IGP-DI", "INPC", "IPCA", "IPCA-E", "IPC-BRASIL", "IPC-SP"

## Licença
Este projeto é proprietário. Todos os direitos reservados ao autor. Nenhuma parte pode ser copiada, redistribuída ou utilizada sem permissão expressa por escrito.
