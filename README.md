# Estudo de Caso DSA - Health Insurance Dashboard

<p align="center">
  <img src="https://i.imgur.com/Acwbys2.png"/>
</p>

## Dashboard

O dashboard pode ser visualizado online e de maneira interativa clicando na imagem abaixo:

<p align="center">
<a href="https://app.powerbi.com/view?r=eyJrIjoiNWQyMjBjNWYtZjZmNS00ZmVhLWE5ZDMtMTBlNGEzNWNkODZkIiwidCI6ImMwZDAzYmU4LTdkNWUtNGVkMS04MGJkLWQxZDIwYmExNGE3MSJ9&pageName=ReportSection"><img src="https://i.imgur.com/Dbbj8Gh.jpg"></a>
</p>

## Caso

Uma operadora de plano de saúde que atende em quatro regiões do Brasil percebeu que os gastos do seguro saúde aumentaram de forma considerável e, por isso, seus diretores precisam monitorar a evolução dessas despesas.

Os dados disponíveis (e fictícios) correspondem ao ano anterior dos usuários da operadora e possuem as seguintes colunas: **Idade**, **Sexo**, **IMC (Índice de Massa Corpórea)**, se **é criança**, se **é fumante**, a **Região** do usuário e o **Valor de Seguro Saúde** de cada cliente.

Os diretores fizeram diversas perguntas e gostariam de poder visualizar as respostas em uma única tela ou visualização.

Tais questionamentos que necessitam de respostas são:

1. Qual o gasto total da operadora?
2. Qual a idade média dos usuários da operadora?
3. Qual o gasto médio por região?
4. Qual faixa etária possui maior gasto com seguro saúde por região?
5. Crianças tem gasto maior que adultos?
6. Qual a proporção de crianças por região?
7. O aumento da idade influencia no IMC?
8. Quem tem maior gasto, homens ou mulheres?
9. Se o usuário for mulher, o IMC é acima ou abaixo da média?
10. Se for homem, com mais de 50 anos e da região Sudeste, o gasto é maior ou menor que a média de gastos da região?

Os dados fornecidos contêm "problemas", erros que foram propositalmente inseridos no dataset, simulando divergências do mundo real.
A proposta é, além de criar os gráficos e atender às solicitações dos diretores, detectar tais problemas e executar um Data Cleansing, assim como interpretar corretamente o estudo de caso e decidir como resolver os equívocos.

## Análise e Resolução

O estudo de caso consistiu em, basicamente, duas etapas: limpeza, tratamento e organização de dados e a criação do dashboard onde os questionamentos dos diretores foram respondidos.
A seguir, o passo a passo para as execuções de cada etapa foram descritas.

### Limpeza, tratamento e organização dos dados

Os <a href="https://github.com/hidekishimoto/health-insurance-dashboard/blob/main/data/seguro_saude.csv">dados</a> contêm, no total, 1340 linhas.
No primeiro momento, é possível logo identificar que os nomes das colunas não estão de acordo com as informações do caso, assim como as duas primeiras linhas estão repetidas e não representam dados válidos.

Ao abrir o **Power Query**, foi utilizada a opção _Usar a Primeira Linha como Cabeçalho_, resolvendo o problema dos nomes das colunas.
Em seguida, a opção _Remover Linhas Principais_ foi selecionada para excluir a linha que antes estava repetida.

<p align="center">
  <img src="https://i.imgur.com/5X7DVQL.png"/>
</p>

Após o primeiro tratamento, o filtro foi utilizado em cada coluna para averiguar se existiam dados inconsistentes, o que provou-se real em diversas colunas.
Eram elas: **Sexo**, **Fumante** e **Região**.
Valores numéricos onde não deveriam estar e valores em branco foram detectados.

Essas sujeiras encontradas nos dados foram removidas com a opção _Remover Linhas Alternadas_.

Após o Data Cleansing, o dataset encontrava-se com 1332 linhas.

<p align="center">
  <img src="https://i.imgur.com/Leis3Xy.jpg"/>
</p>

O próximo passo foi a organização dos dados, onde cada palavra foi devidamente acentuada e suas primeiras letras tornaram-se maiúsculas, a fim de deixar o relatório final mais legível.

Outro ponto a ser corrigido foram os tipos de variável de algumas colunas que estavam como _Texto_ e foram convertidas em _Número Inteiro_ ou _Número Decimal_.
As colunas que sofreram mudanças de tipo de variável foram: **Idade** (número inteiro), **IMC** (número decimal) e **Valor Seguro Saúde** (número decimal).

<p align="center">
  <img src="https://i.imgur.com/vWKpzF7.png"/>
</p>

Por fim, dois grupos de dados e duas medidas foram criadas com o intuito de auxiliar na criação dos gráficos.

