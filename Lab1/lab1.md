# Trabalhando com Machine Learning na Prática no Azure ML

## Desafio

1. Crie um novo repositório no github com um nome a sua preferência
2. Crie um modelo de previsão com seus devidos pontos de extremidade configurados
3. Escreva o passo a passo desse processo em um readme.md de como você chegou nessa etapa
4. Salve nesse repositório o readme.md e o arquivo .json de pontos de extremidade
5. Compartilhe conosco o link desse repositório através do botão 'entregar projeto'

Explore Azure AI Services: 
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/02-content-safety.html

Explore Automated Machine Learning in Azure Machine Learning:
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html

## Tutorial

Passo a passo para utilizar o Machine Learning Automatizado no Microsoft Azure:

1. Crie um espaço de trabalho Azure Machine Learning:
   - Faça login no portal Azure em https://portal.azure.com.
   - Selecione + Criar um recurso e procure por Machine Learning.
   - Crie um novo recurso Azure Machine Learning com as seguintes configurações:
     - Assinatura: Sua assinatura Azure.
     - Grupo de recursos: Crie ou selecione um grupo de recursos.
     - Nome: Insira um nome único para o seu espaço de trabalho.
     - Região: Selecione a região geográfica mais próxima.
     - Conta de armazenamento: Anote a nova conta de armazenamento padrão que será criada para o seu espaço de trabalho.
     - Chave secreta: Anote o novo cofre de chaves padrão que será criado para o seu espaço de trabalho.
     - Insights da aplicação: Anote o novo recurso de insights da aplicação que será criado para o seu espaço de trabalho.
     - Registro de contêiner: Nenhum (será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).
   - Selecione Revisar + criar e, em seguida, selecione Criar. Aguarde a criação do seu espaço de trabalho (pode levar alguns minutos) e, em seguida, vá para o recurso implantado.
   - Selecione Lançar estúdio (ou abra uma nova guia do navegador e acesse https://ml.azure.com) e faça login no Azure Machine Learning studio usando sua conta Microsoft. Feche quaisquer mensagens exibidas.

2. Use o Machine Learning Automatizado para treinar um modelo:
   - No Azure Machine Learning studio, vá para a página Automated ML (em Authoring).
   - Crie um novo trabalho Automated ML com as seguintes configurações:
     - Configurações básicas:
       - Nome do trabalho: mslearn-bike-automl
       - Nome do experimento: mslearn-bike-rental
       - Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
       - Tipo de tarefa e dados:
         - Selecione o tipo de tarefa: Regressão
         - Selecione o conjunto de dados: Crie um novo conjunto de dados com as seguintes configurações:
           - Nome: bike-rentals
           - Descrição: Dados históricos de aluguel de bicicletas
           - Tipo: Tabular
           - Fonte de dados: Selecione De arquivos da web
           - URL da Web: https://aka.ms/bike-rentals
           - Formato do arquivo: Delimitado
           - Delimitador: Vírgula
           - Codificação: UTF-8
           - Cabeçalhos de coluna: Apenas o primeiro arquivo tem cabeçalhos
         - Crie o conjunto de dados.
   - Submeta o trabalho de treinamento. Ele começará automaticamente.
   - Aguarde o término do trabalho. Isso pode levar algum tempo.

3. Revise o melhor modelo:
   - Quando o trabalho de aprendizado de máquina automatizado for concluído, você pode revisar o melhor modelo treinado.
   - Na guia Visão geral do trabalho de aprendizado de máquina automatizado, observe o resumo do melhor modelo.
   - Selecione o texto abaixo do nome do algoritmo para visualizar seus detalhes.
   - Selecione a guia Métricas e selecione os gráficos de resíduos e previsão verdadeira se ainda não estiverem selecionados.
   - Revise os gráficos que mostram o desempenho do modelo.

4. Implante e teste o modelo:
   - Na guia Modelo para o melhor modelo treinado pelo seu trabalho de aprendizado de máquina automatizado, selecione Implante e use a opção Serviço da Web para implantar o modelo com as seguintes configurações:
     - Nome: prever-alugueis
     - Descrição: Prever aluguel de bicicletas
     - Tipo de computação: Instância de Contêiner do Azure
     - Habilitar autenticação: Selecionado
   - Aguarde o início da implantação. O status da implantação para o endpoint prever-alugueis será indicado na página principal como Executando.
   - Aguarde o status da implantação mudar para Concluído.

5. Teste o serviço implantado:
   - Na guia Endpoints, selecione o endpoint de tempo real prever-alugueis.
   - Na página do endpoint de tempo real prever-alugueis, visualize a guia Teste.
   - Na seção Dados de entrada para testar o endpoint, substitua o JSON modelo com os seguintes dados de entrada:

     ```json
     {
       "Inputs": { 
         "data": [
           {
             "day": 1,
             "mnth": 1,   
             "year": 2022,
             "season": 2,
             "holiday": 0,
             "weekday": 1,
             "workingday": 1,
             "weathersit": 2, 
             "temp": 0.3, 
             "atemp": 0.3,
             "hum": 0.3,
             "windspeed": 0.3 
           }
         ]    
       },   
       "GlobalParameters": 1.0
     }
     ```

   - Clique no botão Testar.
   - Revise os resultados do teste, que incluem um número previsto de aluguéis com base nas características de entrada.

6. Limpeza:
   - Exclua o serviço da Web criado para evitar o uso desnecessário do Azure.
   - Para excluir o espaço de trabalho Azure Machine Learning e os recursos associados, siga as instruções de exclusão no portal Azure.

