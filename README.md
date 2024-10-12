# Teste A/B/n - Taxa de Clicks no site

<div align="center">
<img src="img/teste-ab-header.jpg" />
</div>

# Introdução

Esse é um projeto end-to-end de Data Science, focado na especilização com Teste A/B. No qual identificamos qual é melhor variante do site trouxe mais clicks para o ponto específico da página, e mostramos a importância de aplicar esse tipo de teste e suas diferentes vertentes.

Os dados podem ser encontrados nesse repositório.

Esse projeto faz parte da "Comunidade DS", que é um ambiente de estudo que promove o aprendizado, execução, e discussão de projetos de Data Science.

### Plano de Desenvolvimento do Projeto de Data Science

Esse projeto foi desenvolvido seguindo o método CRISP-DS(Cross-Industry Standard Process - Data Science). Essa é uma metodologia capaz de transformar os dados da empresa em conhecimento e informações que auxiliam na tomada de decisão. A metodologia CRISP-DM define o ciclo de vida do projeto, dividindo-as nas seguintes etapas:

- Entendimento do Problema de Negócio
- Coleção dos Dados
- Limpeza de Dados
- Análise Exploratória dos Dados
- Preparação dos Dados
- Modelos de Machine Learning.
- Avaliação dos Resultados do Modelo e Tradução para Negócio.
- Modelo em Produção

![crisp!](img/crisp.png)

Observação: Como esse não é um projeto com uso de Machine Learning, os ciclos do CRISP-DM foram usados no contexto do Teste A/B/n.

### Planejamento

