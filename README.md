
## Relatório : Processamento de Dados Simplificado com Power BI
Objetivo do Desafio
Este relatório detalha o processo de criação e manipulação de um banco de dados e integração com o Power BI, utilizando uma instância MySQL no Azure, além de explorar transformações de dados para gerar relatórios e insights corporativos. 


### Descrição – Processamento de Dados Simplificado com Power BI

Etapas do projeto
1. **Criação de uma Instância MySQL no Azure**

Foi provisionada uma instância MySQL na Azure para hospedar o banco de dados.
Criação do Banco de Dados: A base de dados foi criada com a estrutura disponível no GitHub. Durante o processo, foram observadas diferenças na sintaxe em comparação ao tutorial da instrutora, como o uso de {} em vez de () na criação e inserção de tabelas. Além disso, ao adicionar registros de colaboradores, foi necessário inserir os chefes primeiro para garantir integridade referencial.

2. **Integração do Power BI com MySQL no Azure**

Para conectar o Power BI à instância MySQL na Azure, foi necessário:
- Download do Certificado SSL: Foi feito o download do certificado SSL do site DigiCert Root Certificates para estabelecer uma conexão segura entre o Power BI e o MySQL.

3. **Verificação e Transformação de Dados**

Foram identificados e solucionados problemas na base de dados para garantir consistência e integridade dos dados.

3.1. **Verificação dos Cabeçalhos e Tipos de Dados**

Tipos de Dados: Os IDs foram inicialmente tratados como texto em vez de números.
Remoção de Colunas Irrelevantes: Colunas de metadados que não contribuem para a análise foram removidas.

3.2. **Modificação de Valores Monetários**

A coluna de Salários foi convertida para o tipo "número decimal fixo" para garantir precisão nos cálculos financeiros.

3.3. **Identificação e Tratamento de Valores Nulos**

Foi identificado um registro nulo na coluna Super_ssn da tabela employees, associado a um colaborador no departamento "Headquarters" com um alto salário. Concluímos que essa ausência de valor se justifica pela posição de gerência.
Na coluna horas da tabela works_on, foi encontrado um valor zero para o colaborador James, previamente identificado como gerente (com Super_ssn nulo). Esse valor foi mantido, pois pode indicar que as horas de trabalho administrativo não são contabilizadas.

3.4. **Verificação de Relações Hierárquicas**

Colaboradores sem Gerente: Apenas James não possui gerente, conforme esperado.
Departamentos sem Gerente: Todos os departamentos possuem um gerente.

4. **Transformação e Modelagem dos Dados**
   
4.1. **Separação de Colunas Complexas**

A coluna Address foi desmembrada em Número, Rua, Cidade e Estado (UF) para facilitar a análise.

4.2. **Mesclagem de Dados entre Colaboradores e Departamentos**

Foi realizada uma junção entre as tabelas employee e department para associar cada colaborador ao seu respectivo departamento. A mesclagem foi baseada nas colunas Super_ssn (representando o gerente do colaborador) e Mgr_ssn (representando o gerente do departamento). As colunas irrelevantes foram removidas para simplificar a tabela final.

4.3. **Associações entre Colaboradores e Gerentes**

Os nomes dos gerentes foram associados aos colaboradores utilizando a mesclagem de consultas. Apenas os nomes "Primeiro" e "Último" dos gerentes foram mantidos, enquanto as demais colunas foram descartadas.

4.4. **Concatenação de Colunas para Identificação Completa** 

Para melhorar a identificação dos colaboradores:

Foi criada uma nova coluna "Nome Completo" pela concatenação de Fname e Lname.

4.5. **Criação de Identificadores de Departamentos por Localização**

Para apoiar um modelo estrela em uma futura análise, foi criada uma coluna única para combinar as informações de Department e Dlocation, unindo as tabelas Dept_location e Department com base no campo Dnumber.

Justificativa para o Uso de Mesclagem: Como ambas as tabelas compartilham a coluna Dnumber, a mesclagem foi possível e apropriada.

5. **Eliminação as Colunas Desnecessárias**

    Colunas que não se apresentaram relevantes para os possivies objetivos do DashBoard foram excluídos

6. **Agrupamento de Dados por Gerente** 
Para análise de equipe, foi realizado o agrupamento dos dados para calcular o número de colaboradores sob responsabilidade de cada gerente.


7. **Agrupamento de Dados a Fim de Investigar Quantos Colaboradores Existem por Gerente (exemplo de insigths)]**

    ![Figura: Contagem de Colaboradores por Gerentes](https://github.com/Anajulia-gon/DashBoardCorporativo/blob/main/figura-contagem-de-colaboradores-por-gerentes.png)



###  Conclusão
O processo descrito acima permitiu organizar, transformar e integrar dados entre o MySQL no Azure e o Power BI, facilitando a análise e visualização de informações gerenciais. O desafio abordou diversas técnicas de manipulação de dados, como tratamento de nulos, padronização de tipos de dados, e mesclagem de tabelas, que foram essenciais para a criação de uma estrutura de dados robusta e consistente.
