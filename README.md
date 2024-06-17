# DashBoard Corporativo

## Criando Dashboard Corporativo com Integração com MySQL e Azure

### Descrição do Desafio Módulo 3 – Processamento de Dados Simplificado com Power BI

### Passos:

1. **Criação de uma Instância na Azure para MySQL**
   
2. **Criar o Banco de Dados com Base Disponível no GitHub**

   2.1. O banco de dados foi criado, mas houve divergências no processo em comparação ao da professora. A sintaxe de `{` mudou para `(` na criação e INSERT de tabelas. Além disso, ao inserir os colaboradores, foi necessário inserir os chefes em primeira análise.

3. **Integração do Power BI com MySQL no Azure**

   3.1. Foi necessário o download do arquivo SSL no site [DigiCert Root Certificates](https://www.digicert.com/kb/digicert-root-certificates.htm#roots).

4. **Verificar Problemas na Base a Fim de Realizar a Transformação dos Dados**

### Diretrizes para Transformação dos Dados

1. **Verifique os Cabeçalhos e Tipos de Dados**

   1.1. IDs foram considerados, em primeira análise, como dados textuais e não numéricos.

   1.2. Colunas de metadados foram removidas.

3. **Modifique os Valores Monetários para o Tipo Double Preciso**

   3.1. A coluna Salários foi modificada para número decimal fixo.

4. **Verifique a Existência dos Nulos e Analise a Remoção**

   4.1. Elementos nulos foram encontrados em um membro da tabela de employees, mas tal fato é justificável por gerência. Pode-se afirmar isso conferindo o alto salário na coluna "Salários" e sua listagem no departamento "Headquarters", o que sugere uma gerência de instância superior.

   4.2. Na base, pode ser encontrado um elemento zero na coluna horas da tabela works_on referente ao colaborador James, previamente encontrado nulo em Super_ssn. O zero não será alterado, pois pode significar que horas trabalhadas no cargo de gerência (administrativo) não são consideradas na tabela.

6. **Os Employees com Nulos em Super_ssn Podem Ser os Gerentes. Verifique se Há Algum Colaborador Sem Gerente**

   Não há colaboradores sem gerentes, exceto James, previamente mencionado.

8. **Verifique se Há Algum Departamento Sem Gerente**

   Não há.

9. **Se Houver Departamento Sem Gerente, Suponha que Você Possui os Dados e Preencha as Lacunas**

   Não há.

10. **Verifique o Número de Horas dos Projetos**

   Já previamente citado.

11. **Separar Colunas Complexas**

   Separado a coluna Address em número, rua, cidade e estado (UF).

12. **Mesclar Consultas Employee e Department para Criar uma Tabela Employee com o Nome dos Departamentos Associados aos Colaboradores**

    A mescla terá como base a tabela employee. Fique atento, essa informação influencia no tipo de junção.

13. **Neste Processo Elimine as Colunas Desnecessárias**

    Foi utilizada a junção por mescla a partir das colunas Super_ssn e Mgr_ssn, pois a primeira indica o gerente responsável pelo colaborador e a segunda o gerente responsável pelo departamento. Para detectar os departamentos dos colaboradores, a coluna que indica o gerente na tabela de colaboradores deverá indicar o gerente do respectivo departamento em que o colaborador atua. Demais colunas foram excluídas, já que a informação adicional desejada é apenas a coluna de departamento. É importante ressaltar que a opção "Mesclar consultas como novas" foi escolhida a fim de criar uma nova tabela.

14. **Realize a Junção dos Colaboradores e Respectivos Nomes dos Gerentes**

    Isso pode ser feito com consulta SQL ou pela mescla de tabelas com Power BI. Caso utilize SQL, especifique no README a query utilizada no processo.

    Novamente, a opção "Mesclar consultas como novas" com as condições Super_ssn e ssn para linkar o nome dos gerentes aos colaboradores. Em relação à coluna employees, apenas foram adicionadas as colunas "First" e "Last" names dos gerentes; as demais foram descartadas.

15. **Mescle as Colunas de Nome e Sobrenome para Ter Apenas uma Coluna Definindo os Nomes dos Colaboradores**

    Para fazer esse processo, foram realizados os passos:
    
    1. Ir até a guia Adicionar Coluna (Add Column).
    
    2. Clicar em Coluna Personalizada (Custom Column).
    
    3. Dar um nome à nova coluna, como Nome Completo.
    
    4. Criar e inserir a Fórmula de Concatenação: `[Fname] & " " & [Lname]`.

16. **Mescle os Nomes de Departamentos e Localização**

    Isso fará que cada combinação departamento-local seja única, auxiliando na criação do modelo estrela em um módulo futuro.

    Para fazer isso, uniremos as colunas Department e Dlocation, após a mescla das tabelas Dept_location e Department através das colunas Dnumber presente em ambas.

17. **Explique por que, Neste Caso Supracitado, Podemos Apenas Utilizar o Mesclar e Não o Atribuir**

    Podemos utilizar apenas o mesclar porque ambas as tabelas possuem o Dnumber que referencia o número do departamento em questão.

18. **Agrupe os Dados a Fim de Saber Quantos Colaboradores Existem por Gerente**

    ![Figura: Contagem de Colaboradores por Gerentes](https://github.com/Anajulia-gon/DashBoardCorporativo/blob/main/figura-contagem-de-colaboradores-por-gerentes.png)

19. **Elimine as Colunas Desnecessárias**

    Elimine as colunas que não serão usadas no relatório de cada tabela.