Os grupos de dados foram criados a partir da opção _Novos grupos de dados_ no formato de _Lista_ utilizando a coluna **Idade** como referência.
Assim, as duas novas colunas chamadas **Faixa Etária** e **Meia Idade** foram preenchidas com informações que separavam os clientes da seguradora em grupos por faixa etária além de mais dois grupos de maior ou menor de 50 anos.

Depois, com a opção _Nova medida_, as duas medidas **Média Idade** e **Média IMC** foram adicionadas ao dataset utilizando a fórmula _AVERAGE_ do **Power Query**, trazendo as médias, respectivamente, da **Idade** e do **IMC** dos usuários do plano de saúde.

<p align="center">
  <img src="https://i.imgur.com/oOAs9GJ.png"/>
</p>

### Dashboard e informações solicitadas pela área de negócios

#### 1. Qual o gasto total da operadora?

<p align="center">
  <img src="https://i.imgur.com/uHkJFyd.png"/>
</p>

O gasto total da operadora foi de, aproximadamente, 17.7 milhões.

Foi utilizada a visualização do ***Cartão*** contendo a _Soma_ total do **Valor Seguro Saúde** do dataset.

---

#### 2. Qual a idade média dos usuários da operadora?

<p align="center">
  <img src="https://i.imgur.com/UoDt6uP.png"/>
</p>

A idade média dos usuários da operadora é de 39 anos de idade.

O ***Cartão*** foi novamente usado, onde foi utilizada a medida **Média Idade** para apresentar o resultado.

---

#### 3. Qual o gasto médio por região?

<p align="center">
  <img src="https://i.imgur.com/HUuoJ6L.png"/>
</p>

O ***Gráfico de barras clusterizado na horizontal*** demonstra que o valor gasto médio por região variou entre 12 mil e 15 mil.

A coluna **Região** foi colocada no Eixo do gráfico, enquanto o cálculo da média do **Valor Seguro Saúde** trouxe os valores para se criar a visualização.

---

#### 4. Qual faixa etária possui maior gasto com seguro saúde por região?

<p align="center">
  <img src="https://i.imgur.com/qT5GF0r.png"/>
</p>

Analisando o ***Gráfico de barras clusterizado na vertical***, percebe-se que os clientes da faixa etária dos 50 a 59 anos são os que mais gastam com o seguro saúde em praticamente todas as regiões, salvo o Sudeste, que são as pessoas entre 18 a 29 anos.

O grupo de dados **Faixa Etária** foi utilizado como parâmetro no Eixo do gráfico, a **Região** na Legenda e o **Valor Seguro Saúde** no campo de Valores.


---

#### 5. Crianças tem gasto maior que adultos?

Após análise dos dados e do caso, conclui-se que ***é impossível responder a esta pergunta***.
Isto se deve ao fato de que, relendo o tópico do estudo de caso, afirma-se lá que a coluna **Criança** indica se os usuários **_são_ ou _não são_ crianças**, o que não condiz com os dados fornecidos pelo dataset.

Ao observar a imagem abaixo, a coluna **Criança** traz valores numéricos de 0 a 5, o que nos faz levar a entender que _provavelmente_ esse seria o número de _filhos_ que cada cliente tem, mas ainda assim é uma suposição que exige cautela ao ser feita.
Outro ponto crucial é que, ao utilizar-se um filtro e colocar a coluna **Idade** em ordem crescente, vê-se que todas as pessoas são maiores de 18 anos, salientando ainda mais o fato de que a coluna **Criança** não representa se elas são ou não crianças.

<p align="center">
  <img src="https://i.imgur.com/YO0xUkN.png"/>
</p>

Com essas evidências, ***não é possível calcular se as crianças tem gasto maior ou não que os adultos***.

Uma solução plausível seria entrar em contato com a área de negócio e explicar a situação, solicitando maiores detalhes sobre os dados referentes à coluna em questão.

---

#### 6 Qual a proporção de criança por região?

Assim como na questão 5, ***não há como responder qual a proporção de crianças por região***.

Para que fosse possível fazer essa análise, o dataset deveria fornecer o número de crianças que utilizam o seguro saúde.
Sem esses dados, fica impraticável trazer uma solução confiável e íntegra à área de negócios.

---

#### 7. O aumento da idade influencia no IMC?

<p align="center">
  <img src="https://i.imgur.com/k8Somjt.png"/>
</p>

Através da _Linha de Tendência_ gerada a partir da leitura dos dados do ***Gráfico de dispersão***, é possível reparar uma leve inclinação indicando que há sim, de fato, uma relação entre o aumento da idade e o aumento de IMC.

O Eixo X comporta os dados da **Idade**, enquanto o Eixo Y, os do **IMC**. No entanto, para atingir a visualização desejada, é necessário selecionar a opção _Não resumir_ para que não seja feito nenhum cálculo ou contagem com os dados.

