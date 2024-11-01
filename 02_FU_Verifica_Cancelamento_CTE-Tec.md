![RP5VQiCm3CRVVGgjzA65iWCaXBMq2HjqAqiBUpIEgow6n2woFCQkiwFiObFJFp2O7-nOihvyFsaUsH2dlbF3Xr9PZHOR93WQCZqoXPWh7nY1t7lB6KGaX-CPx8ETmN9NZgNcoJlhJEU-344TmOO-WEW4saVaN6KhF3Zl20Wva0_d1vNf8kPIlGm-CYN9Rr_NVtyc0IXWj2tNvN87NgUOjFC](https://github.com/user-attachments/assets/47fbeb51-1514-4ccd-b752-8dd8918e7925)
# FU_Verifica_Cancelamento_CTE

## Regra de Negócio
O método `FU_Verifica_Cancelamento_CTE` é responsável por verificar se um determinado CTE (Conhecimento de Transporte Eletrônico) foi cancelado. Ele realiza essa verificação consultando a tabela `tb_can_cte_avb_nac_cit` no banco de dados, utilizando informações como a série do documento, o número do documento e o CTE.

## Execução
1. O método recebe três parâmetros:
   - `serie$`: String que representa a série do documento.
   - `doc`: Número do tipo `Double` que representa o documento.
   - `CTE$`: String que representa o número do CTE.
   
2. Um objeto `Recordset` (`Rs`) é inicializado para armazenar o resultado da consulta SQL.

3. O método constrói uma consulta SQL que seleciona o campo `n_usu_inc` da tabela `tb_can_cte_avb_nac_cit`, filtrando pelos parâmetros fornecidos (`u_ser_doc`, `u_doc_ini` e `u_cnh_elt`).

4. A consulta é executada e o resultado é armazenado em `Rs`.

5. O método verifica se o `Recordset` não está no final (`EOF`). Se houver resultados, o retorno da função é definido como `True` e a variável `n_usu_inc_can` é preenchida com o valor do campo `n_usu_inc`.

6. O `Recordset` é fechado antes do final da execução.

## Tratamentos de Erro
O método não possui tratamentos de erro explícitos implementados. Recomenda-se a inclusão de um mecanismo de tratamento de erros para capturar e gerenciar possíveis exceções durante a execução da consulta SQL e o manuseio do `Recordset`, como problemas de conexão com o banco de dados ou erros de sintaxe na consulta.

# Plano de Teste para o Método FU_Verifica_Cancelamento_CTE

## 1. Objetivo do Teste
Validar a funcionalidade do método `FU_Verifica_Cancelamento_CTE`, assegurando que ele verifica corretamente o cancelamento de um CTE com base nos parâmetros fornecidos.

## 2. Cenários de Teste

### 2.1. Cenário 1: CTE Cancelado
- **Descrição**: Testar a situação onde o CTE fornecido foi cancelado.
- **Entradas**:
  - `serie$`: "S1"
  - `doc`: 12345
  - `CTE$`: "CTE123"
- **Resultado Esperado**: 
  - O método deve retornar `True`.
  - A variável `n_usu_inc_can` deve conter o valor do usuário que cancelou.

### 2.2. Cenário 2: CTE Não Cancelado
- **Descrição**: Testar a situação onde o CTE fornecido não foi cancelado.
- **Entradas**:
  - `serie$`: "S2"
  - `doc`: 67890
  - `CTE$`: "CTE456"
- **Resultado Esperado**: 
  - O método deve retornar `False`.

### 2.3. Cenário 3: Parâmetros Inválidos
- **Descrição**: Testar o método com valores de entrada que não correspondem a nenhum registro na tabela.
- **Entradas**:
  - `serie$`: "S3"
  - `doc`: 99999
  - `CTE$`: "CTE999"
- **Resultado Esperado**: 
  - O método deve retornar `False`.

### 2.4. Cenário 4: Parâmetros Nulos
- **Descrição**: Testar o método com valores nulos para verificar o tratamento.
- **Entradas**:
  - `serie$`: `Null`
  - `doc`: `Null`
  - `CTE$`: `Null`
- **Resultado Esperado**: 
  - O método deve retornar `False`.
  
### 2.5. Cenário 5: Erro de Conexão com o Banco de Dados
- **Descrição**: Simular uma falha de conexão com o banco de dados ao executar a consulta.
- **Entradas**:
  - `serie$`: "S1"
  - `doc`: 12345
  - `CTE$`: "CTE123"
- **Resultado Esperado**: 
  - O método deve tratar a exceção adequadamente e não deve falhar.

## 3. Pré-condições
- O ambiente de testes deve ter acesso ao banco de dados.
- A tabela `tb_can_cte_avb_nac_cit` deve estar populada com dados relevantes para os testes.

## 4. Pós-condições
- O estado do banco de dados deve ser consistente após os testes.
- Nenhum dado deve ser modificado durante os testes, a menos que seja parte do teste.

## 5. Ferramentas e Métodos
- Ferramentas de teste unitário (como NUnit ou similar) para executar os testes automatizados.
- Utilizar mocks ou stubs para simular respostas do banco de dados quando necessário.

## 6. Critérios de Aceitação
- O método deve passar em todos os cenários de teste sem falhas.
- Os resultados devem corresponder às expectativas definidas em cada cenário. 

