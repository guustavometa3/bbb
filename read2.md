### Método: `Cmd_Salvar_Click` 
#### Regra de Negócio O método `Cmd_Salvar_Click` executa uma sequência de validações para assegurar que a averbação atende aos requisitos de integridade de dados, regras de apólice e conformidade com as normas de cada seguradora. Cada verificação foi projetada para manter a consistência dos dados e evitar cadastros incorretos no sistema. Ele contempla verificações de dados de entrada (como campos obrigatórios e consistências de tipo e valor), requisitos específicos de seguradoras e validações de limites financeiros. 
#### Execução 
1. **Inicialização e Verificação de Acesso**: * A variável `apo_i_opr_ddr` é limpa. * O método `Fu_Verifica_Acesso_HDI` é chamado para verificar se o usuário tem permissão de acesso; caso contrário, o método é encerrado (`Exit Sub`). 
2. **Validação de Cancelamento de Averbação**: 
	* Se a variável `Ind_Canc_AVB%` estiver `True`, o código valida o cancelamento com `FU_Verifica_Cancelamento_CTE`, buscando correspondência no documento e exibindo mensagens de alerta específicas para cancelamentos automáticos e manuais. 
3. **Checagem de Movimentação**: 
	* Com `Fu_Verifica_Fech_sem_Movimento`, é validado se já existe um fechamento de período sem movimentação. Se houver, o método é interrompido com um aviso ao usuário. 
4. **Validação de Dados Específicos de Seguradoras**: 
	* São realizadas verificações distintas para as seguradoras. Por exemplo: * Para Mitsui, valida-se a consistência de ano (`Txt_U_PT1_AVB` e `Dtb_D_SDA_VGM`). * Para STARR, é verificada a obrigatoriedade do CNPJ (`Txt_u_cpf_cgc_emb`), usando o método `Fu_CNPJ_Pagador_Valido`. 
5.	**Verificações de Documentos e Consistências**: 
	* Campos como `Txt_U_SER_DOC` (série) e `Txt_U_DOC_INI` (número do documento) são obrigatórios dependendo do tipo de documento em `Cmb_e_doc_ebq`. * Documentos com 44 dígitos devem ser numéricos, e o método `FU_Calcular_Digito_Verificar_CTE` é invocado para validar dígitos verificadores. 
6. **Cálculo e Verificação de Limite de Responsabilidade**: 
	* Calcula o limite de responsabilidade de acordo com a seguradora, verificando o valor acumulado em `Fu_Efetua_Acumulo_Risco` e `Fu_Obtem_Limite_Mercadoria`. * Se o valor segurado total (`FLT_V_IS`, `flt_v_is_fte`, `Flt_V_IS_CNN`, e `v_is_acumulada@`) exceder o limite da apólice (`v_lim_rsp_vgm@`), exibe uma mensagem de alerta. 
7. **Verificação do Estado e Cidade**: 
	* Checa se as UFs de origem, transbordo e destino estão preenchidas e se o percurso é adequado (rodo-fluvial ou rodoviário) de acordo com os estados. 
8. **Finalização e Salvamento**: 
	* Se todas as verificações forem aprovadas, o método conclui o salvamento da averbação. 
	* Caso haja alguma falha, uma mensagem específica direciona o usuário para corrigir o erro antes de prosseguir. 
#### Tratamentos de Erro
 * **Permissão de Acesso**: Em caso de falha de permissão no `Fu_Verifica_Acesso_HDI`, o método é interrompido com `Exit Sub`. 
 * **Campos Obrigatórios Ausentes**: Cada campo obrigatório ausente é tratado individualmente. Se `Txt_U_SER_DOC` ou `Txt_U_DOC_INI` estiver vazio, uma `MsgBox` direciona o usuário ao campo específico. 
 * **Cancelamento de Averbação**: Se `Ind_Canc_AVB%` for verdadeiro e o cancelamento for confirmado, exibe uma mensagem de cancelamento, interrompendo a execução. 
 * **Inconsistência nos Limites de Responsabilidade**: Se o valor segurado excede o limite da apólice, o método é interrompido e exibe uma mensagem de alerta. 
 * **Erros de Validação de CPF/CNPJ**: Utilizando `Fu_CNPJ_Pagador_Valido` e `Fu_Verifica_CGC%`, os valores de CPF/CNPJ incorretos geram mensagens de erro e focam o campo específico. * **Erros de Documentação**: Para documentos fora do padrão esperado, a `MsgBox` informa o usuário e o método é interrompido até que os dados sejam corrigidos.



