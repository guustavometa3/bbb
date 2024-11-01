![XL6nJWCn3DtlApnU9RwW35IK8dM01NuWoZdKKiu-ubo5-9kA0PMTXJK_XdDGgRG3KOR8US_FxtcXsQKyzh6P7aqpNpDvSY0m9F6eAj0XR35H8E_AUtcR2jwnn-Xwv2oNnhh1G8pmF29mXMpAxWy64ZwHvkGwWJPXbiG2D4d5MMrmFQftLWcI-YhpYNgg0wCwDhwMVIAyCA6l7fEDKwyVVp0](https://github.com/user-attachments/assets/dcc87400-6962-4a9f-af21-e679b8224e7f)

### Método: `FU_Verifica_Cancelamento_CTE` 

#### Regra de Negócio
O método `FU_Verifica_Cancelamento_CTE` verifica se um documento (identificado por série, número e CTE) possui um cancelamento registrado no sistema. Essa verificação é essencial para garantir que a operação de salvamento posterior não continue caso o documento já tenha sido cancelado, prevenindo a duplicidade de processos para documentos cancelados.

#### Execução
**Definição do Estado Inicial:** 
- O método é iniciado assumindo que o documento não possui cancelamento registrado.

**Consulta de Cancelamento:** 
- O sistema busca por registros de cancelamento na base de dados usando os parâmetros fornecidos: série, número do documento e CTE. 
- Essa busca é específica e retorna dados apenas se houver um registro de cancelamento para o documento solicitado.

**Identificação de Cancelamento:** 
- Se o registro de cancelamento existe, o sistema altera o retorno do método para indicar que o documento foi cancelado e registra o responsável pelo cancelamento. 
- Caso não exista cancelamento, o retorno permanece como inicialmente definido, indicando a ausência de cancelamento.

**Finalização:** 
- O método é concluído retornando uma indicação de cancelamento (`True`) ou de ausência de cancelamento (`False`), permitindo que o processo principal siga de acordo com o status do documento.

#### Tratamentos de Erro
- **Ausência de Registro de Cancelamento:** Quando o documento não possui um cancelamento registrado, o método retorna `False`, indicando que o processo pode continuar. 
- **Cancelamento Encontrado:** Se o cancelamento existe, o método retorna `True`, interrompendo o processo principal e identificando o responsável pelo cancelamento. Essa verificação evita tentativas de salvamento de documentos previamente cancelados.

