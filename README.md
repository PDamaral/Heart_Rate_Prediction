# Heart Rate Prediction
Analysis of IoT sensors with heart rate prediction - Capture data stream from IoT sensors that monitor the environment to predict heart rate- Supervised regression (PT-BR)

## Objetivo

Conforme proposto pela IBM :
“Em um centro de reabilitação de saúde são instalados sensores para determinar a qualidade das suas condições ambientais. É necessário ter controle da qualidade do ar e outros parâmetros relacionados ao meio ambiente, para agir rapidamente caso sejam detectadas anomalias, que podem ser muito prejudiciais aos pacientes.
Os sensores estão instalados em vários locais como: sala de espera, quartos, banheiros, refeitório, sala de atividades, escritório, jardim.
Os níveis aceitáveis de dados medidos podem variar dependendo da localização do medidor.
Também existem pulseiras que medem a frequência cardíaca, elas são colocadas em pacientes com doenças ou riscos cardíacos. O objetivo é poder controlar e realizar intervenções precoces em pacientes que possuam alterações desses valores.
No escritório, há um servidor disponível para monitoramento dos parâmetros medidos, disponibilizando os níveis dos mesmos em tempo real.’’

## Resumo do desenvolvimento

Inicialmente foi desenvolvido na nuvem da IBM uma API serverless utilizando a ferramenta Cloud Functions, na qual iria ler um json com informações de qual ambiente e dos valores dos sensores, com objetivo de enviar uma mensagem de alarme caso um ou mais sensores enviassem valores fora da faixa de medição apropriada ou saudavel.
A IBM criou um brokerMQTT com envio de stream de dados com valores medidos dos sensores, a partir disso criei um software em nodered para capturar estes valores e exportar para um arquivo .csv, onde os dados foram posteriormente tratados e organizados.
Após o tratamento, usando o jupyter notebook, a base de dados foi consumida com o objetivo de usar métodos de analise de dados e aprendizado de maquina para que se possa prever o ritmo cardíaco do paciente de acordo com os dados enviados pelos sensores. Após carregar a base no notebook, foi realizada analise exploratória dos dados de maneira univariavel e multivariável, devido a natureza dos dados nesta etapa não houve necessidade de preparações e transformações para que eles pudessem ser inseridos em modelos de aprendizado de maquina.
Os dados foram separados em conjuntos de treino e teste e aplicados a 4 modelos diferentes Regressao linear, Lasso e random forest, sendo random forest o que apresentou melhor resposta, utilizando o coeficiente de determinação (r2) como métrica de avaliação, em sequencia o modelo foi testado novamente com novos parâmetros assim realizando o ajuste fino do modelo, após colher os melhores parâmetros foi aplicada a tabela resposta e gerado o resultado final do primeiro ciclo.

## Conclusão

Por fazer parte da maratona Behind the code 2021 o tempo de desenvolvimento do projeto foi bem curto, sendo feito em apenas 3 dias, além de desenvolver o notebook como nos outros projetos, realizar a criação da API e do software em nodered se mostrou um aprendizado importante para a coleta de dados que em diversas ocasiões não poderão ser entregues em tabelas mas sim atualizados momento a momento.
Em vista do negocio, quanto maior o valor do coeficiente melhor podemos prever o ritmo cardíaco em relação aos fatores do ambiente, como temperatura e nível de CO2, assim um modelo com boa precisao pode enviar alarmes caso a tendencia da variação do ambiente seja nociva assim como não enviar caso a tendencia não tenha grande impacto no ritmo cardíaco do paciente e dos ocupantes.