- [1. Descrição e Problema de Negócio](#1-descrição-e-problema-de-negócio)
- [2. Base de Dados e Premissas de Negócio](#2-base-de-dados-e-premissas-de-negócio)
- [3. Estratégia de Solução](#3-estratégia-de-solução)
- [4. Definição dos Parâmetros](#4-definição-dos-parâmetros)
- [5. Teste de Hipóteses](#5-teste-de-hipóteses)
- [6. Post Hoc Testing](#6-post-hoc-testing)
- [7. Resultados de Negócio](#7-resultados-de-negócio)
- [8. Conclusão](#8-conclusão)
- [9. Aprendizados e Trabalhos Futuros](#9-aprendizados-e-trabalhos-futuros)

# 1. Descrição e Problema de Negócio

### 1.1 Descrição

A universidade de Montada, nos Estados Unidos, possui vários serviços de apoio ao aluno, incluindo um biblioteca.

A biblioteca da universidade oferece vários serviços para os estudantes, como alocação de salas de estudos, livros, computadores, discussões em grupo, webnários e etc. Todos esses serviços e vários outros, ficam disponíveis dentro da página web da própria biblioteca e os alunos podem acessá-la para agendar algum dos serviços disponíveis.

A página possuí um banner da universidade, uma barra de busca, três principais categorias de acesso e um barra lateral direita que exibi as últimas notícias.

Durante o período de 3 de Abril de 2013 até 10 de Abril de 2013, a página “home” da biblioteca recebeu 10.819 visitantes. Ao analisar os dados de acesso da página, o time de TI da universidade percebeu uma grande diferença entre os acessos das categorias das páginas. **A taxa de click da “Find” foi de 35%, “Request” foi de 6% e “Interact” foi de 2%.**

<div align="center">
<img src="data\HomepageVersion1-Interact5-29-2013\Homepage Version 1 - Interact, 5-29-2013\Heatmap Homepage Version 1 - Interact, 5-29-2013.jpg" />
</div>

Olhando para as taxas de clicks, o time de TI se perguntou o motivo da conversão da categoria “Interact” estar tão baixa.

Uma das hipóteses do time de TI foi de que o nome “Interact” está confundindo os alunos, pois não deixa claro o propósito daquela categoria. Assim, quatro novos nomes foram propostos para substituir o nome atual da categoria: “Connect”, “Learn”, “Help” e “Service”.

<div align="center">
<img src="img/variantes.png" />
</div>

Com as variações do nome da categoria, um teste A/B/n precisa ser definido para validar qual das variações deixa a categoria mais compreensível e atraente para os estudantes, com a expectativa de aumentar a taxa de clicks nessa categoria.

Assim, um teste A/B/n foi realizado durante 3 semanas, entre os dias 29 de Maio de 2013 e 18 de Junho de 2013. O experimento foi desenhado para garantir que um usuário acessasse qualquer uma das variações com a mesma probabilidade.

### 1.2 Problema de Negócio

Você foi contratado como um freelancer pela universidade de Montana para ajudar o time de TI a avaliar os dados das variações da página home da biblioteca e dizer se alguma das variações é realmente melhor do que a atual. Em caso de resposta afirmativa, qual das variações seria a melhor e deveria substituir o nome da categoria atual. E os entregáveis são:

**- Alguma das conversão é realmente melhor do que a atual? Qual seria o nome da variação?**

# 2. Base de Dados e Premissas de Negócio

## 2.1 Base de Dados

O conjunto de dados total possui os seguintes atributos:
| **Atributos** | **Descrição** |
| ------------------- | ------------------- |
| variant | Variante do site |
| visits | Número de visitas no site |
| clicks_all | Total de ckicks na página |
| clicks_link | Total de cliques na variante |
| conversion | Proporção de cliques na variante sobre o total de clicks |

## 2.2 Premissas de Negócio

Para realizar esse projeto as seguintes premissas de negócio foram adotadas:

- A métrica de conversão que foi considerada é a quantidade de cliques na variante sobre o total de cliques no site inteiro.
- Os dados foram retirados de maneira manual para fazer o dataframe final e aplicar o Teste A/B/n.
- As hipóteses do teste serão:<br>
  **H0 - Não há nenhuma diferença entre o CTR das variantes da página**<br>
  **H1 - Há diferença entre os CTR das variantes da página**
- Depois é feito um Teste Post-Hoc onde as hipóteses são:<br>
  **H0 - Não há nenhuma diferença entre o CTR das variantes A e B da página**<br>
  **H1 - Há diferença entre o CTR das variantes A e B da página**

# 3. Estratégia de Solução

A estratégia de solução foi a seguinte:

### Passo 01. Coleta dos dados

Os dados não vieram estruturados para a aplicação do teste. Dessa forma, foi escolhido criar o dataframe com as informações de maneira manual, pegando das planilhas. Pois o principal intuito é a aplicação e entendimento do tipo do teste.

### Passo 02. Design do Experimento

Nesse momento as hipóteses foram formadas, os parâmetros foram definidos em com isso o tamanho da amostra foi encontrado.

### Passo 03. Teste de Hipóteses

A metodologia do teste de hipóteses foi aplicado, seguindo a lógica ensinado e o resultado encontrado.

### Passo 04. Teste de Post-Hoc

Após a decisão de que a hipótese nula foi rejeitada, um outro teste é aplicado com o intuito de entender qual variante de fato foi a influenciadora para esse resultado.

### Passo 05. Resultados de Negócio

Respondendo a pergunta de negócio com base nas informações tiradas através do teste e trazendo os benefícios disso para o negócio.

# PAREI AQUI

# 4. Definição dos Parâmetros

A seguir daremos definições dos parâmetros e quais valores foram usados.

## 5.1 Nível de Confiança

É a probabilidade de que o intervalo de confiança contenha o verdadeiro parâmetro da população. Nesse teste um valor padrão de **95%** foi utilizado.

## 5.2 Nível de Significância

Pode ser definido como a probabilidade de rejeitar a hipótese nula quando ela é verdadeira, denotada por α (alfa), é o inverso do nível de confiência. Nesse projeto o valor foi de **5%**

## 5.3 Tamanho do Efeito

Seria a magnitude da diferença entre grupos ou a força de uma relação entre variáveis, indicando a importância prática dos resultados. O tamanho do efeito nos diz que quando o efeito é facilmente detectável, o tamanho da amostra é menor, enquanto, quando o efeito é mínimo, é preciso de uma amostra bem maior para prová-lo.

Entretanto, isso não foi definido por quem solicitou o teste, dessa forma podemos alterar os tamanhos do efeito, com o intuito de buscar um resultado com êxito no teste de hipóteses (desde que haja amostrar o suficiente).

Assim, para definir esse valor primeiro definimos as métridas de spent e purchases, com isso, adicionamos um **lift de 1%, 5%, 10%, 15% e 20%**.

Com isso, o tamanho do efeito foi encontrado fazendo a **diferença entre o valor pós lift e antes do mesmo, sobre o desvio médio padrão do valor da população**.

## 5.4 Poder Estatístico

É probabilidade de detectar um efeito, se ele realmente existir, denotado por 1 - β (beta), onde β é a taxa de falso negativo. Nesse projeto o valor padrão de **80%** foi utilizado.

## 5.5 Tamanho da amostra

Com todos esse parâmetros encontramos o tamanho da amostra, que é a quantidade de observações ou indivíduos incluídos em um estudo ou experimento, essencial para garantir a validade e precisão dos resultados estatísticos.
Os valores foram encontrados para cada lift, e os valores que encontrarmos de conversão estarão representando toda a população, considerando um nível de confiância de 95%.

# 5. Teste de Hipóteses

A seguir daremos definições dos parâmetros e quais valores foram usados.

## 5.1 Nível de Confiança

É a probabilidade de que o intervalo de confiança contenha o verdadeiro parâmetro da população. Nesse teste um valor padrão de **95%** foi utilizado.

## 5.2 Nível de Significância

Pode ser definido como a probabilidade de rejeitar a hipótese nula quando ela é verdadeira, denotada por α (alfa), é o inverso do nível de confiência. Nesse projeto o valor foi de **5%**

## 5.3 Tamanho do Efeito

Seria a magnitude da diferença entre grupos ou a força de uma relação entre variáveis, indicando a importância prática dos resultados. O tamanho do efeito nos diz que quando o efeito é facilmente detectável, o tamanho da amostra é menor, enquanto, quando o efeito é mínimo, é preciso de uma amostra bem maior para prová-lo.

Entretanto, isso não foi definido por quem solicitou o teste, dessa forma podemos alterar os tamanhos do efeito, com o intuito de buscar um resultado com êxito no teste de hipóteses (desde que haja amostrar o suficiente).

Assim, para definir esse valor primeiro definimos as métridas de spent e purchases, com isso, adicionamos um **lift de 1%, 5%, 10%, 15% e 20%**.

Com isso, o tamanho do efeito foi encontrado fazendo a **diferença entre o valor pós lift e antes do mesmo, sobre o desvio médio padrão do valor da população**.

## 5.4 Poder Estatístico

É probabilidade de detectar um efeito, se ele realmente existir, denotado por 1 - β (beta), onde β é a taxa de falso negativo. Nesse projeto o valor padrão de **80%** foi utilizado.

## 5.5 Tamanho da amostra

Com todos esse parâmetros encontramos o tamanho da amostra, que é a quantidade de observações ou indivíduos incluídos em um estudo ou experimento, essencial para garantir a validade e precisão dos resultados estatísticos.
Os valores foram encontrados para cada lift, e os valores que encontrarmos de conversão estarão representando toda a população, considerando um nível de confiância de 95%.

# 6. Post Hoc Testing

Através da amostra encontrada, foram calculadas as médias das métricas de sucessos para cada amostra, mas apenas comparar esses resultados não é o suficiente para provar que um tipo de preenchimento é melhor que o outro.

Para isso faremos um teste de hipóteses, onde o intuito é rejeitar a hipótese nula, ou seja, que o preencimento automático tem uma média de spent ou purchases menor que a do preenchimento manual.

Assim, precisamos definir qual teste será usado, e para foi utilizado esse guia:

<div align="center">
<img src="img/Testes de Hipóteses-2.png" />
</div>

Através do diagrama utilizaremos o Two Sample t-test, para isso os teste de Parametric Assumption foram feitos.

O resultado é um p-valor, onde se o p-valor for menor que o nível de significância, a hipótese nula é rejeitada, se for maior, significa que com esses dados não é possível rejeitar a hipótese nula. Assim apresentamos o resultado para diferentes lifts e métricas de sucesso:

| **Lift** | **Spent**              | **Purchases**          |
| -------- | ---------------------- | ---------------------- |
| 1%       | Amostras insuficientes | Amostras insuficientes |
| 5%       | Falha                  | Falha                  |
| 10%      | A < B                  | Falha                  |
| 15%      | Falha                  | Falha                  |
| 20%      | Falha                  | Falha                  |

Com esse resultado, **não podemos rejeitar a hipótese nula na maioria dos testes**, com excessão ao de lift de 10%. Contudo, esse teste nos provou que a média de de valor gasto no preenchimento automático é **10% MENOR** que a do preenchimento manual.

Ou seja, a nova funcionalidade não só não superou a funcionalidade anterior, como obteve um desempenho pior na questão do valor gasto.

Como nossos dados iniciais apresentam features como país, gênero e device, podemos aprofundar a análise em cada uma delas, afim de levar não apenas o resultado final do teste, mas a conclusões um pouco mais aprofundadas.

# 7. Resultados de Negócio

Respondendo as perguntas de negócio:

**Qual a melhor forma de pagamento: Preenchimento Manual ou Automático do formulário de dados do cartão de crédito?**

Através do teste de hipóteses podemos provar que apesar de uma boa ideia, o Preenchimento Manual continua sendo a melhor forma para preencher os dados de cartão de crédito. Observamos que a média de valor gasto com compras nesse tipo de preenchiemnto é 10% maior que a média do valor gasto no preenchimento manual.

Com isso, a hipótese é que esse novo tipo de preenchimento não foi bem recebido pelos usuários, para saber exatamento o motivo seria interessante fazer um teste de usuabilidade.

Além disso, descobrimos que variáveis como gênero e device não influenciam na média de valor gasto e de compras para ambos os tipos de preenchimento.

Por fim, em alguns lugares observamos uma preferência no tipo de preenchimento, como no México, que apresentou média de valor gasto 10% maior no preenchimento automático. Em contrapartida, na França de encontram os principais ofensores so novo tipo de preenchimento, onde a média de valor gasto de de compras é 10% menor no novo método.

# 8. Conclusão

Nesse projeto, foram realizadas todas as etapas necessárias para a implementação de um projeto completo de Data Science focado na utilização do Teste A/B. Foi utilizado o método de gerenciamento de projeto chamado CRISP-DM/DS e obteve-se um desempenho satisfatório em compreender a utilização do teste A/B e aplicar em um problema real.

Tendo em vista os resultados, o projeto alcançou seu objetivo de fazer o teste e provar para a empresa de forma estatística que o nov tipo de preenchimento não foi o esperado.

# 9. Aprendizados e Trabalhos Futuros

**Aprendizados**

- Compreensão e aplicação do Teste A/B com médias.
- Conceitos estatísticos e parâmetros com teste de hipóteses.

**Trabalhos Futuros**

- Aprofundar na análise do que influencia mais na compra ao invés do preenchimento do formulário.
- Aplicar os testes nos páises com divergências maiores, segregando ainda mais, como com device e gênero.
