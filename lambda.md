### O que é o AWS Lambda?

AWS Lambda é um serviço de computação **serverless** que permite executar código sem a necessidade de provisionar ou gerenciar servidores. Ele é executado sob demanda e você só paga pelo tempo de computação consumido.

#### Lambda vs. Amazon EC2

A tabela abaixo resume as principais diferenças entre os dois serviços, um ponto fundamental para o exame:

| Característica | Amazon EC2 | AWS Lambda |
| :--- | :--- | :--- |
| **Gerenciamento de Servidores** | Requer gerenciamento (provisionamento, patching, etc.). | Não há gerenciamento de servidores. |
| **Execução** | Servidores virtuais (instâncias) em execução contínua. | Funções executadas sob demanda, apenas quando são invocadas. |
| **Tempo de Execução** | Ilimitado. | Limitado a execuções curtas (até 15 minutos). |
| **Escalabilidade** | Requer configuração de Grupos de Auto Scaling. | O dimensionamento é **automático** e gerenciado pela AWS. |
| **Modelo de Custo** | Você paga pela instância em execução (horas/segundos), mesmo que ela esteja ociosa. | Você paga por requisição e pelo tempo de computação usado (em milissegundos). |

---

### Principais Características e Benefícios

* **Pagamento por uso**: O preço é baseado no número de invocações e no tempo de execução do código, medido em milissegundos.
* **Nível Gratuito Generoso**: Oferece 1 milhão de requisições e 400.000 GB-segundos de tempo de computação gratuitos por mês.
* **Recursos Otimizados**: Aumentar a quantidade de RAM de uma função também melhora o desempenho da CPU e da rede. Você pode provisionar até 10 GB de RAM por função.
* **Suporte a Linguagens**: Suporta Node.js, Python, Java, C# (.NET), Ruby e outras linguagens através da API de runtime customizada (como Golang e Rust).
* **Monitoramento Fácil**: Totalmente integrado com o **Amazon CloudWatch** para monitoramento e visualização de logs.

---

### Integrações com Outros Serviços AWS

O AWS Lambda pode ser invocado ou interagir com uma vasta gama de serviços AWS, o que o torna a "cola" para arquiteturas serverless. As integrações mais importantes para o exame incluem:

* **Amazon S3**: Aciona uma função Lambda quando um objeto é criado, modificado ou excluído em um bucket.
* **Amazon API Gateway**: Cria uma API REST que invoca uma função Lambda.
* **Amazon DynamoDB**: Funções podem ser acionadas por eventos no banco de dados (DynamoDB Streams).
* **Amazon Kinesis**: Processa dados de streams em tempo real.
* **Amazon SNS e SQS**: Permite que o Lambda processe mensagens de tópicos e filas.
* **Amazon Cognito**: Aciona uma função em eventos de autenticação de usuário (ex: login, cadastro).
* **Amazon CloudFront**: Habilita o **Lambda@Edge**, que executa código em locais de borda da rede para personalização em tempo real.
* **Amazon CloudWatch/EventBridge**: Permite a criação de gatilhos agendados ou baseados em eventos na sua infraestrutura, como um CRON serverless.

---

### Exemplos de Casos de Uso Serverless

A aula apresentou dois exemplos práticos que são excelentes para entender a aplicação do Lambda:

1.  **Criação de Miniaturas de Imagens**:
    * Uma imagem é carregada em um bucket do S3.
    * Este evento **aciona** uma função Lambda.
    * A função redimensiona a imagem para criar uma miniatura e a armazena em outro bucket S3 e, opcionalmente, insere metadados sobre a imagem no DynamoDB.

2.  **Trabalho CRON Serverless**:
    * Uma regra agendada no **CloudWatch Events** (ou EventBridge) é configurada para disparar em um horário específico.
    * Esta regra **invoca** uma função Lambda.
    * A função executa a tarefa agendada, eliminando a necessidade de uma instância EC2 dedicada para essa finalidade.

Lembre-se: Para a prova, mesmo que o Lambda suporte a execução de containers, a preferência para executar imagens Docker deve ser sempre **Amazon ECS** ou **AWS Fargate**. O Lambda é ideal para funções de curta duração e que respondem a eventos.
