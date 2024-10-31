![fPC_JyCm4CNtV8eRsuczNLe5a41G8Y9WTfjBESdsLMSRyNLG1yJ0X5XOyyMuf2cj-BSqaoK_l_UxPsSIef6OdCswHPPH3ODR5AffOM2wm10OAeQRa9ed8Hv2l4SFWvBSC0FzHlazgh90SHH2yuu1AkmFZZEq0M4mQzRSgqyUQOxWq0UpHDTAKKI5xMQ8lChGLrJt6CPIPPhdhUcngJZ0rLn](https://github.com/user-attachments/assets/63cf022f-d84c-41fc-864c-048d2efe423c)
### Método: `Cmd_Salvar_Click` 
#### Regra de Negócio 
O método `Cmd_Salvar_Click` é responsável por realizar as validações e consistências necessárias antes de permitir o salvamento de uma averbação de transporte. Este processo assegura que os dados fornecidos estão de acordo com as políticas da empresa e com as regulamentações exigidas por diferentes seguradoras. A lógica de negócio abrange verificações de dados obrigatórios, permissões de acesso, validade de documentos e limites de responsabilidade. 
#### Execução 
1. **Verificação de Acesso e Permissão**: 
  * O método inicia validando se o usuário possui permissão para realizar a operação de salvamento.
2. **Validações de Dados Obrigatórios**:
  * Campos essenciais, como série do documento, número do documento, CPF/CNPJ do tomador e descrição do documento, são verificados. Caso estejam incompletos, o processo é interrompido.
3. **Verificações de Cancelamento**:
    * São realizadas verificações para identificar se a averbação foi cancelada. Dependendo da origem do cancelamento (manual ou automático via WebService), mensagens de alerta específicas são exibidas ao usuário.
4. **Validação de Limites e Políticas das Seguradoras**:
    * Validações específicas das seguradoras, como Liberty, AXA, Mitsui, entre outras, são aplicadas. Estas verificações incluem:
      * Controle de limites de responsabilidade por apólice.
      * Verificações de datas e adequação do percurso de transporte.
      * Consistência entre valores segurados acumulados e limites das apólices.
5. **Finalização e Salvamento**:
* Após todas as validações, a averbação é salva no sistema. Caso alguma verificação falhe, uma mensagem de erro é apresentada, orientando o usuário sobre como proceder. 
#### Tratamentos de Erro 
* **Falha de Acesso**: Se o usuário não tiver permissão, o processo é interrompido imediatamente, e uma mensagem de erro é exibida. 
* **Dados Obrigatórios Ausentes**: Campos obrigatórios ausentes ou incompletos resultam em mensagens de erro, indicando o campo específico que deve ser preenchido.
* **Cancelamento Identificado**: Quando a averbação já está cancelada, uma mensagem de aviso é exibida (com distinção entre cancelamento manual e WS).
* **Inconsistência nos Limites de Responsabilidade**: Quando o valor segurado total ultrapassa o limite da apólice, o processo é interrompido com uma mensagem de alerta.
* **Outras Inconsistências de Dados**: Qualquer dado em formato incorreto, como documentos fora do padrão ou campos de valor inválido, gera mensagens de erro direcionadas, impedindo o salvamento da averbação até que o usuário corrija a entrada.