---

#### 8. Quem tem maior gasto, homens ou mulheres?

<p align="center">
  <img src="https://i.imgur.com/TgKtfX6.png"/>
</p>

Esse questionamento é facilmente respondido com o ***Gráfico de pizza***, onde as informações de **Sexo** ficam na Legenda, e o **Valor Seguro Saúde** nos Valores.

Com os rótulos, conclui-se que os homens são aqueles que mais gastam com o plano de saúde, sendo em sua totalidade 53.34% dos usuários.

---

#### 9. Se o usuário for mulher, o IMC é acima ou abaixo da média?

<p align="center">
  <img src="https://i.imgur.com/5PtNof6.png"/>
</p>

Foram utilizadas duas ferramentas de visualização para fornecer essa solução.

Primeiramente, a medida **Média IMC** calculada é usada em conjunto com o ***Cartão*** para estabelecer a média de IMC de todos os usuários, totalizando 30.64.
Após isso, a ***Tabela*** é preenchida com os dados de **Sexo** e depois pela mesma medida usada anteriormente, possibilitando a separação das médias de IMC para cada sexo.

Dessa maneira, fica evidente que caso o usuário seja mulher, geralmente, o IMC será abaixo da média daqueles que são clientes da seguradora.

---

#### 10. Se for homem, com mais de 50 anos e da região Sudeste, o gasto é maior ou menor que a média de gastos da região?

<p align="center">
  <img src="https://i.imgur.com/ghCaLoG.png"/>
</p>

A utilização de filtros nos dashboards são facilitadores para que os usuários possam encontrar as informações que querem de maneira mais específica e mais rápida.
Por conta disso, a ferramenta ***Segmentação de Dados*** foi adotada para resolver essa questão.

Com a adição de três filtros distintos, um para **Sexo**, um para **Região** e outro para **Meia Idade**, os gráficos interagem entre si e mostram, com maiores detalhes, qual a média de capital gasto por homens da região Sudeste e que estão acima dos 50 anos de idade no já demonstrado ***Gráfico de barras clusterizado na horizontal***.
O grupo de dados **Meia Idade** foi usado com o intuito de auxiliar essa segmentação.

Para que a comparação seja feita de uma melhor maneira, uma ***Tabela*** foi adicionada com as informações de média de valor do seguro saúde por região e ela **não interage com os filtros**, isto é, ela não sofre alterações quando a filtragem ocorre e, por isso, seus valores permanecem estáticos.

Assim, é possível visualizar que os homens com mais de 50 anos e da região Sudeste gastam bem mais do seguro saúde.

---

#### Extra. Qual a média de valor gasta por faixa etária e considerando se a pessoa é fumante ou não?

<p align="center">
  <img src="https://i.imgur.com/OqKcVY0.png"/>
</p>

O estudo de caso desenvolvido pela Data Science Academy não propôs nenhuma atividade relacionada aos dados da coluna **Fumante**.
Por conta disso, utilizei desses recursos para criar uma atividade extra e entregar maior valor à área de negócios.

A primeira modificação na proposta do caso foi a adição de uma quarta ***Segmentação de Dados*** para filtrar todas as pessoas que são fumantes ou não, a fim de trazer mais especificidade nas consultas dos diretores.

Depois disso, adotei um ***Tornado Chart*** (que foi baixado pela Store da Microsoft) para responder a pergunta proposta.
Nele, o grupo de dados **Faixa Etária** foi colocado no campo Grupo, enquanto na Legenda foram colocados os dados da coluna **Fumante**. Por fim, o cálculo da média do **Valor Seguro Saúde** foi adicionado no campo Valores.

Com essas configurações, tornou-se possível visualizar a média de valor gasta por faixa etária considerando se a pessoa é fumante ou não.

## Conclusão

O estudo de caso trouxe uma valor inestimável para o meu aprendizado com Power BI.
Desde as técnicas de Data Cleansing até a confecção dos gráficos, esses recursos trouxeram insights inimagináveis que, com certeza, serão sempre utilizados em meus próximos projetos.

Minhas noções de aperfeiçoamento e melhoria contínua também foram muito trabalhados, uma vez que em diversos momentos encontrei pontos de melhoria e que foram executados.

O projeto também me fez estudar mais a fundo quais cores e quais gráficos funcionam melhor para quais situações, melhorando as técnicas de storytelling com dados.

Senti, no entanto, que necessito aprimorar conceitos mais avançados sobre DAX e M, assim como a confecção das visualizações.

Em suma, sinto-me orgulhoso por esse trabalho feito e gostaria de agradecer imensamente à Data Science Academy pela dedicação e conhecimento que vem passando aos alunos.