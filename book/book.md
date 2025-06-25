### CAPÍTULO

# 5

## Análise Discriminante Múltipla

## e Regressão Logística

#### Objetivos de aprendizagem

```
Ao concluir este capítulo, você deverá ser capaz de:
```
■ (^) Estabelecer as circunstâncias sob as quais a análise discriminante linear ou a regressão
logística deve ser usada no lugar de uma regressão múltipla.
■ (^) Identifi car as questões mais importantes relativas aos tipos de variáveis usadas e ao tamanho
de amostra exigido na aplicação de análise discriminante.
■ (^) Compreender as suposições inerentes à análise discriminante para avaliar a adequação de
seu uso em um problema em particular.
■ (^) Descrever as duas abordagens computacionais para a análise discriminante e o método para
avaliar o ajuste geral do modelo.
■ (^) Explicar o que é uma matriz de classifi cação e como desenvolver uma, e descrever as
maneiras de avaliar a precisão preditiva da função discriminante.
■ (^) Dizer como identifi car variáveis independentes com poder discriminatório.
■ (^) Justifi car o uso de uma abordagem de partição de amostras para validação.
■ (^) Compreender as vantagens e desvantagens da regressão logística comparada com a análise
discriminante e a regressão múltipla.
■ (^) Interpretar os resultados de uma análise de regressão logística, comparando-os com a
regressão múltipla e a análise discriminante.

#### Apresentação do capítulo

```
A regressão múltipla é sem dúvida a técnica de dependência multivariada mais amplamente empre-
gada. A base para a popularidade da regressão tem sido sua habilidade de prever e explicar variáveis
métricas. Mas o que acontece quando variáveis não-métricas tornam a regressão múltipla inadequada?
Este capítulo introduz duas técnicas – análise discriminante e regressão logística – que tratam da situa-
ção de uma variável dependente não-métrica. Neste tipo de situação, o pesquisador está interessado
na previsão e na explicação das relações que afetam a categoria na qual um objeto está localizado,
como a questão do por quê uma pessoa é um cliente ou não, ou se uma empresa terá sucesso ou fra-
cassará. Os dois maiores objetivos deste capítulo são:
```
**1.** Introduzir a natureza, a fi losofi a e as condições da análise discriminante múltipla e da regressão logís-
    tica
**2.** Demonstrar a aplicação e interpretação dessas técnicas com um exemplo ilustrativo
    O Capítulo 1 estabeleceu que o propósito básico da análise discriminante é estimar a relação entre
uma variável dependente não-métrica (categórica) e um conjunto de variáveis independentes métricas,
nesta forma geral:


##### 222 Análise Multivariada de Dados

#### Termos-chave

Antes de começar o capítulo, leia os termos-chave para com-
preender os conceitos e a terminologia empregados. Ao longo
do capítulo, os termos-chave aparecem em **negrito**. Outros
pontos que merecem destaque, além das referências cruza-
das nos termos-chave, estão em itálico. Exemplos ilustrativos
estão em quadros.

**Amostra de análise** Grupo de casos usado para estimar a(s)
função(ões) discriminante(s) ou o modelo de regressão logís-
tica. Quando se constroem matrizes de classifi cação, a amos-
tra original é dividida aleatoriamente em dois grupos, um para
estimação do modelo (a amostra de análise) e o outro para
validação (a amostra de teste).
**Abordagem de extremos polares** Método para construir uma
variável dependente categórica a partir de uma variável métri-
ca. Primeiro, a variável métrica é dividida em três categorias.
Em seguida, as categorias extremas são usadas na análise
discriminante ou na regressão logística, e a categoria do meio
não é incluída na análise.
**Amostra de teste** Grupo de objetos não usados para computar
a(s) função(ões) discriminante(s) ou o modelo de regressão
logística. Esse grupo é então usado para validar a função
discriminante ou o modelo de regressão logística em uma
amostra separada de respondentes. É também chamada de
amostra de validação.
**Amostra de validação** Ver amostra de teste.
**Análise logit** Ver regressão logística.
**Cargas discriminantes** Medida da correlação linear simples
entre cada variável independente e o escore Z discriminante
para cada função discriminante; também chamadas de corre-
lações estruturais. As cargas discriminantes são calculadas
sendo incluída uma variável independente na função discri-
minante ou não.
**Centróide** Valor médio para os escores Z discriminantes de to-
dos os objetos, em uma dada categoria ou grupo. Por exem-
plo, uma análise discriminante de dois grupos tem dois cen-
tróides, um para os objetos em cada grupo.
**Coefi ciente discriminante** Ver peso discriminante.
**Coefi ciente logístico exponenciado** Anti-logaritmo do coefi -
ciente logístico, usado para fi ns de interpretação na regres-
são logística. O coefi ciente exponenciado menos 1,0 é igual
à mudança percentual nas desigualdades. Por exemplo, um
coefi ciente exponenciado de 0,20 representa uma mudança
negativa de 80% na desigualdade (0,20 – 1,0 = – 0,80) para
cada unidade de variação na variável independente (o mes-
mo se a desigualdade fosse multiplicada por 0,20). Assim, um

```
valor de 1,0 se iguala a nenhuma mudança na desigualdade,
e valores acima de 1,0 representam aumentos na desigualda-
de prevista.
Coefi ciente logístico Coefi ciente no modelo de regressão lo-
gística que atua como o fator de ponderação para as variá-
veis independentes em relação a seu poder discriminatório.
Semelhante a um peso de regressão ou um coefi ciente dis-
criminante.
Correlações estruturais Ver cargas discriminantes.
Critério das chances proporcionais Outro critério para avaliar
a razão de sucesso, no qual a probabilidade média de clas-
sifi cação é calculada considerando-se todos os tamanhos de
grupos.
Critério de chance máxima Medida de precisão preditiva na
matriz de classifi cação que é calculada como o percentual de
respondentes no maior grupo. A idéia é que a melhor escolha
desinformada é classifi car cada observação no maior grupo.
Curva logística Uma curva em S formada pela transformação
logit que representa a probabilidade de um evento. A forma
em S é não-linear porque a probabilidade de um evento deve
se aproximar de 0 e 1, porém jamais sair destes limites. As-
sim, apesar de haver uma componente linear no meio do in-
tervalo, à medida que as probabilidades se aproximam dos
limites inferior e superior de probabilidade (0 e 1), elas devem
se amenizar e fi car assintóticas nesses limites.
Escore de corte ótimo Valor de escore Z discriminante que me-
lhor separa os grupos em cada função discriminante para fi ns
de classifi cação.
Escore de corte Critério segundo o qual cada escore Z discri-
minante individual é comparado para determinar a pertinência
prevista em um grupo. Quando a análise envolve dois grupos,
a previsão de grupo é determinada computando-se um úni-
co escore de corte. Elementos com escores Z discriminantes
abaixo dessa marca são designados a um grupo, enquanto
aqueles com escores acima são classifi cados no outro. Para
três ou mais grupos, funções discriminantes múltiplas são
usadas, com um escore de corte diferente para cada função.
Escore Z Ver escore Z discriminante.
Escore Z discriminante Escore defi nido pela função discri-
minante para cada objeto na análise e geralmente dado em
termos padronizados. Também conhecido como escore Z, é
calculado para cada objeto em cada função discriminante e
usado em conjunção com o escore de corte para determinar
pertinência prevista ao grupo. É diferente da terminologia es-
core z usada para variáveis padronizadas.
Estatística Q de Press Medida do poder classifi catório da
função discriminante quando comparada com os resultados
```
```
A análise discriminante múltipla e a regressão logística encontram amplas aplicações em situações
nas quais o objetivo principal é identifi car o grupo ao qual um objeto (p.ex., uma pessoa, uma fi rma
ou um produto) pertence. Aplicações potenciais incluem prever o sucesso ou fracasso de um novo
produto, decidir se um estudante deve ser aceito em uma faculdade, classifi car estudantes quanto a
interesses vocacionais, determinar a categoria de risco de crédito de uma pessoa, ou prever se uma
empresa terá sucesso. Em cada caso, os objetos recaem em grupos, e o objetivo é prever ou explicar
as bases para a pertinência de cada objeto a um grupo através de um conjunto de variáveis indepen-
dentes selecionadas pelo pesquisador
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 223

esperados de um modelo de chances. O valor calculado é
comparado com um valor crítico baseado na distribuição qui-
quadrado. Se o valor calculado exceder o valor crítico, os re-
sultados da classifi cação serão signifi cantemente melhores
do que se esperaria do acaso.
**Estatística Wald** Teste usado em regressão logística para a sig-
nifi cância do coefi ciente logístico. Sua interpretação é seme-
lhante aos valores F ou t usados para o teste de signifi cância
de coefi cientes de regressão.
**Estimação simultânea** Estimação da(s) função(ões) discrimi-
nante(s) ou do modelo de regressão logística em um único
passo, onde pesos para todas as variáveis independentes
são calculados simultaneamente; contrasta com a estimação
stepwise, na qual as variáveis independentes entram seqüen-
cialmente de acordo com o poder discriminante.
**Estimação stepwise** Processo de estimação de função(ões)
discriminante(s) ou do modelo de regressão logística no qual
variáveis independentes entram seqüencialmente de acordo
com o poder discriminatório que elas acrescentam à previsão
de pertinência no grupo.
**Expansão dos vetores** Vetor escalonado no qual o vetor origi-
nal é modifi cado para representar a razão F correspondente.
Usado para representar grafi camente as cargas da função
discriminante de uma maneira combinada com os centróides
de grupo.
**Função de classifi cação** Método de classifi cação no qual uma
função linear é defi nida para cada grupo. A classifi cação é
realizada calculando-se um escore para cada observação na
função de classifi cação de cada grupo e então designando-
se a observação ao grupo com o maior escore. É diferente do
cálculo do escore Z discriminante, que é calculado para cada
função discriminante.
**Função discriminante linear de Fisher** Ver função de classifi -
cação.
**Função discriminante** Uma variável estatística das variáveis
independentes selecionadas por seu poder discriminatório
usado na previsão de pertinência ao grupo. O valor previsto
da função discriminante é o escore Z discriminante, o qual é
calculado para cada objeto (pessoa, empresa ou produto) na
análise. Ele toma a forma da equação linear

```
onde
Zjk = escore Z discriminante da função discriminante j para
o objeto k
a = intercepto
Wi = peso discriminante para a variável independente i
Xik = variável independente i para o objeto k
```
**Índice potência** Medida composta do poder discriminatório de
uma variável independente quando mais de uma função dis-
criminante é estimada. Baseada em cargas discriminantes, é
uma medida relativa usada para comparar a discriminação
geral dada por conta de cada variável independente em to-
das as funções discriminantes signifi cantes.
**M de Box** Te s t e e s t a t í s t i c o p a r a a i g u a l d a d e d a s m a t r i z e s d e c o -
variância das variáveis independentes nos grupos da variável
dependente. Se a signifi cância estatística não exceder o nível

```
crítico (i.e., não-signifi cância), então a igualdade das matrizes
de covariância encontra sustentação. Se o teste mostra signi-
fi c â n c i a e s t a t í s t i c a , o s g r u p o s s ã o c o n s i d e r a d o s d i f e r e n t e s e
a suposição é violada.
Mapa territorial Representação gráfi ca dos escores de corte
em um gráfi co de duas dimensões. Quando é combinado com
os gráfi cos de casos individuais, a dispersão de cada grupo
pode ser vista e as classifi cações ruins de casos individuais
podem ser diretamente identifi cadas a partir do mapa.
Matriz de classifi cação Meio de avaliar a habilidade preditiva
da(s) função(ões) discriminante(s) ou da regressão logística
(também chamada de matriz confusão, designação ou de
previsão). Criada pela tabulação cruzada dos membros do
grupo real com os do grupo previsto, essa matriz consiste em
números na diagonal, que representam classifi cações corre-
tas, e números fora da diagonal, que representam classifi ca-
ções incorretas.
Percentual corretamente classifi cado Ver razão de sucesso.
Peso discriminante Peso cujo tamanho se relaciona ao poder
discriminatório daquela variável independente ao longo dos
grupos da variável dependente. Variáveis independentes com
grande poder discriminatório geralmente têm pesos grandes,
e as que apresentam pouco poder discriminatório geralmente
têm pesos pequenos. No entanto, a multicolinearidade entre
as variáveis independentes provoca exceções a essa regra. É
também chamado de coefi ciente discriminante.
Pseudo R^2 Um valor de ajuste geral do modelo que pode ser
calculado para regressão logística; comparável com a medi-
da R^2 usada em regressão múltipla.
Razão de desigualdade A comparação da probabilidade de
um evento acontecer com a probabilidade de o evento não
acontecer, a qual é usada como uma medida da variável de-
pendente em regressão logística.
Razão de sucesso Percentual de objetos (indivíduos, respon-
dentes, empresas etc.) corretamente classifi cados pela fun-
ção discriminante. É calculada como o número de objetos na
diagonal da matriz de classifi cação dividido pelo número total
de objetos. Também conhecida como percentual corretamen-
te classifi cado.
Regressão logística Forma especial de regressão na qual a va-
riável dependente é não-métrica, dicotômica (binária). Apesar
de algumas diferenças, a maneira geral de interpretação é
semelhante à da regressão linear.
Tolerância Proporção da variação nas variáveis independentes
não explicada pelas variáveis que já estão no modelo (função).
Pode ser usada como proteção contra a multicolinearidade.
Calculada como 1 – Ri2*, onde Ri2* é a quantia de variância da
variável independente i explicada por todas as outras variáveis
independentes. Uma tolerância de 0 signifi ca que a variável in-
dependente sob consideração é uma combinação linear per-
feita de variáveis independentes já no modelo. Uma tolerância
de 1 signifi ca que uma variável independente é totalmente in-
dependente de outras variáveis que já estão no modelo.
Transformação logit Tr a n s f o r m a ç ã o d o s v a l o re s d a v a r i á v e l
dependente binária discreta da regressão logística em uma
curva em S (curva logística) que representa a probabilidade
de um evento. Essa probabilidade é então usada para formar
```

##### 224 Análise Multivariada de Dados

a razão de desigualdade, a qual atua como a variável depen-
dente na regressão logística.
**Validação cruzada** Procedimento de divisão da amostra em
duas partes: a amostra de análise, usada na estimação da(s)
função(ões) discriminante(s) ou do modelo de regressão lo-
gística, e a amostra de teste, usada para validar os resultados.
A validação cruzada evita o super-ajuste da função discrimi-
nante ou da regressão logística, permitindo sua validação em
uma amostra totalmente separada.
**Validação por partição de amostras** Ver validação cruzada.
**Valor de verossimilhança** Medida usada em regressão logís-
tica para representar a falta de ajuste preditivo. Ainda que
esses métodos não usem o procedimento dos mínimos qua-
drados na estimação do modelo, como se faz em regressão
múltipla, o valor de verossimilhança é parecido com a soma
de erros quadrados na análise de regressão.
**Variável categórica** Ver variável não-métrica.
**Variável estatística** Combinação linear que representa a soma
ponderada de duas ou mais variáveis independentes que for-
mam a função discriminante. Também chamada de combina-
ção linear ou composta linear.
**Variável métrica** Variável com uma unidade constante de medi-
da. Se uma variável métrica tem intervalo de 1 a 9, a diferença
entre 1 e 2 é a mesma que aquela entre 8 e 9. Uma discussão
mais completa de suas características e diferenças em rela-
ção a uma variável não-métrica ou categórica é encontrada
no Capítulo 1.
**Variável não-métrica** Variável com valores que servem me-
ramente como um rótulo ou meio de identifi cação, também
conhecida como variável categórica, nominal, binária, quali-
tativa ou taxonômica. O número de um uniforme de futebol é
um exemplo. Uma discussão mais completa sobre suas ca-
racterísticas e diferenças em relação a uma variável métrica é
encontrada no Capítulo 1.
**Vetor** Representação da direção e magnitude do papel de uma
variável como retratada em uma interpretação gráfi ca de re-
sultados da análise discriminante.

#### O QUE SÃO ANÁLISE DISCRIMINANTE

#### E REGRESSÃO LOGÍSTICA?

Ao tentarmos escolher uma técnica analítica apropriada,
às vezes encontramos um problema que envolve uma va-
riável dependente categórica e várias variáveis indepen-
dentes métricas. Por exemplo, podemos querer distinguir
riscos de crédito bons de ruins. Se tivéssemos uma medida
métrica de risco de crédito, poderíamos usar a regressão
múltipla. Em muitos casos não temos a medida métrica
necessária para regressão múltipla. Ao invés disso, somos
capazes somente de verifi car se alguém está em um grupo
particular (p.ex., risco de crédito bom ou ruim).
Análise discriminante e regressão logística são as téc-
nicas estatísticas apropriadas quando a variável depen-
dente é **categórica** (nominal ou **não-métrica** ) e as **variáveis**
independentes são **métricas**. Em muitos casos, a variável

```
dependente consiste em dois grupos ou classifi cações, por
exemplo, masculino versus feminino ou alto versus bai-
xo. Em outros casos, mais de dois grupos são envolvidos,
como as classifi cações em baixo, médio e alto. A análi-
se discriminante é capaz de lidar com dois ou múltiplos
(três ou mais) grupos. Quando duas classifi cações estão
envolvidas, a técnica é chamada de análise discriminan-
te de dois grupos. Quando três ou mais classifi cações são
identifi cadas, a técnica é chamada de análise discriminante
múltipla ( MDA ). A regressão logística , também conheci-
da como análise logit , é limitada, em sua forma básica, a
dois grupos, apesar de formulações alternativas poderem
lidar com mais de dois grupos.
```
#### Análise discriminante

```
A análise discriminante envolve determinar uma variável
estatística. Uma variável estatística discriminante é a com-
binação linear das duas (ou mais) variáveis independentes
que melhor discriminarão entre os objetos (pessoas, em-
presas etc.) nos grupos defi nidos a priori. A discriminação
é conseguida estabelecendo-se os pesos da variável esta-
tística para cada variável independente para maximizar as
diferenças entre os grupos (i.e., a variância entre grupos
relativa à variância interna no grupo). A variável estatís-
tica para uma análise discriminante, também conhecida
como a função discriminante , é determinada a partir de
uma equação que se parece bastante com aquela vista em
regressão múltipla. Ela assume a seguinte forma:
Zjk! a " W 1 X 1 k " W 2 X 2 k "... " WnXnk
onde
Zjk = escore Z discriminante da função discriminante
j para o objeto k
a = intercepto
Wi = peso discriminante para a variável indepen-
dente i
Xik = variável independente i para o objeto k
Como acontece com a variável estatística em regres-
são ou qualquer outra técnica multivariada, percebemos
o escore discriminante para cada objeto na análise (pes-
soa, fi rma etc.) como sendo uma soma dos valores obtidos
pela multiplicação de cada variável independente por seu
peso discriminante. O que torna a análise discriminante
única é que mais de uma função discriminante pode estar
presente, resultando na possibilidade de que cada obje-
to possa ter mais de um escore discriminante. Discutire-
mos o que determina o número de funções discriminantes
depois, mas aqui vemos que a análise discriminante tem
semelhanças e diferenças quando comparada com outras
técnicas multivariadas.
A análise discriminante é a técnica estatística apro-
priada para testar a hipótese de que as médias de grupo
de um conjunto de variáveis independentes para dois ou
mais grupos são iguais. Calculando a média dos escores
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 225

discriminantes para todos os indivíduos em um grupo
particular, conseguimos a média do grupo. Essa média de
grupo é chamada de **centróide**. Quando a análise envolve
dois grupos, há dois centróides; com três grupos, há três
centróides, e assim por diante. Os centróides indicam o
local mais típico de qualquer indivíduo de um grupo par-
ticular, e uma comparação dos centróides de grupos mos-
tra o quão afastados estão os grupos em termos da função
discriminante.
O teste para a signifi cância estatística da função discri-
minante é uma medida generalizada da distância entre os
centróides de grupos. Ela é computada comparando-se as
distribuições dos escores discriminantes para os grupos.
Se a sobreposição nas distribuições é pequena, a função
discriminante separa bem os grupos. Se a sobreposição é
grande, a função é um discriminador pobre entre os gru-
pos. Duas distribuições de escores discriminantes mos-
tradas na Figura 5-1 ilustram melhor esse conceito. O
diagrama do alto representa as distribuições de escores
discriminantes para uma função que separa bem os gru-
pos, mostrando sobreposição mínima (a área sombreada)
entre os grupos. O diagrama abaixo exibe as distribuições
de escores discriminantes em uma função discriminan-
te que é relativamente pobre entre os grupos A e B. As
áreas sombreadas de sobreposição representam os casos
nos quais podem ocorrer classifi cação ruim de objetos do
grupo A no grupo B e vice-versa.
A análise discriminante múltipla é única em uma ca-
racterística entre as relações de dependência. Se a variável
dependente consiste de mais do que dois grupos, a análise
discriminante calcula mais de uma função discriminante.
Na verdade, calcula _NG –_ 1 funções, onde _NG_ é o número
de grupos. Cada função discriminante calcula um escore

```
discriminante Z. No caso de uma variável dependente
de três grupos, cada objeto (respondente, empresa etc.)
terá um escore separado para funções discriminantes um
e dois, permitindo que os objetos sejam representados
grafi camente em duas dimensões, com cada dimensão re-
presentando uma função discriminante. Logo, a análise
discriminante não está limitada a uma única variável esta-
tística, como ocorre na regressão múltipla, mas cria múlti-
plas variáveis estatísticas que representam dimensões de
discriminação entre os grupos.
```
#### Regressão logística

```
A regressão logística é uma forma especializada de regres-
são que é formulada para prever e explicar uma variável
categórica binária (dois grupos), e não uma medida depen-
dente métrica. A forma da variável estatística de regressão
logística é semelhante à da variável estatística da regres-
são múltipla. A variável estatística representa uma relação
multivariada com coefi cientes como os da regressão indi-
cando o impacto relativo de cada variável preditora.
As diferenças entre regressão logística e análise discri-
minante fi carão mais claras em nossa discussão posterior,
neste capítulo, sobre as características únicas da regressão
logística. Mas também existem muitas semelhanças entre
os dois métodos. Quando as suposições básicas de ambos
são atendidas, eles oferecem resultados preditivos e classi-
fi catórios comparáveis e empregam medidas diagnósticas
semelhantes. A regressão logística, porém, tem a vanta-
gem de ser menos afetada do que a análise discriminante
quando as suposições básicas, particularmente a normali-
dade das variáveis, não são satisfeitas. Ela também pode
acomodar variáveis não-métricas por meio da codifi cação
```
```
Função discriminante
```
```
Função discriminante
```
**FIGURA 5-1** Representação univariada de escores _Z_ discriminantes.


##### 226 Análise Multivariada de Dados

em variáveis dicotômicas, assim como a regressão. No en-
tanto, a regressão logística é limitada a prever apenas uma
medida dependente de dois grupos. Logo, em casos nos
quais três ou mais grupos formam a medida dependente, a
análise discriminante é mais adequada.

#### ANALOGIA COM REGRESSÃO

#### E MANOVA

A aplicação e interpretação de análise discriminante são
quase as mesmas da análise de regressão. Ou seja, a fun-
ção discriminante é uma combinação linear (variável es-
tatística) de medidas métricas para duas ou mais variáveis
independentes e é usada para descrever ou prever uma
única variável dependente. A diferença chave é que a aná-
lise discriminante é adequada a problemas de pesquisa
nos quais a variável dependente é categórica (nominal ou
não-métrica), ao passo que a regressão é usada quando a
variável dependente é métrica. Como discutido anterior-
mente, a regressão logística é uma variante da regressão,
tendo assim muitas semelhanças, exceto pelo tipo de va-
riável dependente.
A análise discriminante também é comparável à aná-
lise multivariada de variância (MANOVA) “reversa”, a
qual discutimos no Capítulo 6. Na análise discriminante,
a variável dependente é categórica e as independentes
são métricas. O oposto é verdadeiro em MANOVA, que
envolve variáveis dependentes métricas e variável(eis)
independente(s) categórica(s). As duas técnicas usam as
mesmas medidas estatísticas de ajuste geral do modelo,
como será visto a seguir neste e no próximo capítulo.

#### EXEMPLO HIPOTÉTICO DE

#### ANÁLISE DISCRIMINANTE

A análise discriminante é aplicável a qualquer questão de
pesquisa com o objetivo de entender a pertinência a gru-
pos, seja de indivíduos (p. ex., clientes versus não-clien-
tes), empresas (p. ex., lucrativas versus não-lucrativas),
produtos (p. ex., de sucesso versus sem sucesso) ou qual-
quer outro objeto que possa ser avaliado em uma série
de variáveis independentes. Para ilustrar as premissas bá-
sicas da análise discriminante, examinamos dois cenários
de pesquisa, um envolvendo dois grupos (compradores
versus não-compradores) e o outro, três grupos (níveis de
comportamento de troca). A regressão logística opera de
uma maneira comparável à da análise discriminante para
dois grupos. Logo, não ilustramos especifi camente a re-
gressão logística aqui, adiando nossa discussão até uma
consideração separada sobre a regressão logística poste-
riormente neste capítulo.

#### Uma análise discriminante de dois grupos:

#### compradores versus não-compradores

```
Suponha que a KitchenAid queira determinar se um
de seus novos produtos – um processador de alimentos
novo e aperfeiçoado – será comercialmente bem-suce-
dido. Ao levar a cabo a investigação, a KitchenAid está
interessada em identifi car (se possível) os consumidores
que comprariam o novo produto e os que não compra-
riam. Em terminologia estatística, a KitchenAid gostaria
de minimizar o número de erros que cometeria ao pre-
ver quais consumidores comprariam o novo processador
de alimentos e quais não. Para auxiliar na identifi cação
de compradores potenciais, a KitchenAid planejou es-
calas de avaliação em três características – durabilidade,
desempenho e estilo – para serem usadas por consumi-
dores para avaliar o novo produto. Em vez de confi ar em
cada escala como uma medida separada, a KitchenAid
espera que uma combinação ponderada das três preveja
melhor se um consumidor tem predisposição para com-
prar o novo produto.
```
```
A meta principal da análise discriminante é obter uma
combinação ponderada das três escalas a serem usadas
na previsão da possibilidade de um consumidor comprar
o produto. Além de determinar se os consumidores que
têm tendência para comprar o novo produto podem ser
diferenciados daqueles que não têm, a KitchenAid tam-
bém gostaria de saber quais características de seu novo
produto são úteis na diferenciação entre compradores e
não-compradores. Ou seja, avaliações de quais das três
características do novo produto melhor separam compra-
dores de não-compradores?
```
```
Por exemplo, se a resposta “eu compraria” estiver sem-
pre associada com uma medida de alta durabilidade, e a
resposta “eu não compraria” estiver sempre associada
com uma medida de baixa durabilidade, a KitchenAid
concluirá que a característica de durabilidade distingue
compradores de não-compradores. Em contrapartida,
se a KitchenAid descobrisse que tantas pessoas com
alta avaliação para estilo dissessem que comprariam o
processador quanto aquelas que não comprariam, en-
tão estilo seria uma característica que discrimina muito
mal entre compradores e não-compradores.
```
##### Identifi cação de variáveis discriminantes

```
Para identifi car variáveis que possam ser úteis na discrimina-
ção entre grupos (ou seja, compradores versus não-compra-
dores), coloca-se ênfase em diferenças de grupos em vez de
medidas de correlação usadas em regressão múltipla.
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 227

```
TABELA 5-1 Resultados do levantamento da KitchenAid para avaliação de um novo produto
Avaliação do novo produto*
Grupos baseados em
intenção de compra
```
```
X 1
Durabilidade
```
```
X 2
Desempenho
```
```
X 3
Estilo
Grupo 1: Compraria
Indivíduo 1 8 9 6
Indivíduo 2 6 7 5
Indivíduo 3 10 6 3
Indivíduo 4 9 4 4
Indivíduo 5 4 8 2
Média do grupo 7,4 6,8 4,
Grupo 2: Não compraria
Indivíduo 6 5 4 7
Indivíduo 7 3 7 2
Indivíduo 8 4 5 5
Indivíduo 9 2 4 3
Indivíduo 10 2 2 2
Média do grupo 3,2 4,4 3,
Diferença entre médias de grupos 4,2 2,4 0,
*Avaliações são feitas em uma escala de 10 pontos (de 1 = muito pobre a 10 = excelente).
```
A Tabela 5-1 lista as avaliações dessas três característi-
cas do novo processador (com um preço especifi cado)
por um painel de 10 compradores em potencial. Ao ava-
liar o processador de alimentos, cada membro do painel
estaria implicitamente comparando-o com produtos já
disponíveis no mercado. Depois que o produto foi ava-
liado, os avaliadores foram solicitados a estabelecer suas
intenções de compra (“compraria” ou “não compraria”).
Cinco disseram que comprariam o novo processador de
alimentos, e cinco disseram que não comprariam.
A Tabela 5-1 identifi ca diversas variáveis potencial-
mente discriminantes. Primeiro, uma diferença subs-
tancial separa as avaliações médias de _X_ 1 (durabilida-
de) para os grupos “compraria” e “não compraria” (7,
versus 3,2). Como tal, a durabilidade parece discriminar
bem entre os grupos e ser uma importante característica
para compradores em potencial. No entanto, a caracte-
rística de estilo ( _X_ 3 ) tem uma diferença menor, de 0,2,
entre avaliações médias (4,0 – 3,8 = 0,2) para os grupos
“compraria” e “não compraria”. Portanto, esperaríamos
que essa característica fosse menos discriminante em ter-
mos de uma decisão de compra. Contudo, antes que pos-
samos fazer tais declarações de forma conclusiva, deve-
mos examinar a distribuição de escores para cada grupo.
Desvios-padrão grandes dentro de um ou dos dois grupos
podem fazer a diferença entre médias não-signifi cantes e
inconseqüente na discriminação entre os grupos.
Como temos apenas 10 respondentes em dois grupos
e três variáveis independentes, também podemos olhar

```
os dados grafi camente para determinar o que a análi-
se discriminante está tentando conseguir. A Figura 5-
mostra os dez respondentes em cada uma das três variá-
veis. O grupo “compraria” é representado por círculos e
o grupo “não compraria”, por quadrados. Os números
de identifi cação dos respondentes estão dentro das for-
mas.
```
- _X_ 1 (Durabilidade) tem uma diferença substancial em
    escores médios, permitindo uma discriminação quase
    perfeita entre os grupos usando apenas essa variável.
    Se estabelecêssemos o valor de 5,5 como nosso ponto
    de corte para discriminar entre os dois grupos, então
    classifi caríamos incorretamente apenas o respondente 5,
    um dos membros do grupo “compraria”. Esta variável
    ilustra o poder discriminatório ao se ter uma grande
    diferença nas médias para os dois grupos e uma falta de
    superposição entre as distribuições dos dois grupos.
- _X_ 2 (Desempenho) fornece uma distinção menos clara
    entre os dois grupos. No entanto, essa variável dá ele-
    vada discriminação para o respondente 5, o qual seria
    classifi cado incorretamente se usássemos apenas _X_ 1.
    Além disso, os respondentes que seriam mal classifi ca-
    dos usando _X_ 2 estão bem separados em _X_ 1. Logo, _X_ 1 e
    _X_ 2 podem efetivamente ser usadas em combinação para
    prever a pertinência a grupo.
- _X_ 3 (Estilo) mostra pouca distinção entre os grupos. As-
    sim, formando-se uma variável estatística com apenas
    _X_ 1 e _X_ 2 e omitindo-se _X_ 3 , pode-se formar uma função
    discriminante que maximize a separação dos grupos no
    escore discriminante.


##### 228 Análise Multivariada de Dados

##### Cálculo de uma função discriminante

Com as três variáveis discriminantes potenciais identifi ca-
das, a atenção se desvia para a investigação da possibilida-
de de se usar as variáveis discriminantes em combinação
para melhorar o poder discriminatório de qualquer variá-
vel individual. Para este fi m, uma variável estatística pode
ser formada com duas ou mais variáveis discriminantes
para atuarem juntas na discriminação entre grupos.

#### Uma representação geométrica da

#### função discriminante de dois grupos

```
Uma ilustração gráfi ca de uma outra análise de dois
grupos ajudará a explicar melhor a natureza da análise
discriminante [7]. A Figura 5-3 demonstra o que acon-
tece quando uma função discriminante de dois grupos
é computada. Suponha que temos dois grupos, A e B, e
duas medidas, V 1 e V 2 , para cada membro dos dois gru-
pos. Podemos representar grafi camente em um diagrama
de dispersão a associação da variável V 1 com a variável
V 2 para cada membro dos dois grupos. Na Figura 5-3, os
```
```
Durabilidade
```
```
Estilo
```
```
Desempenho
```
**FIGURA 5-2** Representação gráfi ca de 10 compradores potenciais sobre três variáveis discriminantes possíveis.

```
A Tabela 5-2 contém os resultados para três diferentes
formulações de funções discriminantes, cada uma repre-
sentando diferentes combinações das três variáveis in-
dependentes.
```
- A primeira função discriminante contém apenas _X_ 1 ,
    igualando o valor de _X_ 1 ao escore discriminante _Z_ (tam-
    bém implicando um peso de 1,0 para _X_ 1 e pesos nulos
    para as demais variáveis). Como discutido anteriormen-
    te, o uso de apenas _X_ 1 , o melhor discriminador, resulta
    na classifi cação errônea do indivíduo 5, conforme se
    mostra na Tabela 5-2, onde quatro entre cinco indiví-
    duos do grupo 1 (todos exceto o 5) e cinco entre cinco
    indivíduos do grupo 2 estão corretamente classifi cados
    (i.e., estão na diagonal da matriz de classifi cação). O
    percentual corretamente classifi cado é, portanto, 90%
    (9 entre 10 sujeitos).
- Como _X_ 2 fornece discriminação para o sujeito 5, pode-
    mos formar uma segunda função discriminante combi-
    nando igualmente _X_ 1 e _X_ 2 (ou seja, implicando pesos de
    1,0 para _X_ 1 e _X_ 2 , e 0,0 para _X_ 3 ) para utilizar os poderes
    discriminatórios únicos de cada variável. Usando-se um
    escore de corte de 11 com essa nova função discriminan-

```
te (ver Tabela 5-2), atinge-se uma perfeita classifi cação
dos dois grupos (100% corretamente classifi cados).
Logo, X 1 e X 2 em combinação são capazes de fazer
melhores previsões de pertinência a grupos do que qual-
quer variável separadamente.
```
- A terceira função discriminante na Tabela 5-2 repre-
    senta a verdadeira função discriminante estimada ( _Z_ =
    –4,53 + 0,476 _X_ 1 + 0,359 _X_ 2 ). Usando um escore de corte
    de 0, essa terceira função também atinge uma taxa de
    classifi cações corretas de 100%, com a máxima separa-
    ção possível entre os grupos.
       Como visto neste exemplo simples, a análise discri-
minante identifi ca as variáveis com as maiores diferen-
ças entre os grupos e deriva um coefi ciente discriminante
que pondera cada variável para refl etir tais diferenças. O
resultado é uma função discriminante que melhor distin-
gue entre os grupos com base em uma combinação das
variáveis independentes.


##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 229

pontos pequenos* representam as medidas das variáveis
para os membros do grupo B, e os pontos grandes* cor-
respondem ao grupo A. As elipses desenhadas em tor-
no dos pontos pequenos e grandes envolveriam alguma
proporção pré-especifi cada dos pontos, geralmente 95%
ou mais em cada grupo. Se desenharmos uma reta pelos
dois pontos nos quais as elipses se interceptam e então
projetarmos a reta sobre um novo eixo _Z_ , podemos dizer
que a sobreposição entre as distribuições univariadas A#
e B# (representada pela área sombreada) é menor do que
se fosse obtida por qualquer outra reta através das elipses
formadas pelos diagramas de dispersão [7].
O importante a ser notado a respeito da Figura 5-3 é
que o eixo _Z_ expressa os perfi s de duas variáveis dos gru-
pos A e B como números únicos (escores discriminantes).
Encontrando uma combinação linear das variáveis origi-
nais _V_ 1 e _V_ 2 , podemos projetar os resultados como uma
função discriminante. Por exemplo, se os pontos pequenos
e grandes são projetados sobre o novo eixo _Z_ como esco-
res _Z_ discriminantes, o resultado condensa a informação
sobre diferenças de grupos (mostrada no gráfi co _V_ 1 _V_ 2 ) em
um conjunto de pontos (escores _Z_ ) sobre um único eixo,
mostrado pelas distribuições A# e B#.
Para resumir, para um dado problema de análise dis-
criminante, uma combinação linear das variáveis indepen-
dentes é determinada, resultando em uma série de escores
discriminantes para cada objeto em cada grupo. Os esco-

```
res discriminantes são computados de acordo com a regra
estatística de maximizar a variância entre os grupos e mini-
mizar a variância dentro deles. Se a variância entre os gru-
pos é grande em relação à variância dentro dos grupos, di-
zemos que a função discriminante separa bem os grupos.
```
#### Um exemplo de análise discriminante

#### de três grupos: intenções de troca

```
O exemplo de dois grupos já examinado demonstra o obje-
tivo e o benefício de se combinarem variáveis independen-
tes em uma variável estatística para fi ns de discriminação
entre grupos. A análise discriminante também tem um ou-
tro meio de discriminação – a estimação e o uso de múlti-
plas variáveis estatísticas – em casos onde há três ou mais
grupos. Essas funções discriminantes agora se tornam di-
mensões de discriminação, sendo cada dimensão separada
e diferente da outra. Assim, além de melhorar a explicação
de pertinência ao grupo, essas funções discriminantes adi-
cionais dão informação quanto às várias combinações de
variáveis independentes que discriminam entre grupos.
```
```
TABELA 5-2 Criação de funções discriminantes para prever compradores versus não-
compradores
Escores Z discriminantes calculados
```
```
Grupo
```
```
Função 1
Z! X 1
```
```
Função 2
Z! X 1 " X 2
```
```
Função 3
Z! $ 4,53 " 0,476 X 1 " 0,359 X 2
Grupo 1: Compraria
Indivíduo 1 8 17 2,
Indivíduo 2 6 13 0,
Indivíduo 3 10 16 2,
Indivíduo 4 9 13 1,
Indivíduo 5 4 12 0,
Grupo 2: Não compraria
Indivíduo 6 59 –0,
Indivíduo 7 3 10 –0,
Indivíduo 8 49 –0,
Indivíduo 9 26 –2,
Indivíduo 10 24 –2,
Escore de corte 5,5 11 0,
Precisão de classifi cação
Grupo previsto Grupo previsto Grupo previsto
Grupo real 12 12 12
1: Compraria 41 50 50
2: Não-compraria 0 5 05 05
```
```
Para ilustrar uma aplicação de análise discriminante
a três grupos, examinamos a pesquisa conduzida pela
HBAT referente à possibilidade de os clientes de um
concorrente trocarem de fornecedores. Um pré-teste em
pequena escala envolveu entrevistas de 15 clientes de um
concorrente importante. Durante as entrevistas, os clien-
tes foram indagados sobre a probabilidade de trocarem
( Continua )
```
* N. de R. T.: Na verdade, os pontos nos grupos A e B não diferem
em tamanho e, sim, no formato. No A a forma é quadrada e no B é
circular.


##### 230 Análise Multivariada de Dados

##### Identifi cação de variáveis discriminantes

Com três categorias da variável dependente, a análise
discriminante pode estimar duas funções discriminantes,
cada uma representando uma dimensão diferente de dis-
criminação.

```
A Tabela 5-3 contém os resultados da pesquisa para os
15 clientes, cinco em cada categoria da variável depen-
dente. Como fi zemos no exemplo de dois grupos, pode-
mos olhar para os escores médios de cada grupo para
ver se uma das variáveis discrimina bem entre todos os
grupos. Para X 1 , competitividade de preço, percebemos
uma grande diferença de médias entre o grupo 1 e os
grupos 2 ou 3 (2,0 versus 4,6 ou 3,8). X 1 pode discrimi-
nar bem entre o grupo 1 e os grupos 2 ou 3, mas é muito
menos efi ciente para discriminar entre os grupos 2 e 3.
Para X 2 , nível de serviço, percebemos que a diferença
entre os grupos 1 e 2 é muito pequena (2,0 versus 2,2),
ao passo que há uma grande diferença entre o grupo 3 e
os grupos 1 ou 2 (6,2 versus 2,0 ou 2,2). Logo, X 1 distin-
gue o grupo 1 dos grupos 2 e 3, e X 2 diferencia o grupo
3 dos grupos 1 e 2. Como resultado, vemos que X 1 e
X 2 fornecem diferentes “dimensões” de discriminação
entre os grupos.
```
```
Função discriminante
```
**FIGURA 5-3** Ilustração gráfi ca da análise discriminante de dois grupos.

```
de fornecedores em uma escala de três categorias. As
três respostas possíveis eram “defi nitivamente trocaria”,
“indeciso” e “defi nitivamente não trocaria”. Clientes fo-
ram designados a grupos 1, 2 ou 3, respectivamente, de
acordo com suas respostas. Os clientes também avalia-
ram o concorrente em duas características: competitivi-
dade de preço ( X 1 ) e nível de serviço ( X 2 ). A questão da
pesquisa agora é determinar se as avaliações dos clientes
a respeito do concorrente podem prever sua probabilida-
de de trocar de fornecedor. Como a variável dependente
de troca de fornecedor foi medida como uma variável ca-
tegórica (não-métrica) e as medidas de preço e serviço
são métricas, a análise discriminante é adequada.
```
```
( Continuação )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 231

##### Cálculo de duas funções discriminantes

Com as potenciais variáveis discriminantes identifi cadas,
o próximo passo é combiná-las em funções discriminantes
que utilizarão seu poder combinado de diferenciação para
separar grupos.

```
Para ilustrar grafi camente essas dimensões, a Figura 5-
retrata os três grupos em cada variável independente se-
paradamente. Vendo os membros dos grupos em qual-
quer variável, podemos perceber que nenhuma variável
discrimina bem entre todos os grupos. Mas se construí-
mos duas funções discriminantes simples, usando apenas
pesos simples de 1,0 e 0,0, os resultados se tornam mui-
to mais claros. A função discriminante 1 dá para X 1 um
peso de 1,0, e para X 2 um peso de 0,0. Do mesmo modo,
a função discriminante 2 dá para X 2 um peso de 1,0 e
para X 1 um peso de 0,0. As funções podem ser enuncia-
das matematicamente como
Função discriminante 1 = 1,0( X 1 ) + 0,0( X 2 )
Função discriminante 2 = 0,0( X 1 ) + 1,0( X 2 )
Essas equações mostram em termos simples como o
procedimento de análise discriminante estima os pesos
para maximizar a discriminação.
```
```
Com as duas funções, agora podemos calcular dois es-
cores discriminantes para cada respondente. Além disso,
as duas funções discriminantes fornecem as dimensões de
discriminação.
```
```
TABELA 5-3 Resultados da pesquisa HBAT sobre intenções de troca por clientes potenciais
Avaliação do fornecedor atual*
Grupos baseados em
intenção de troca
```
```
X 1
Competitividade de preço
```
```
X 2
Nível do serviço
Grupo 1: Defi nitivamente trocaria
Indivíduo 1 2 2
Indivíduo 2 1 2
Indivíduo 3 3 2
Indivíduo 4 2 1
Indivíduo 5 2 3
Média do grupo 2,0 2,
Grupo 2: Indeciso
Indivíduo 6 4 2
Indivíduo 7 4 3
Indivíduo 8 5 1
Indivíduo 9 5 2
Indivíduo 10 5 3
Média do grupo 4,6 2,
Grupo 3: Defi nitivamente não trocaria
Indivíduo 11 2 6
Indivíduo 12 3 6
Indivíduo 13 4 6
Indivíduo 14 5 6
Indivíduo 15 5 7
Média do grupo 3,8 6,
*Avaliações são feitas em uma escala de 10 pontos (de 1 = muito pobre a 10 = excelente).
```
```
A Figura 5-4 também contém um gráfi co de cada respon-
dente em uma representação bidimensional. A separa-
ção entre grupos agora fi ca bastante clara, e cada grupo
pode ser facilmente diferenciado. Podemos estabelecer
valores em cada dimensão que defi nirão regiões conten-
do cada grupo (p.ex., todos os membros do grupo 1 es-
tão na região menos que 3,5 na dimensão 1 e menos que
4,5 na dimensão 2). Cada um dos outros grupos pode ser
analogamente defi nido em termos das amplitudes dos
escores de suas funções discriminantes.
Em termos de dimensões de discriminação, a primei-
ra função discriminante, competitividade de preço, dife-
rencia clientes indecisos (mostrados com um quadrado)
de clientes que decidiram trocar (círculos). Mas compe-
titividade de preço não diferencia aqueles que decidiram
não trocar (losangos). Em vez disso, a percepção de ní-
vel de serviço, que defi ne a segunda função discriminan-
te, prevê se um cliente decidirá não trocar versus se um
cliente está indeciso ou determinado a trocar de forne-
( Continua )
```

##### 232 Análise Multivariada de Dados

```
A estimação de mais de uma função discriminante,
quando possível, fornece ao pesquisador uma discrimina-
ção melhorada e perspectivas adicionais sobre as caracte-
rísticas e as combinações que melhor discriminam entre os
grupos. As seções a seguir detalham os passos necessários
```
```
cedores. O pesquisador pode apresentar à gerência os
impactos separados de competitividade de preço e nível
de serviço para a tomada de decisões.
```
```
(a) variáveis individuais
```
```
Definitivamente troca
```
```
Representação
bidimensional de
funções discriminantes
```
```
Definitivamente não troca
```
```
Função
discriminante 1 = 1,0 X 1 + 0 X 2
```
```
Função
discriminante 1
```
```
Função
discriminante 2
```
```
Função
discriminante 2 = 0 X 1 + 1,0 X 2
```
```
Indeciso
```
```
Definitivamente troca
```
```
Definitivamente não troca
```
```
Indeciso
```
```
(b)
```
**FIGURA 5-4** Representação gráfi ca de variáveis discriminantes potenciais para uma análise discriminante de três grupos.

```
( Continuação )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 233

para se executar uma análise discriminante, avaliar seu ní-
vel de ajuste preditivo e então interpretar a infl uência de
variáveis independentes ao se fazer uma previsão.

#### O PROCESSO DE DECISÃO PARA

#### ANÁLISE DISCRIMINANTE

A aplicação de análise discriminante pode ser vista da
perspectiva da construção de modelo de seis estágios in-
troduzida no Capítulo 1 e retratada na Figura 5-5 (está-
gios 1-3) e na Figura 5-6 (estágios 4-6). Assim como em
todas as aplicações multivariadas, estabelecer os objetivos
é o primeiro passo na análise. Em seguida, o pesquisa-
dor deve abordar questões específi cas de planejamento e
se certifi car de que as suposições inerentes estão sendo
atendidas. A análise continua com a dedução da função
discriminante e a determinação de se uma função esta-
tisticamente signifi cante pode ser obtida para separar os
dois (ou mais) grupos. Os resultados discriminantes são
então avaliados quanto à precisão preditiva pelo desen-
volvimento de uma matriz de classifi cação. Em seguida, a
interpretação da função discriminante determina qual das
variáveis independentes mais contribui para discriminar
entre os grupos. Finalmente, a função discriminante deve
ser validada com uma amostra de teste. Cada um desses
estágios é discutido nas seções a seguir. Discutimos a re-
gressão logística em uma seção à parte depois de exami-

```
narmos o processo de decisão para a análise discriminan-
te. Desse modo, as semelhanças e diferenças entre essas
duas técnicas podem ser destacadas.
```
#### ESTÁGIO 1: OBJETIVOS DA

#### ANÁLISE DISCRIMINANTE

```
Uma revisão dos objetivos de aplicar a análise discrimi-
nante deve esclarecer melhor sua natureza. A análise dis-
criminante pode abordar qualquer um dos seguintes obje-
tivos de pesquisa:
```
**1.** Determinar se existem diferenças estatisticamente signifi -
    cantes entre os perfi s de escore médio em um conjunto de
    variáveis para dois (ou mais) grupos defi nidos _a priori_.
**2.** Determinar quais das variáveis independentes explicam o
    máximo de diferenças nos perfi s de escore médio dos dois
    ou mais grupos.
**3.** Estabelecer o número e a composição das dimensões de dis-
    criminação entre grupos formados a partir do conjunto de
    variáveis independentes.
**4.** Estabelecer procedimentos para classifi car objetos (indiví-
    duos, fi rmas, produtos e assim por diante) em grupos, com
    base em seus escores em um conjunto de variáveis indepen-
    dentes.
Como observado nesses objetivos, a análise discrimi-
nante é útil quando o pesquisador está interessado em
compreender diferenças de grupos ou em classifi car obje-

```
Estágio 1 Problema de pesquisa
```
```
Suposições
Normalidade de variáveis independentes
Linearidade de relações
Falta de multicolinearidade entre variáveis independentes
Matrizes de dispersão iguais
```
```
Questões de planejamento de pesquisa
Seleção de variáveis independentes
Considerações sobre tamanho de amostra
Criação de amostras de análise e teste
```
```
Selecione objetivo(s):
Calcule diferenças de grupo em um perfil multivariado
Classifique observações em grupos
identifique dimensões de discriminação entre grupos
```
```
Estágio 2
```
```
Estágio 3
```
```
Para
estágio
4
```
**FIGURA 5-5** Estágios 1-3 no diagrama de decisão da análise discriminante.


##### 234 Análise Multivariada de Dados

tos corretamente em grupos ou classes. Portanto, a análi-
se discriminante pode ser considerada um tipo de análise
de perfi l ou uma técnica preditiva analítica. Em qualquer
caso, a técnica é mais apropriada onde existe uma só va-
riável dependente categórica e diversas variáveis indepen-
dentes métricas.

- Como uma _análise de perfi l_ , a análise discriminante fornece
    uma avaliação objetiva de diferenças entre grupos em um
    conjunto de variáveis independentes. Nesta situação, a aná-
    lise discriminante é bastante semelhante à análise multiva-
    riada de variância (ver Capítulo 6 para uma discussão mais
    detalhada de análise multivariada de variância). Para enten-
    der as diferenças de grupos, a análise discriminante permite
    discernir o papel de variáveis individuais, bem como defi nir
    combinações dessas variáveis que representam dimensões
    de discriminação entre grupos. Essas dimensões são os efei-
    tos coletivos de diversas variáveis que trabalham conjunta-
    mente para distinguir entre os grupos. O uso de métodos de
    estimação seqüenciais também permite identifi car subcon-
    juntos de variáveis com o maior poder discriminatório.
- Para _fi ns de classifi cação_ , a análise discriminante fornece
    uma base para classifi car não somente a amostra usada para
    estimar a função discriminante, mas também quaisquer ou-
    tras observações que possam ter valores para todas as va-
    riáveis independentes. Desse modo, a análise discriminante
    pode ser usada para classifi car outras observações nos gru-
    pos defi nidos.

#### ESTÁGIO 2: PROJETO DE PESQUISA

#### PARA ANÁLISE DISCRIMINANTE

A aplicação bem-sucedida da análise discriminante requer
a consideração de várias questões. Tais questões incluem
a seleção da variável dependente e das variáveis indepen-
dentes, o tamanho necessário da amostra para a estima-
ção das funções discriminantes, e a divisão da amostra
para fi ns de validação.

#### Seleção de variáveis dependente

#### e independentes

Para aplicar a análise discriminante, o pesquisador deve
primeiramente especifi car quais variáveis devem ser inde-
pendentes e qual deve ser a medida dependente. Lembre-
se que a variável dependente é categórica e as indepen-
dentes são métricas.

##### A variável dependente

O pesquisador deve se concentrar na variável dependente
primeiro. O número de grupos (categorias) da variável de-
pendente pode ser dois ou mais, mas esses grupos devem
ser mutuamente excludentes e cobrir todos os casos. Ou
seja, cada observação pode ser colocada em apenas um
grupo. Em alguns casos, a variável dependente pode en-
volver dois grupos (dicotômicas), como bom versus ruim.
Em outros casos, a variável dependente envolve vários

```
grupos (multicotômica), como as ocupações de médico,
advogado ou professor.
```
```
Quantas categorias na variável dependente? Teorica-
mente, a análise discriminante pode lidar com um número
ilimitado de categorias na variável dependente. Na práti-
ca, porém, o pesquisador deve selecionar uma variável de-
pendente e o número de categorias com base em diversas
considerações.
```
**1.** Além de serem mutuamente excludentes e exaustivas, as
    categorias da variável dependente devem ser distintas e
    únicas no conjunto escolhido de variáveis independentes. A
    análise discriminante considera que cada grupo _deveria_ ter
    um perfi l único nas variáveis independentes usadas, e assim
    desenvolve as funções discriminantes para separar ao má-
    ximo os grupos com base nessas variáveis. Não obstante, a
    análise discriminante não tem um meio para acomodar ou
    combinar categorias que não sejam distintas nas variáveis
    independentes. Se dois ou mais grupos têm perfi s semelhan-
    tes, a análise discriminante não será capaz de estabelecer
    univocamente o perfi l de cada grupo, resultando em uma
    explicação e classifi cação mais pobres dos grupos como um
    todo. Dessa forma, o pesquisador deve escolher as variáveis
    dependentes e suas categorias para refl etir diferenças nas
    variáveis independentes. Um exemplo ajudará a ilustrar
    este ponto.

```
Imagine que o pesquisador deseja identifi car diferen-
ças entre categorias ocupacionais baseado em algumas
características demográfi cas (p.ex., renda, formação,
características familiares). Se ocupações fossem repre-
sentadas por um pequeno número de categorias (p.ex.,
pessoal de segurança e limpeza, técnicos, pessoal de es-
critório e profi ssionais de nível superior), então espera-
ríamos que houvesse diferenças únicas entre os grupos
e que a análise discriminante seria mais adequada para
desenvolver funções discriminantes que explicariam as
distinções de grupos e classifi cariam com sucesso os indi-
víduos em suas categorias corretas.
Se, porém, o número de categorias ocupacionais fos-
se aumentado, a análise discriminante poderia ter uma
difi culdade maior para identifi car diferenças. Por exem-
plo, considere que a categoria de profi ssionais de nível
superior fosse expandida para as categorias de médicos,
advogados, gerentes gerais, professores universitários e
assim por diante. A despeito de esta expansão fornecer
uma classifi cação ocupacional mais refi nada, seria muito
mais difícil fazer distinções entre essas categorias com
base em variáveis demográfi cas. Os resultados teriam
um desempenho mais pobre na análise discriminante,
tanto em termos de explicação quanto de classifi cação.
```
**2.** O pesquisador deve também buscar um número menor, e
    não maior, de categorias na medida dependente. Pode pare-
    cer mais lógico expandir o número de categorias em busca
    de mais agrupamentos únicos, mas a expansão do número


##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 235

de categorias apresenta mais complexidades nas tarefas de
classifi cação e estabelecimento de perfi l na análise discrimi-
nante. Se a análise discriminante pode estimar _NG_ – 1 (nú-
mero de grupos menos um) funções discriminantes, então o
aumento do número de grupos expande o número de pos-
síveis funções discriminantes, aumentando a complexidade
da identifi cação das dimensões inerentes de discriminação
refl etidas por conta de cada função discriminante, bem
como representando o efeito geral de cada variável inde-
pendente.
Como esses dois pontos sugerem, o pesquisador sem-
pre deve equilibrar a vontade de expandir as categorias
em favor da unicidade (exclusividade) com a crescente
efetividade de um número menor de categorias. O pesqui-
sador deve testar e selecionar uma variável dependente
com categorias que tenham as maiores diferenças entre
todos os grupos, ao mesmo tempo que mantenham supor-
te conceitual e relevância administrativa.

**Conversão de variáveis métricas** Os exemplos anteriores
de variáveis categóricas eram verdadeiras dicotomias (ou
multicotomias). Há algumas situações, contudo, em que
a análise discriminante é apropriada mesmo se a variável
dependente não é verdadeiramente categórica (não-mé-
trica). Podemos ter uma variável dependente de medida
ordinal ou intervalar, a qual queremos usar como uma
variável dependente categórica. Em tais casos, teríamos
de criar uma variável categórica, e duas abordagens estão
entre as mais usuais:

- O método mais comum é estabelecer categorias usando uma
    escala métrica. Por exemplo, se tivéssemos uma variável que
    medisse o número médio de refrigerantes consumidos por
    dia e os indivíduos respondessem em uma escala de zero a
    oito ou mais por dia, poderíamos criar uma tricotomia (três
    grupos) artifi cial simplesmente designando aqueles indiví-
    duos que consumissem nenhum, um ou dois refrigerantes
    por dia como usuários modestos, aqueles que consumissem
    três, quatro ou cinco por dia como usuários médios, e os que
    consumissem seis, sete, oito ou mais como usuários pesados.
    Tal procedimento criaria uma variável categórica de três
    grupos na qual o objetivo seria discriminar entre usuários
    de refrigerantes que fossem modestos, médios e pesados.
    Qualquer número de grupos categóricos artifi ciais pode ser
    desenvolvido. Mais freqüentemente, a abordagem envolve-
    ria a criação de duas, três ou quatro categorias. Um número
    maior de categorias poderia ser estabelecido se houvesse
    necessidade.
- Quando três ou mais categorias são criadas, surge a possi-
    bilidade de se examinarem apenas os grupos extremos em
    uma análise discriminante de dois grupos. A **abordagem de**
    **extremos polares** envolve a comparação somente dos dois
    grupos extremos e a exclusão do grupo do meio da análise
    discriminante. Por exemplo, o pesquisador poderia examinar
    os usuários modestos e pesados de refrigerantes e excluir os
    usuários médios. Esse tratamento pode ser usado toda vez
    que o pesquisador desejar olhar apenas os grupos extremos.
    Contudo, ele também pode querer tentar essa abordagem
    quando os resultados de uma análise de regressão não são

```
tão bons quanto o previsto. Tal procedimento pode ser útil
porque é possível que diferenças de grupos possam aparecer
até quando os resultados de regressão são pobres. Ou seja,
a abordagem de extremos polares com a análise discrimi-
nante pode revelar diferenças que não são tão evidentes em
uma análise de regressão do conjunto completo de dados
[7]. Tal manipulação dos dados naturalmente necessitaria
de cuidado na interpretação das descobertas.
```
##### As variáveis independentes

```
Depois de ter tomado uma decisão sobre a variável de-
pendente, o pesquisador deve decidir quais variáveis
independentes serão incluídas na análise. As variáveis
independentes geralmente são selecionadas de duas ma-
neiras. A primeira abordagem envolve a identifi cação de
variáveis a partir de pesquisa prévia ou do modelo teórico
que é a base inerente da questão de pesquisa. A segun-
da abordagem é a intuição – utilizar o conhecimento do
pesquisador e selecionar intuitivamente variáveis para as
quais não existe pesquisa prévia ou teoria, mas que logi-
camente poderiam ser relacionadas à previsão dos grupos
para a variável dependente.
Em ambos os casos, as variáveis independentes mais
apropriadas são aquelas que diferem da variável depen-
dente em pelo menos dois dos grupos. Lembre que o pro-
pósito de qualquer variável independente é apresentar um
perfi l único de pelo menos um grupo quando comparado
a outros. Variáveis que não diferem ao longo dos grupos
são de pouca utilidade em análise discriminante.
```
#### Tamanho da amostra

```
A análise discriminante, como as outras técnicas multi-
variadas, é afetada pelo tamanho da amostra sob análise.
Como discutido no Capítulo 1, amostras muito pequenas
têm grandes erros amostrais, de modo que a identifi ca-
ção de todas, exceto as grandes diferenças, é improvável.
Além disso, amostras muito grandes tornarão todas as
diferenças estatisticamente signifi cantes, ainda que essas
mesmas diferenças possam ter pouca ou nenhuma rele-
vância administrativa. Entre esses extremos, o pesquisa-
dor deve considerar o impacto do tamanho das amostras
sobre a análise discriminante, tanto no nível geral quanto
em uma base de grupo-por-grupo.
```
##### Tamanho geral da amostra

```
A primeira consideração envolve o tamanho geral da
amostra. A análise discriminante é bastante sensível à
proporção do tamanho da amostra em relação ao número
de variáveis preditoras. Como resultado, muitos estudos
sugerem uma proporção de 20 observações para cada va-
riável preditora. Apesar de essa proporção poder ser di-
fícil de manter na prática, o pesquisador deve notar que
os resultados se tornam instáveis quando o tamanho da
amostra diminui em relação ao número de variáveis inde-
pendentes. O tamanho mínimo recomendado é de cinco
```

##### 236 Análise Multivariada de Dados

observações por variável independente. Note que essa
proporção se aplica a todas as variáveis consideradas na
análise, mesmo que todas as variáveis consideradas não
entrem na função discriminante (como na estimação _ste-
pwise_ ).

##### Tamanho da amostra por categoria

Além do tamanho da amostra geral, o pesquisador tam-
bém deve considerar o tamanho da amostra de cada
categoria. No mínimo, o menor grupo de uma catego-
ria deve exceder o número de variáveis independentes.
Como uma orientação prática, cada categoria deve ter
no mínimo 20 observações. Mas mesmo que todas as
categorias excedam 20 observações, o pesquisador tam-
bém deve considerar os tamanhos relativos das mesmas.
Se os grupos variam muito em tamanho, isso pode cau-
sar impacto na estimação da função discriminante e na
classifi cação de observações. No estágio de classifi cação,
grupos maiores têm uma chance desproporcionalmente
maior de classifi cação. Se os tamanhos de grupos variam
muito, o pesquisador pode querer extrair uma amostra
aleatoriamente a partir do(s) grupo(s) maior(es), redu-
zindo assim seu(s) tamanho(s) a um nível comparável
ao(s) grupo(s) menor(es). Sempre se lembre, porém, de
manter um tamanho adequado de amostra geral e para
cada grupo.

#### Divisão da amostra

Uma observação fi nal sobre o impacto do tamanho da
amostra na análise discriminante. Como será posterior-
mente discutido no estágio 6, a maneira preferida de va-
lidar uma análise discriminante é dividir a amostra em
duas sub-amostras, uma usada para estimação da função
discriminante e outra para fi ns de validação. Em termos
de considerações sobre tamanho amostral, é essencial
que cada sub-amostra tenha tamanho adequado para su-
portar as conclusões dos resultados. Dessa forma, todas
as considerações discutidas na seção anterior se aplicam
não somente à amostra total, mas agora a cada uma das
duas sub-amostras (especialmente aquela usada para esti-
mação). Nenhuma regra rígida e rápida foi desenvolvida,
mas parece lógico que o pesquisador queira pelo menos
100 na amostra total para justifi car a divisão da mesma em
dois grupos.

##### Criação das sub-amostras

Vários procedimentos têm sido sugeridos para dividir a
amostra em sub-amostras. O procedimento usual é divi-
dir a amostra total de respondentes aleatoriamente em
dois grupos. Um deles, a **amostra de análise** , é usado para
desenvolver a função discriminante. O segundo grupo, a
**amostra de teste** , é usado para testar a função discrimi-
nante. Esse método de validação da função é chamado de
abordagem de **partição da amostra** ou **validação cruzada**
[1,5,9,18].

```
Nenhuma orientação defi nitiva foi estabelecida para
determinar os tamanhos relativos das sub-amostras de
análise e de teste (ou validação). O procedimento mais
popular é dividir a amostra total de forma que metade
dos respondentes seja colocada na amostra de análise e a
outra metade na amostra de teste. No entanto, nenhuma
regra rígida e rápida foi estabelecida, e alguns pesquisa-
dores preferem uma partição 60-40 ou mesmo 75-25 entre
os grupos de análise e de teste, dependendo do tamanho
da amostra geral.
Quando se selecionam as amostras de análise e teste,
geralmente segue-se um procedimento de amostragem
proporcionalmente estratifi cada. Assuma primeiro que
o pesquisador deseja uma divisão 50-50. Se os grupos
categóricos para a análise discriminante são igualmen-
te representados na amostra total, as amostras de esti-
mação e de teste devem ser de tamanhos aproximada-
mente iguais. Se os grupos originais são diferentes, os
tamanhos das amostras de estimação e de teste devem
ser proporcionais em relação à distribuição da amostra
total. Por exemplo, se uma amostra consiste em 50 ho-
mens e 50 mulheres, as amostras de estimação e de tes-
te teriam 25 homens e 25 mulheres cada. Se a amostra
tiver 70 mulheres e 30 homens, então as amostras de
estimação e de teste consistirão em 35 mulheres e 15
homens cada.
```
##### E se a amostra geral for muito pequena?

```
Se a amostra é muito pequena para justifi car uma divisão
em grupos de análise e de teste, o pesquisador tem duas
opções. Primeiro, desenvolver a função na amostra inteira
e então usar a função para classifi car o mesmo grupo usa-
do para desenvolver a função. Esse procedimento resulta
em um viés ascendente na precisão preditiva da função,
mas certamente é melhor do que não testar a função de
forma alguma. Segundo, diversas técnicas discutidas no
estágio 6 podem desempenhar um tipo de procedimento
de teste no qual a função discriminante é repetidamen-
te estimada sobre a amostra, cada vez reservando uma
observação diferente para previsão. Nesta abordagem,
amostras muito menores podem ser usadas, pois a amos-
tra geral não precisa ser dividida em sub-amostras.
```
#### ESTÁGIO 3: SUPOSIÇÕES DA

#### ANÁLISE DISCRIMINANTE

```
Como ocorre em todas as técnicas multivariadas, a aná-
lise discriminante é baseada em uma série de suposições.
Tais suposições se relacionam a processos estatísticos en-
volvidos nos procedimentos de estimação e classifi cação
e a questões que afetam a interpretação dos resultados.
A seção a seguir discute cada tipo de suposição e os im-
pactos sobre a aplicação apropriada da análise discrimi-
nante.
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 237

#### Impactos sobre estimação e classifi cação

As suposições-chave para determinar a função discrimi-
nante são a de normalidade multivariada das variáveis
independentes, e a de estruturas (matrizes) de dispersão
e covariância desconhecidas (mas iguais) para os grupos
como defi nidos pela variável dependente [8,10]. Existem
evidências da sensibilidade da análise discriminante a vio-
lações dessas suposições. Os testes para normalidade dis-
cutidos no Capítulo 2 estão disponíveis ao pesquisador,
juntamente com o teste **M de Box** para avaliar a simila-
ridade das matrizes de dispersão das variáveis indepen-
dentes entre os grupos. Se as suposições são violadas, o
pesquisador deve considerar métodos alternativos (p.ex.,
regressão logística, descrita na próxima seção) e com-
preender os impactos sobre os resultados que podem ser
esperados.

##### Impacto sobre estimação

Dados que não atendem a suposição de normalidade mul-
tivariada podem causar problemas na estimação da função
discriminante. Ações corretivas podem ser viáveis através
de transformações dos dados para reduzir as disparidades
entre as matrizes de covariância. No entanto, em muitos
casos essas ações corretivas são inefi cientes. Em tais casos,
os modelos devem ser diretamente validados. Se a medida
dependente é binária, a regressão logística deve ser utili-
zada sempre que possível.

##### Impacto sobre classifi cação

Matrizes de covariância desiguais também afetam negati-
vamente o processo de classifi cação. Se os tamanhos das
amostras são pequenos e as matrizes de covariância são
diferentes, então a signifi cância estatística do processo de
estimação é afetada adversamente. O caso mais comum
é o de covariâncias desiguais entre grupos de tamanho
adequado, em que as observações são super-classifi cadas
nos grupos com matrizes de covariância maiores. Esse
efeito pode ser minimizado aumentando-se o tamanho
da amostra e também usando-se as matrizes de covariân-
cia específi cas dos grupos para fi ns de classifi cação, mas
essa abordagem exige a validação cruzada dos resultados
discriminantes. Finalmente, técnicas de classifi cação qua-
dráticas estão disponíveis em muitos dos programas esta-
tísticos caso existam grandes diferenças entre as matrizes
de covariância dos grupos e as ações corretivas não mini-
mizem o efeito [6,12,14].

#### Impactos sobre interpretação

Uma outra característica dos dados que afeta os resultados
é a multicolinearidade entre as variáveis independentes.
A multicolinearidade, medida em termos de **tolerância** ,
denota que duas ou mais variáveis independentes estão
altamente correlacionadas, de modo que uma variável
pode ser altamente explicada ou prevista pela(s) outra(s)

```
variável(eis), acrescentando pouco ao poder explicativo
do conjunto como um todo. Essa consideração se torna
especialmente crítica quando procedimentos stepwise são
empregados. O pesquisador, ao interpretar a função discri-
minante, deve estar ciente da multicolinearidade e de seu
impacto na determinação de quais variáveis entram na so-
lução stepwise. Para uma discussão mais detalhada da mul-
ticolinearidade e seu impacto nas soluções stepwise , ver o
Capítulo 4. Os procedimentos para detectar a presença da
multicolinearidade são também abordados no Capítulo 4.
Como em qualquer técnica multivariada que emprega
uma variável estatística, uma suposição implícita é a de
que todas as relações são lineares. As relações não-line-
ares não são refl etidas na função discriminante, a menos
que transformações específi cas de variáveis sejam executa-
das para representarem efeitos não-lineares. Finalmente,
observações atípicas podem ter um impacto substancial na
precisão de classifi cação de quaisquer resultados da aná-
```
##### Planejamento de análise discriminante

- A variável dependente deve ser não-métrica,
    representando grupos de objetos que devem diferir nas
    variáveis independentes
- Escolha uma variável dependente que:
    - Melhor represente diferenças de grupos de interesse
    - Defi na grupos que são substancialmente distintos
    - Minimize o número de categorias ao mesmo tempo
       que atenda aos objetivos da pesquisa
- Ao converter variáveis métricas para uma escala
    não-métrica para uso como a variável dependente,
    considere o uso de grupos extremos para maximizar as
    diferenças de grupos
- Variáveis independentes devem identifi car diferenças
    entre pelo menos dois grupos para uso em análise
    discriminante
- A amostra deve ser grande o bastante para:
    - Ter pelo menos uma observação a mais por grupo
       do que o número de variáveis independentes, mas
       procurar por pelo menos 20 casos por grupo
    - Ter 20 casos por variável independente, com um
       nível mínimo recomendado de 5 observações por
       variável
    - Ter uma amostra grande o bastante para dividi-la
       em amostras de teste e de estimação, cada uma
       atendendo às exigências acima
- A suposição mais importante é a igualdade das matrizes
    de covariância, o que afeta tanto estimação quanto
    classifi cação
- Multicolinearidade entre as variáveis independentes
    pode reduzir sensivelmente o impacto estimado de
    variáveis independentes na função discriminante
    derivada, particularmente no caso de emprego de um
    processo de estimação _stepwise_

###### REGRAS PRÁTICAS 5-


##### 238 Análise Multivariada de Dados

lise discriminante. O pesquisador é encorajado a exami-
nar todos os resultados quanto à presença de observações
atípicas e a eliminar observações atípicas verdadeiras, se
necessário. Para uma discussão sobre algumas das técnicas
que avaliam as violações das suposições estatísticas básicas
ou a detecção de observações atípicas, ver Capítulo 2.

#### ESTÁGIO 4: ESTIMAÇÃO DO

#### MODELO DISCRIMINANTE E

#### AVALIAÇÃO DO AJUSTE GERAL

Para determinar a função discriminante, o pesquisador
deve decidir o método de estimação e então determinar o

```
número de funções a serem retidas (ver Figura 5-6). Com
as funções estimadas, o ajuste geral do modelo pode ser
avaliado de diversas maneiras. Primeiro, escores Z discri-
minantes , também conhecidos como os escores Z , podem
ser calculados para cada objeto. A comparação das mé-
dias dos grupos (centróides) nos escores Z fornece uma
medida de discriminação entre grupos. A precisão predi-
tiva pode ser medida como o número de observações clas-
sifi cadas nos grupos corretos, com vários critérios dispo-
níveis para avaliar se o processo de classifi cação alcança
signifi cância prática ou estatística. Finalmente, diagnósti-
cos por casos podem identifi car a precisão de classifi cação
de cada caso e seu impacto relativo sobre a estimação ge-
ral do modelo.
```
**FIGURA 5-6** Estágios 4-6 no diagrama de decisão da análise discriminante.


##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 239

#### Seleção de um método de estimação

A primeira tarefa na obtenção da função discriminante é
selecionar o método de estimação. Ao fazer tal escolha,
o pesquisador deve balancear a necessidade de controle
sobre o processo de estimação com o desejo pela parci-
mônia nas funções discriminantes. Os dois métodos dis-
poníveis são o simultâneo (direto) e o _stepwise_ , cada um
discutido adiante.

##### Estimação simultânea

A **estimação simultânea** envolve a computação da fun-
ção discriminante, de modo que todas as variáveis inde-
pendentes são consideradas juntas. Assim, a função dis-
criminante é computada com base no conjunto inteiro
de variáveis independentes, sem consideração do poder
discriminatório de cada uma delas. O método simultâ-
neo é apropriado quando, por conta de razões teóricas, o
pesquisador quer incluir todas as variáveis independen-
tes na análise e não está interessado em ver resultados
intermediários baseados apenas nas variáveis mais dis-
criminantes.

##### Estimação stepwise

A **estimação** **_stepwise_** é uma alternativa à abordagem si-
multânea. Envolve a inclusão das variáveis independentes
na função discriminante, uma por vez, com base em seu
poder discriminatório. A abordagem _stepwise_ segue um
processo seqüencial de adicionar ou descartar variáveis da
seguinte maneira:

**1.** Escolher a melhor variável discriminatória.
**2.** Comparar a variável inicial com cada uma das outras variá-
    veis independentes, uma de cada vez, e selecionar a variável
    mais adequada para melhorar o poder discriminatório da
    função em combinação com a primeira variável.
**3.** Selecionar as demais variáveis de maneira semelhante. Note
    que conforme variáveis adicionais são incluídas, algumas
    previamente escolhidas podem ser removidas se a infor-
    mação que elas contêm sobre diferenças de grupos estiver
    disponível em alguma combinação das outras variáveis in-
    cluídas em estágios posteriores.
**4.** Considerar o processo concluído quando todas as variáveis
    independentes forem incluídas na função ou as variáveis ex-
    cluídas forem julgadas como não contribuindo signifi cante-
    mente para uma discriminação futura.
O método _stepwise_ é útil quando o pesquisador quer
considerar um número relativamente grande de variáveis
independentes para inclusão na função. Selecionando-se
seqüencialmente a próxima melhor variável discriminante
em cada passo, as variáveis que não são úteis na discrimi-
nação entre os grupos são eliminadas e um conjunto re-
duzido de variáveis é identifi cado. O conjunto reduzido
geralmente é quase tão bom quanto – e às vezes melhor
que – o conjunto completo de variáveis.
    O pesquisador deve notar que a estimação _stepwise_ se
torna menos estável e generalizável à medida que a pro-
porção entre tamanho da amostra e variável independente

```
diminui abaixo do nível recomendado de 20 observações
por variável independente. É particularmente importan-
te, nesses casos, validar os resultados de tantas maneiras
quanto possível.
```
#### Signifi cância estatística

```
Após a estimação da função discriminante, o pesquisador
deve avaliar o nível de signifi cância para o poder discrimi-
natório coletivo das funções discriminantes, bem como a
signifi cância de cada função discriminante em separado. A
avaliação da signifi cância geral fornece ao pesquisador a
informação necessária para decidir se deve proceder com
a interpretação da análise ou se uma reespecifi cação se faz
necessária. Se o modelo geral for signifi cante, a avaliação
das funções individuais identifi ca aquelas que devem ser
mantidas e interpretadas.
```
##### Signifi cância geral

```
Ao se avaliar a signifi cância estatística do modelo geral,
diferentes critérios são aplicáveis para procedimentos de
estimação simultânea versus stepwise. Em ambas as situa-
ções, os testes estatísticos se relacionam com a habilidade
das funções discriminantes de obterem escores Z discri-
minantes que sejam signifi cantemente diferentes entre
grupos.
```
```
Estimação simultânea. Quando uma abordagem si-
multânea é usada, as medidas de lambda de Wilks, o
traço de Hotelling e o critério de Pillai avaliam a sig-
nificância estatística do poder discriminatório da(s)
função(ões) discriminante(s). A maior raiz característica
de Roy avalia apenas a primeira função discriminante.
Para uma discussão mais detalhada sobre as vantagens e
desvantagens de cada critério, veja a discussão de testes
de signifi cância em análise multivariada de variância no
Capítulo 6.
```
```
Estimação stepwise. Se um método stepwise é empre-
gado para estimar a função discriminante, as medidas
D^2 de Mahalanobis e V de Rao são mais adequadas.
Ambas são medidas de distância generalizada. O pro-
cedimento D^2 de Mahalanobis é baseado em distância
euclideana quadrada generalizada que se adapta a va-
riâncias desiguais. A maior vantagem deste procedi-
mento é que ele é computado no espaço original das
variáveis preditoras, em vez de ser computado como
uma versão extraída de outras medidas. O procedimen-
to D^2 de Mahalanobis se torna particularmente crítico
quando o número de variáveis preditoras aumenta por-
que ele não resulta em redução de dimensionalidade.
Uma perda em dimensionalidade causaria uma perda
de informação, porque ela diminui a variabilidade das
variáveis independentes. Em geral, D^2 de Mahalanobis
é o procedimento preferido quando o pesquisador está
interessado no uso máximo de informação disponível
em um processo stepwise.
```

##### 240 Análise Multivariada de Dados

##### Signifi cância de funções discriminantes individuais

Se o número de grupos é três ou mais, então o pesquisa-
dor deve decidir não apenas se a discriminação entre gru-
pos é estatisticamente signifi cante, mas também se cada
função discriminante estimada é estatisticamente signifi -
cante. Como discutido anteriormente, a análise discrimi-
nante estima uma função discriminante a menos do que
o número de grupos. Se três grupos são analisados, então
duas funções discriminantes serão estimadas; para quatro
grupos, três funções serão estimadas, e assim por diante.
Todos os programas de computador fornecem ao pesqui-
sador a informação necessária para verifi car o número de
funções necessárias para obter signifi cância estatística,
sem incluir funções discriminantes que não aumentam o
poder discriminatório signifi cantemente.
O critério de signifi cância convencional de 0,05 ou
acima é freqüentemente usado, sendo que alguns pesqui-
sadores estendem o nível requerido (p.ex., 0,10 ou mais)
com base na ponderação de custo versus o valor da infor-
mação. Se os maiores níveis de risco para incluir resulta-
dos não-signifi cantes (p.ex., níveis de signifi cância > 0,05)
são aceitáveis, pode-se reter funções discriminantes que
são signifi cantes no nível 0,2 ou até mesmo 0,3.
Se uma ou mais funções são consideradas estatistica-
mente não-signifi cantes, o modelo discriminante deve ser
reestimado com o número de funções a serem determi-
nadas limitado ao número de funções signifi cantes. Desse
modo, a avaliação de precisão preditiva e a interpretação
das funções discriminantes serão baseadas apenas em fun-
ções signifi cantes.

#### Avaliação do ajuste geral do modelo

Logo que as funções discriminantes signifi cantes tenham
sido identifi cadas, a atenção se desvia para a verifi cação
do ajuste geral das funções discriminantes mantidas. Essa
avaliação envolve três tarefas:

**1.** Calcular escores _Z_ discriminantes para cada observação
**2.** Calcular diferenças de grupos nos escores _Z_ discriminantes
**3.** Avaliar a precisão de previsão de pertinência a grupos.
    Devemos observar que o emprego da função discri-
minante para fi ns de classifi cação é apenas um entre dois
possíveis tratamentos. O segundo utiliza uma **função de
classifi cação** , também conhecida como **função discrimi-
nante linear de Fisher**. As funções de classifi cação, uma
para cada grupo, são usadas exclusivamente para classifi -
car observações. Nesse método de classifi cação, os valores
de uma observação para as variáveis independentes são
inseridos nas funções de classifi cação, e um escore de clas-
sifi cação para cada grupo é calculado para aquela obser-
vação. A observação é então classifi cada no grupo com o
maior escore de classifi cação.
    Examinamos a função discriminante como o meio de
classifi cação porque ela fornece uma representação conci-
sa e simples de cada função discriminante, simplifi cando
o processo de interpretação e a avaliação da contribuição
de variáveis independentes. Ambos os métodos conse-
guem resultados comparáveis, apesar de usarem diferen-
tes meios.

##### Cálculo de escores Z discriminantes

```
Com as funções discriminantes retidas defi nidas, a base
para calcular os escores Z discriminantes foi estabelecida.
Como discutido anteriormente, o escore Z discriminante
de qualquer função discriminante pode ser calculado para
cada observação pela seguinte fórmula:
Zjk! a " W 1 X 1 k " W 2 X 2 k "... " WnXnk
onde
Zjk = escore Z discriminante da função discriminante
j para o objeto k
a = intercepto
Wi = coefi ciente discriminante para a variável inde-
pendente i
Xik = variável independente i para o objeto k
Este escore, uma variável métrica, fornece uma manei-
ra direta de comparar observações em cada função. As-
sume-se que as observações com escores Z semelhantes
são mais parecidas com base nas variáveis que constituem
essa função do que aquelas com escores totalmente distin-
tos. A função discriminante pode ser expressa com pesos
e valores padronizados ou não-padronizados. A versão
padronizada é mais útil para fi ns de interpretação, mas a
não-padronizada é mais fácil de utilizar no cálculo do es-
core Z discriminante.
```
##### Avaliação de diferenças de grupos

```
Uma vez que os escores Z discriminantes são calculados,
a primeira avaliação de ajuste geral do modelo é deter-
minar a magnitude de diferenças entre os membros de
cada grupo em termos dos escores Z discriminantes. Uma
```
##### Estimação e ajuste do modelo

- Apesar de a estimação _stepwise_ poder parecer ótima ao
    selecionar o mais parcimonioso conjunto de variáveis
    maximamente discriminantes, cuidado com o impacto
    de multicolinearidade sobre a avaliação do poder
    discriminatório de cada variável.
- O ajuste geral do modelo avalia a signifi cância
    estatística entre grupos sobre os escores _Z_
    discriminantes, mas não avalia precisão preditiva.
- Tendo mais de dois grupos, não confi ne sua análise
    a apenas as funções discriminantes estatisticamente
    signifi cantes, mas considere a possibilidade de funções
    não-signifi cantes (com níveis de até 0,3) adicionarem
    poder explanatório.

###### REGRAS PRÁTICAS 5-


##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 241

medida resumo das diferenças de grupos é uma compara-
ção dos **centróides** dos grupos, o escore _Z_ discriminante
médio para todos os membros dos grupos. Uma medida
de sucesso da análise discriminante é sua habilidade em
defi nir função(ões) discriminante(s) que resulte(m) em
centróides de grupos signifi cantemente diferentes. As di-
ferenças entre centróides são medidas em termos do _D_^2
de Mahalanobis, para o qual há testes disponíveis para de-
terminar se as diferenças são estatisticamente signifi can-
tes. O pesquisador deve garantir que, mesmo com funções
discriminantes signifi cantes, há diferenças consideráveis
entre os grupos.
Os centróides de grupos em cada função discriminan-
te também podem ser representados grafi camente para
demonstrar os resultados de uma perspectiva gráfi ca.
Gráfi cos geralmente são preparados para as primeiras
duas ou três funções discriminantes (assumindo que elas
são funções estatisticamente signifi cantes). Os valores
para cada grupo mostram sua posição no espaço discri-
minante reduzido (assim chamado porque nem todas as
funções e, assim, nem toda a variância, são representa-
das grafi camente). O pesquisador pode ver as diferenças
entre os grupos em cada função; no entanto, a inspeção
visual não explica totalmente o que são essas diferenças.
Pode-se desenhar círculos que envolvam a distribuição de
observações em volta de seus respectivos centróides para
esclarecer melhor as diferenças de grupos, mas esse pro-
cedimento está além do escopo deste texto (ver Dillon e
Goldstein [4]).

##### Avaliação da precisão preditiva

##### de pertinência a grupo

Dado que a variável dependente é não-métrica, não é pos-
sível usar uma medida como _R_^2 , como se faz em regressão
múltipla, para avaliar a precisão preditiva. Em vez disso,
cada observação deve ser avaliada com o objetivo de sa-
ber se ela foi corretamente classifi cada. Ao fazer isso, di-
versas considerações importantes devem ser feitas:

- A concepção estatística e prática para desenvolver matrizes
    de classifi cação
- A determinação do escore de corte
- A construção das matrizes de classifi cação
- Os padrões para avaliar a precisão de classifi cação

**Por que matrizes de classifi cação são desenvolvidas.** Os
testes estatísticos para avaliar a signifi cância das funções
discriminantes somente avaliam o grau de diferença en-
tre os grupos com base nos escores _Z_ discriminantes,
mas não dizem quão bem a função prevê. Esses testes
estatísticos sofrem das mesmas desvantagens dos testes
de hipóteses clássicos. Por exemplo, suponha que os dois
grupos são considerados signifi cantemente diferentes
além do nível 0,01. Com amostras sufi cientemente gran-
des, as médias de grupo (centróides) poderiam ser virtu-
almente idênticas e ainda teriam signifi cância estatística.

```
Para determinar a habilidade preditiva de uma função
discriminante, o pesquisador deve construir matrizes de
classifi cação.
A matriz de classifi cação fornece uma perspectiva so-
bre signifi cância prática, e não sobre signifi cância estatís-
tica. Com a análise discriminante múltipla, o percentual
corretamente classifi cado , também conhecido como razão
de sucesso , revela o quão bem a função discriminante
classifi cou os objetos. Com uma amostra sufi cientemen-
te grande em análise discriminante, poderíamos ter uma
diferença estatisticamente signifi cante entre os dois (ou
mais) grupos e mesmo assim classifi car corretamente
apenas 53% (quando a chance é de 50%, com grupos de
mesmo tamanho) [16]. Em tais casos, o teste estatístico
indicaria signifi cância estatística, ainda que a razão de su-
cesso viabilizasse um julgamento à parte a ser feito em
termos de signifi cância prática. Logo, devemos usar o pro-
cedimento da matriz de classifi cação para avaliar precisão
preditiva além de simples signifi cância estatística.
```
```
Cálculo do escore de corte. Usando as funções discrimi-
nantes consideradas signifi cantes, podemos desenvolver
matrizes de classifi cação para uma avaliação mais preci-
sa do poder discriminatório das funções. Antes que uma
matriz de classifi cação seja defi nida, porém, o pesquisador
deve determinar o escore de corte (também chamado de
valor Z crítico) para cada função discriminante. O escore
de corte é o critério em relação ao qual o escore discrimi-
nante de cada objeto é comparado para determinar em
qual grupo o objeto deve ser classifi cado.
O escore de corte representa o ponto divisor usado
para classifi car observações em um entre dois grupos ba-
seado no escore da função discriminante. O cálculo de um
escore de corte entre dois grupos quaisquer é baseado
nos centróides de dois grupos (média de grupo dos esco-
res discriminantes) e no tamanho relativo dos grupos. Os
centróides são facilmente calculados e fornecidos em cada
estágio do processo stepwise. Para calcular corretamente
o escore de corte ótimo , o pesquisador deve abordar dois
pontos:
```
**1.** Defi nir as probabilidades _a priori_ , baseado nos tamanhos
    relativos dos grupos observados ou especifi cados pelo pes-
    quisador (ou assumidos iguais, ou com valores dados pelo
    pesquisador).
**2.** Calcular o valor do escore de corte ótimo como uma média
    ponderada sobre os tamanhos assumidos dos grupos (obti-
    do a partir das probabilidades _a priori_ ).

```
Defi nição das probabilidades a priori. O impacto
e a importância de tamanhos relativos de grupos são mui-
tas vezes desconsiderados, apesar de serem baseados nas
suposições do pesquisador relativas à representatividade
da amostra. Neste caso, representatividade se relaciona à
representação dos tamanhos relativos dos grupos na po-
pulação real, o que pode ser estabelecido como probabili-
```

##### 242 Análise Multivariada de Dados

dades _a priori_ (ou seja, a proporção relativa de cada grupo
em relação à amostra total).
A questão fundamental é: os tamanhos relativos dos
grupos são representativos dos tamanhos de grupos na
população? A suposição padrão para a maioria dos pro-
gramas estatísticos é de probabilidades iguais; em outras
palavras, cada grupo é considerado como tendo a mesma
chance de ocorrer, mesmo que os tamanhos dos grupos
na amostra sejam desiguais. Se o pesquisador está inse-
guro sobre se as proporções observadas na amostra são
representativas das proporções da população, a aborda-
gem conservadora é empregar probabilidades iguais. Em
alguns casos, estimativas das probabilidades _a priori_ po-
dem estar disponíveis, como em pesquisa anterior. Aqui a
suposição padrão de probabilidades iguais _a priori_ é subs-
tituída por valores especifi cados pelo pesquisador. Em
qualquer caso, os reais tamanhos de grupos são substituí-
dos com base nas probabilidades _a priori_ especifi cadas.
No entanto, se a amostra foi conduzida aleatoriamen-
te e o pesquisador sente que os tamanhos de grupos são
representativos da população, então o pesquisador pode
especifi car probabilidade _a priori_ com base na amostra
de estimação. Assim, os verdadeiros tamanhos de gru-
pos são considerados representativos e diretamente usa-
dos no cálculo do escore de corte (ver a discussão que
se segue). Em todos os casos, porém, o pesquisador deve
especifi car como as probabilidades _a priori_ são calcula-
das, o que afeta os tamanhos de grupos usados no cálculo
como ilustrado.

```
Por exemplo, considere uma amostra de teste consis-
tindo de 200 observações, com tamanhos de grupos de
60 a 140 que se relacionam com probabilidades a priori
de 30% e 70%, respectivamente. Se a amostra é consi-
derada representativa, então os tamanhos de 60 e 140
são empregados no cálculo do escore de corte. Não obs-
tante, se a amostra é considerada não-representativa, o
pesquisador deve especifi car as probabilidades a prio-
ri. Se elas são especifi cadas como iguais (50% e 50%),
os tamanhos amostrais de 100 e 100 seriam usados no
cálculo do escore de corte no lugar dos tamanhos reais.
Especifi car outros valores para as probabilidades a prio-
ri resultaria em diferentes tamanhos amostrais para os
dois grupos.
```
**_Cálculo do escore de corte ótimo._** A importância
das probabilidades _a priori_ no escore de corte é muito evi-
dente depois que se percebe como o mesmo é calculado.
A fórmula básica para computar o escore de corte entre
dois grupos quaisquer é:

```
onde
ZCS = escore de corte ótimo entre grupos A e B
NA = número de observações no grupo A
NB = número de observações no grupo B
ZA = centróide para o grupo A
ZB = centróide para o grupo B
Com tamanhos desiguais de grupos, o escore de cor-
te ótimo para uma função discriminante é agora a média
ponderada dos centróides de grupos. O escore de corte
é ponderado na direção do grupo menor, gerando, com
sorte, uma melhor classifi cação do grupo maior.
Se os grupos são especifi cados como sendo de iguais
tamanhos (probabilidades a priori defi nidas como iguais),
então o escore de corte ótimo estará a meio caminho en-
tre os dois centróides e se torna simplesmente a média dos
mesmos:
```
```
onde
ZCE = valor do escore de corte crítico para grupos de
mesmo tamanho
ZA = centróide do grupo A
ZB = centróide do grupo B
Ambas as fórmulas para cálculo do escore de corte óti-
mo assumem que as distribuições são normais e as estru-
turas de dispersão de grupos são conhecidas.
```
```
O conceito de um escore de corte ótimo para grupos
iguais e distintos é ilustrado nas Figuras 5-7 e 5-8, res-
pectivamente. Os escores de corte ponderados e não-
ponderados são mostrados. Fica evidente que se o grupo
A é muito menor que o grupo B, o escore de corte ótimo
está mais próximo ao centróide do grupo A do que ao
centróide do grupo B. Além disso, se o escore de corte
não-ponderado fosse usado, nenhum dos objetos no gru-
po A seria mal classifi cado, mas uma parte substancial
dos que estão no grupo B seria mal classifi cada.
```
```
Custos de má classifi cação. O escore de corte ótimo
também deve considerar o custo de classifi car um obje-
to no grupo errado. Se os custos de má classifi cação são
aproximadamente iguais para todos os grupos, o escore
de corte ótimo será aquele que classifi car mal o menor nú-
mero de objetos em todos os grupos. Se os custos de má
classifi cação são desiguais, o escore de corte ótimo será o
que minimizar os custos de má classifi cação. Abordagens
mais sofi sticadas para determinar escores de corte são dis-
cutidas em Dillon e Goldstein [4] e Huberty et al. [13].
Essas abordagens são baseadas em um modelo estatístico
bayesiano e são adequadas quando os custos de má classi-
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 243

fi cação em certos grupos são altos, quando os grupos são
de tamanhos muito diferentes, ou quando se deseja tirar
vantagem de um conhecimento _a priori_ de probabilidades
de pertinência a grupo.
Na prática, quando se calcula o escore de corte, ge-
ralmente não é necessário inserir as medidas originais da
variável para cada indivíduo na função discriminante e
obter o escore discriminante para cada pessoa para usar
no cálculo de _Z_ A e _Z_ B (centróides dos grupos A e B). O
programa de computador fornece os escores discriminan-
tes, bem como _Z_ A e _Z_ B, como _output_ regular. Quando o
pesquisador tem os centróides de grupo e os tamanhos da
amostra, o escore de corte ótimo pode ser obtido simples-
mente substituindo-se os valores na fórmula apropriada.

**Construção das matrizes de classifi cação.** Para validar a
função discriminante pelo uso de matrizes de classifi cação,
a amostra deve ser aleatoriamente dividida em dois gru-
pos. Um dos grupos (a amostra de análise) é usado para
computar a função discriminante. O outro (a amostra de
teste ou de validação) é retido para uso no desenvolvi-
mento da matriz de classifi cação. O procedimento envolve
a multiplicação dos pesos gerados pela amostra de análise

```
pelas medidas originais da variável da amostra de teste.
Em seguida, os escores discriminantes individuais para a
amostra de teste são comparados com o valor do escore
de corte crítico e classifi cados como se segue:
Classifi que um indivíduo no grupo A se Zn < Zct
ou
Classifi que um indivíduo no grupo B se Zn > Zct.
onde
Zn = escore Z discriminante para o n -ésimo indivíduo
Zct = valor do escore de corte crítico
Os resultados do procedimento de classifi cação são
apresentados em forma matricial, como mostrado na Ta-
bela 5-4. As entradas na diagonal da matriz representam o
número de indivíduos corretamente classifi cados. Os nú-
meros fora da diagonal representam as classifi cações in-
corretas. As entradas sob a coluna rotulada de “Tamanho
do grupo real” representam o número de indivíduos que
realmente estão em cada um dos dois grupos. As entradas
na base das colunas representam o número de indivíduos
designados aos grupos pela função discriminante. O per-
```
```
Escore de corte = Z CE
```
```
Classifique como A
(Não-comprador)
```
```
Classifique como B
(Comprador)
```
```
Grupo A Grupo B
```
**FIGURA 5-7** Escore de corte ótimo com amostras de tamanhos iguais.

```
Escore de corte
não-ponderado
```
```
Escore de corte
ótimo ponderado
```
```
Grupo A
```
```
Grupo B
```
**FIGURA 5-8** Escore de corte ótimo com tamanhos desiguais de amostras.


##### 244 Análise Multivariada de Dados

centual corretamente classifi cado para cada grupo é mos-
trado no lado direito da matriz, e o percentual geral corre-
tamente classifi cado, também conhecido como a razão de
sucesso, é mostrado na base.

```
Em nosso exemplo, o número de indivíduos correta-
mente designados ao grupo 1 é 22, enquanto 3 mem-
bros do grupo 1 estão incorretamente designados ao
grupo 2. Do mesmo modo, o número de classifi cações
corretas no grupo 2 é 20, e o número de designações
incorretas no grupo 1 é 5. Assim, os percentuais de
precisão de classifi cação da função discriminante para
os grupos reais 1 e 2 são 88% e 80%, respectivamente.
A precisão de classifi cação geral (razão de sucesso) é
84%.
```
Um tópico fi nal sobre os procedimentos de classifi -
cação é o teste _t_ disponível para determinar o nível de
signifi cância para a precisão de classifi cação. A fórmu-
la para uma análise de dois grupos (igual tamanho de
amostra) é

onde

_p =_ proporção corretamente classifi cada
_N =_ tamanho da amostra
Essa fórmula pode ser adaptada para uso com mais
grupos e diferentes tamanhos de amostra.

**Estabelecimento de padrões de comparação para a razão
de sucesso.** Como observado anteriormente, a precisão
preditiva da função discriminante é medida pela razão
de sucesso, a qual é obtida a partir da matriz de classi-
fi cação. O pesquisador pode questionar o que é ou não
considerado um nível aceitável de precisão preditiva para
uma função discriminante. Por exemplo, 60% é um nível
aceitável ou deveríamos esperar obter de 80% a 90% de
precisão preditiva? Para responder essa questão o pesqui-

```
sador deve primeiro determinar o percentual que poderia
ser classifi cado corretamente por chances ( sem a ajuda da
função discriminante ).
```
```
Padrões de comparação para a razão de sucesso em
grupos de mesmo tamanho. Quando os tamanhos de
amostra dos grupos são iguais, a determinação da classifi -
cação por chances é bem simples; ela é obtida dividindo-
se 1 pelo número de grupos. A fórmula é
C IGUAL = 1/(Número de grupos).
Por exemplo, para uma função de dois grupos, a pro-
babilidade seria de 0,50; para uma função de três grupos,
seria de 0,33, e assim por diante.
```
```
Padrões de comparação para a razão de sucesso em
grupos de tamanhos desiguais. A determinação da
classifi cação por chances para situações nas quais os ta-
manhos dos grupos são desiguais é um pouco mais com-
plicada. Devemos considerar apenas o maior grupo, a
probabilidade combinada de todos os tamanhos de gru-
pos, ou algum outro padrão? Imaginemos que temos uma
amostra total de 200 indivíduos divididos como amostras
de teste e de análise de 100 observações cada. Na amostra
de teste, 75 objetos pertencem a um grupo e 25 ao outro.
Examinaremos os possíveis caminhos nos quais podemos
construir um padrão para comparação e aquilo que cada
um representa.
```
- Conhecido como o **critério de chance máxima** , poderíamos
    arbitrariamente designar todos os indivíduos ao maior gru-
    po. O critério da chance máxima deve ser usado quando
    o único objetivo da análise discriminante é maximizar o
    percentual corretamente classifi cado [16]. É também o pa-
    drão mais conservador, pois ele gera o mais alto padrão de
    comparação. No entanto, são raras as situações nas quais
    estamos interessados apenas em maximizar o percentual
    corretamente classifi cado. Geralmente, o pesquisador usa a
    análise discriminante para identifi car corretamente os mem-
    bros de todos os grupos. Em casos nos quais os tamanhos
    das amostras são desiguais e o pesquisador deseja classifi car
    os membros de todos os grupos, a função discriminante vai
    contra as chances, classifi cando um indivíduo no(s) grupo(s)
    menor(es). O critério por chances não leva esse fato em
    consideração [16].

```
TABELA 5-4 Matriz de classifi cação para análise discriminante de dois grupos
Grupo previsto
```
```
Grupo real 1 2
```
```
Tamanho do
grupo real
```
```
Percentual correta-
mente classifi cado
12 2 32 588
2 52 02580
Tamanho previsto
do grupo 27 23 50 84 a
aPercentual corretamente classifi cado = (Número corretamente classifi cado/Número total de observações) x 100
= [(22 + 20)/50] × 100
= 84%
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 245

```
Em nosso exemplo simples de uma amostra com dois
grupos (75 e 25 pessoas cada), usando esse método te-
ríamos uma precisão de classifi cação de 75%, o que se
conseguiria classifi cando-se todos no grupo maior sem
a ajuda de qualquer função discriminante. Pode-se con-
cluir que, a menos que a função discriminante consiga
uma precisão de classifi cação maior do que 75%, ela
deve ser descartada, pois não nos ajuda a melhorar a
precisão preditiva que podemos atingir sem qualquer
análise discriminante.
```
- Quando os tamanhos de grupos são desiguais e o pesquisa-
    dor deseja identifi car corretamente os membros de todos os
    grupos, não apenas do maior, o **critério de chances propor-**
    **cionais** é considerado por muitos como o mais apropriado.
    A fórmula para esse critério é
       _C_ PRO! _p_^2 "(1 $ _p_ )^2

onde

```
p = proporção de indivíduos no grupo 1
1 – p = proporção de indivíduos no grupo 2
```
```
Usando os tamanhos de grupos de nosso exemplo ante-
rior (75 e 25), percebemos que o critério de chances pro-
porcionais seria de 62,5% [0,75^2 + (1,0 – 0,75)^2 = 0,625]
comparado com 75%. Logo, neste caso, uma precisão
preditiva de 75% seria aceitável porque está acima dos
62,5% do critério de chances proporcionais.
```
- Um problema dos critérios de chance máxima e de chances
    proporcionais são os tamanhos das amostras usados para cál-
    culo dos padrões. Você deve usar grupos com o tamanho da
    amostra geral, da amostra de análise/estimação, ou da amos-
    tra de validação/teste? Aqui vão algumas sugestões:
    - Se os tamanhos das amostras de análise e estimação são
       considerados sufi cientemente grandes (i.e., amostra total
       de 100 com cada grupo tendo pelo menos 20 casos), obte-
       nha padrões separados para cada amostra.
    - Se as amostras separadas não são consideradas sufi cien-
       temente grandes, use os tamanhos de grupos da amostra
       total para calcular os padrões.
    - Atente a tamanhos de grupos diferentes entre amostras
       quando usar o critério de chance máxima, pois ele depen-
       de do maior tamanho de grupo. Esta orientação é espe-
       cialmente crítica quando a amostra é pequena ou quando
       as proporções de tamanhos de grupos variam muito de
       amostra para amostra. Este é outro motivo de cautela no
       emprego do critério de chance máxima.
Esses critérios de chances são úteis somente quando
computados com amostras de teste (abordagem da parti-
ção da amostra). Se os indivíduos usados no cálculo da fun-
ção discriminante são os classifi cados, o resultado é um viés
ascendente na precisão preditiva. Em tais casos, os critérios
deveriam ser ajustados para cima em função desse viés.

```
Comparação da razão de sucesso com o padrão. A
questão de “quanta precisão de classifi cação devo ter?”
é crucial. Se o percentual de classifi cações corretas é sig-
nifi cantemente maior do que se esperaria por chances, o
pesquisador pode proceder à interpretação das funções
discriminantes e de perfi s de grupos. No entanto, se a pre-
cisão de classifi cação não é maior do que pode ser espera-
do das chances, quaisquer diferenças que pareçam existir
merecem pouca ou nenhuma interpretação; ou seja, as
diferenças em perfi s de escores não forneceriam qualquer
informação signifi cativa para identifi car a pertinência a
grupos.
A questão, então, é o quanto a precisão de classi-
fi cação deve ser relativa às chances? Por exemplo, se
as chances são de 50% (dois grupos, com iguais tama-
nhos), uma precisão de classifi cação (preditiva) de 60%
justifi ca ir para o estágio de interpretação? Em última
instância, a decisão depende do custo em relação ao va-
lor da informação. O argumento do custo versus valor
oferece pouca ajuda ao pesquisador iniciante, mas o
seguinte critério é sugerido: A precisão de classifi cação
deve ser pelo menos um quarto maior do que a obtida
por chances.
```
```
Por exemplo, se a precisão por chances for de 50%, a
precisão de classifi cação deverá ser 62,5% (62,5% = 1,25
× 50%). Se a precisão de chances for de 30%, a preci-
são de classifi cação deverá ser 37,5% (37,5%! 1,25 ×
30%).
```
```
Esse critério fornece apenas uma estimativa grosseira
do nível aceitável de precisão preditiva. O critério é fácil
de aplicar com grupos de mesmo tamanho. Com grupos de
tamanhos desiguais, um limite superior é alcançado quan-
do o modelo de chance máxima é usado para determinar
a precisão de chances. No entanto, isso não representa um
grande problema, pois sob a maioria das circunstâncias o
modelo de chance máxima não seria usado com grupos de
tamanhos distintos.
```
```
Razões de sucesso geral versus específicas de gru-
pos. Até este ponto, nos concentramos no cálculo da
razão de sucesso geral em todos os grupos avaliando a
precisão preditiva de uma análise discriminante. O pes-
quisador também deve estar preocupado com a razão de
sucesso (percentual corretamente classifi cado) para cada
grupo separado. Se você se concentrar somente na razão
de sucesso geral, é possível que um ou mais grupos, par-
ticularmente os menores, possam ter razões de sucesso
inaceitáveis enquanto a razão de sucesso geral é aceitá-
vel. O pesquisador deve calcular a razão de sucesso de
cada grupo e avaliar se a análise discriminante fornece
níveis adequados de precisão preditiva tanto no nível ge-
ral quanto para cada grupo.
```

##### 246 Análise Multivariada de Dados

**Medidas com base estatística de precisão de classifi cação
relacionada a chances*** Um teste estatístico do poder
discriminatório da matriz de classifi cação quando com-
parada com um modelo de chances é a **estatística** **_Q_** **de
Press**. Essa medida simples compara o número de clas-
sifi cações corretas com o tamanho da amostra total e o
número de grupos. O valor calculado é então comparado
com um valor crítico (o valor qui-quadrado para um grau
de liberdade no nível de confi ança desejado). Se ele exce-
de este valor crítico, então a matriz de classifi cação pode
ser considerada estatisticamente melhor do que as chan-
ces. A estatística _Q_ é calculada pela seguinte fórmula:

onde

```
N = tamanho da amostra total
n = número de observações corretamente classifi ca-
das
K = número de grupos
```
```
Por exemplo, na Tabela 5-4, a estatística Q seria baseada
em uma amostra total de N = 50, n = 42 observações cor-
retamente classifi cadas, e K = 2 grupos. A estatística cal-
culada seria:
```
```
O valor crítico em um nível de signifi cância de 0,01 é
6,63. Assim, concluiríamos que, no exemplo, as previsões
seriam signifi cantemente melhores do que chances, as
quais teriam uma taxa de classifi cação correta de 50%.
```
Esse teste simples é sensível ao tamanho da amostra;
amostras grandes são mais prováveis de mostrar signifi -
cância do que amostras pequenas da mesma taxa de clas-
sifi cação.

```
Por exemplo, se o tamanho da amostra é aumentado para
100 no exemplo e a taxa de classifi cação permanece em
84%, a estatística Q aumenta para 46,24. Se o tamanho
da amostra sobe para 200, mas mantém a taxa de classifi -
cação em 84%, a estatística Q novamente aumenta para
92,48%. Mas se a amostra for apenas 20 e a taxa de classi-
fi cação incorreta** for ainda de 84% (17 previsões corre-
tas), a estatística Q seria de somente 9,8. Ou seja, examine
a estatística Q à luz do tamanho amostral, pois aumentos
no tamanho da amostra fazem subir a estatística Q ainda
que seja para a mesma taxa de classifi cação geral.
```
```
Porém, é necessário cuidado nas conclusões baseadas
apenas nessa estatística, pois à medida que a amostra fi ca
maior, uma taxa de classifi cação menor ainda será consi-
derada signifi cante.
```
#### Diagnóstico por casos

```
O meio fi nal de avaliar o ajuste de modelo é examinar os
resultados preditivos em uma base de casos. Semelhante
à análise de resíduos em regressão múltipla, o objetivo é
entender quais observações (1) foram mal classifi cadas e
(2) não são representativas dos demais membros do gru-
po. Apesar de a matriz de classifi cação fornecer precisão
de classifi cação geral, ela não detalha os resultados indi-
viduais. Além disso, mesmo que possamos denotar quais
casos são correta ou incorretamente classifi cados, ainda
precisamos de uma medida da similaridade de uma obser-
vação com o restante do grupo.
```
##### Má classifi cação de casos individuais

```
Quando se analisam resíduos de uma análise de regressão
múltipla, uma decisão importante envolve estabelecer o
nível de resíduo considerado substancial e merecedor de
atenção. Em análise discriminante, essa questão é mais
simples, porque uma observação é ou correta, ou incorre-
tamente classifi cada. Todos os programas de computador
fornecem informação que identifi ca quais casos são mal
classifi cados e para quais grupos eles foram mal classifi -
cados. O pesquisador pode identifi car não apenas aqueles
casos com erros de classifi cação, mas uma representação
direta do tipo de má classifi cação.
```
##### Análise de casos mal classifi cados

```
O propósito de identifi car e analisar as observações mal
classifi cadas é identifi car quaisquer características dessas
observações que pudessem ser incorporadas à análise dis-
criminante para melhorar a precisão preditiva. Essa análi-
se pode assumir a forma de se estabelecer o perfi l de casos
mal classifi cados tanto nas variáveis independentes quan-
to em outras variáveis não incluídas no modelo.
```
```
O perfi l das variáveis independentes. Examinar esses
casos nas variáveis independentes pode identifi car ten-
dências não-lineares ou outras relações ou atributos que
conduziram à má classifi cação. Várias técnicas são parti-
cularmente adequadas em análise discriminante:
```
- Uma representação gráfi ca das observações é talvez a abor-
    dagem mais simples e efetiva para examinar as caracterís-
    ticas de observações, especialmente as mal classifi cadas. A
    abordagem mais comum é fazer o gráfi co das observações
    com base em seus escores _Z_ discriminantes e mostrar a so-
    breposição entre grupos e os casos mal classifi cados. Se duas
    ou mais funções são mantidas, os pontos de corte ótimo
    também podem ser representados grafi camente para forne-
    cer aquilo que é conhecido como um **mapa territorial** , que
    exibe as regiões correspondentes para cada grupo.

* N. de R. T.: A palavra “chance” também poderia ser traduzida como
“acaso”.
** N. de R. T.: A frase correta seria “taxa de classifi cação correta”.


##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 247

- Representar grafi camente as observações individuais com
    os centróides dos grupos, como anteriormente discutido,
    mostra não apenas as características gerais dos grupos via
    centróides, mas também a variação nos membros nos gru-
    pos. Isso é análogo às áreas defi nidas no exemplo de três
    grupos no começo deste capítulo, em que escores de cor-
    te em ambas as funções defi niam áreas correspondentes às
    previsões de classifi cação para cada grupo.
- Uma avaliação empírica direta da similaridade de uma ob-
    servação com os membros do outro grupo pode ser feita
    calculando-se a distância _D_^2 de Mahalanobis da observação
    ao centróide do grupo. Com base no conjunto de variáveis
    independentes, observações mais próximas ao centróide
    têm um _D_^2 de Mahalanobis menor e são consideradas mais
    representativas do grupo do que as mais afastadas.
- No entanto, a medida empírica deve ser combinada com uma
    análise gráfi ca, pois apesar de um grande _D_^2 de Mahalanobis
    indicar observações que são bastante diferentes dos centrói-
    des de grupo, isso nem sempre indica má classifi cação. Por
    exemplo, em uma situação de dois grupos, um membro do
    grupo A pode ter uma grande distância _D_^2 de Mahalanobis,
    indicando que ele é menos representativo do grupo. Contu-
    do, se essa distância está afastada do centróide do grupo B,
    então realmente aumentam as chances de classifi cação corre-
    ta, mesmo que ele seja menos representativo do grupo. Uma
    menor distância que coloca uma observação entre os dois
    centróides provavelmente teria uma menor probabilidade
    de classifi cação correta, mesmo que ela esteja mais próxima
    ao centróide de seu grupo do que na situação anterior.
Apesar de não existir qualquer análise pré-especifi -
cada, como na regressão múltipla, o pesquisador é enco-
rajado a avaliar esses casos mal classifi cados de diversos
pontos de vista, na tentativa de descobrir as caracterís-
ticas únicas que eles têm em comparação com os outros
membros do seu grupo.

**Perfi l de variáveis não presentes na análise.** O exame de
outras variáveis quanto às suas diferenças nos casos mal
classifi cados seria o primeiro passo para sua possível in-
clusão na análise discriminante. Muitas vezes, variáveis
que discriminam apenas em um conjunto menor de casos
não são identifi cadas no primeiro conjunto de análises,
mas se tornam mais evidentes na análise de casos mal
classifi cados. O pesquisador é encorajado a rever as áreas
de suporte conceitual para identifi car novas possíveis va-
riáveis que possam se relacionar unicamente com os casos
mal classifi cados e aumentar a precisão preditiva geral.

#### Resumo

O estágio de estimação e avaliação tem várias semelhan-
ças com as outras técnicas de dependência, permitindo um
processo de estimação direta ou _stepwise_ e uma análise da
precisão preditiva geral e de casos. O pesquisador deve de-
dicar considerável atenção a essas questões para evitar o
uso de um modelo de análise discriminante fundamental-
mente errado.

#### ESTÁGIO 5: INTERPRETAÇÃO

#### DOS RESULTADOS

```
Se a função discriminante é estatisticamente signifi cante e
a precisão de classifi cação é aceitável, o pesquisador deve
se concentrar em fazer interpretações substanciais das
descobertas. Esse processo envolve o exame das funções
discriminantes para determinar a importância relativa de
cada variável independente na discriminação entre os gru-
pos. Três métodos para determinar a importância relativa
foram propostos:
```
**1.** Pesos discriminantes padronizados
**2.** Cargas discriminantes (correlações de estrutura)
**3.** Valores _F_ parciais

#### Pesos discriminantes

```
A abordagem tradicional para interpretar funções dis-
criminantes examina o sinal e a magnitude do peso
discriminante padronizado (às vezes chamado de coefi -
ciente discriminante ) designado para cada variável ao se
computarem as funções discriminantes. Quando o sinal
é ignorado, cada peso representa a contribuição relativa
de sua variável associada àquela função. As variáveis
independentes com pesos relativamente maiores con-
tribuem mais para o poder discriminatório da função
do que as variáveis com pesos menores. O sinal indica
```
##### Avaliação do ajuste de modelo e precisão preditiva

- A matriz de classifi cação e a razão de sucesso
    substituem _R_^2 como a medida de ajuste de modelo:
    - Avalie a razão de sucesso geral e por grupo
    - Se as amostras de estimação e análise excederem 100
       casos e cada grupo exceder 20 casos, derive padrões
       separados para cada amostra; caso contrário, derive
       um único padrão a partir da amostra geral
- Critérios múltiplos são usados para comparação com a
    razão de sucesso:
    - O critério de chance máxima para avaliação da
       razão de sucesso é o mais conservador, dando a mais
       elevada base para exceder
    - Seja cuidadoso no uso do critério de chance máxima
       em situações com amostras gerais menores que 100
       e/ou grupos com menos de 20
    - O critério de chance proporcional considera
       todos os grupos no estabelecimento do padrão de
       comparação e é o mais popular
    - A verdadeira precisão preditiva (razão de sucesso)
       deve exceder qualquer valor de critério em pelo
       menos 25%
- Analise as observações mal classifi cadas gráfi ca (mapa
    territorial) e empiricamente ( _D_^2 de Mahalanobis)

###### REGRAS PRÁTICAS 5-3


##### 248 Análise Multivariada de Dados

apenas que a variável tem uma contribuição positiva ou
negativa [4].
A interpretação de pesos discriminantes é análoga
à interpretação de pesos beta em análise de regressão e
está, portanto, sujeita às mesmas críticas. Por exemplo,
um peso pequeno pode indicar que sua variável corres-
pondente é irrelevante na determinação de uma relação,
ou que ela tenha sido deixada de lado na relação por cau-
sa de um elevado grau de multicolinearidade. Um outro
problema do uso de pesos discriminantes é que eles es-
tão sujeitos a considerável instabilidade. Esses problemas
sugerem cuidado ao se usarem pesos para interpretar os
resultados da análise discriminante.

#### Cargas discriminantes

As **cargas discriminantes** , às vezes chamadas de **correla-
ções de estrutura** , são cada vez mais usadas como uma
base para interpretação, por conta das defi ciências na utili-
zação de pesos. Medindo a correlação linear simples entre
cada variável independente e a função discriminante, as
cargas discriminantes refl etem a variância que as variáveis
independentes compartilham com a função discriminan-
te. Em relação a isso, elas podem ser interpretadas como
cargas fatoriais na avaliação da contribuição relativa de
cada variável independente para a função discriminante.
(O Capítulo 3 discute melhor a interpretação de cargas
fatoriais.)
Uma característica ímpar de cargas é que elas podem
ser calculadas para todas as variáveis, sejam elas usadas na
estimação da função discriminante ou não. Este aspecto
é particularmente útil quando um processo de estimação
_stepwise_ é empregado e algumas variáveis não são incluí-
das na função discriminante. Em vez de não se ter forma
alguma de compreender seu impacto relativo, as cargas
fornecem um efeito relativo de cada variável em uma me-
dida comum.
Com as cargas, a questão principal é: Quais valores as
cargas devem assumir para serem consideradas substan-
tivas discriminadoras dignas de nota? Tanto em análise
discriminante simultânea quanto _stepwise_ , variáveis que
exibem uma carga de ± 0,40 ou mais são consideradas
substantivas. Com procedimentos _stepwise_ , tal determi-
nação é suplementada, pois a técnica evita que variáveis
não-signifi cantes entrem na função. Porém, multicoline-
aridade e outros fatores podem evitar uma variável na
equação, o que não signifi ca necessariamente que ela não
tenha um efeito substancial.
As cargas discriminantes (assim como os pesos) podem
estar sujeitas à instabilidade. As cargas são consideradas
relativamente mais válidas do que os pesos como um meio
de interpretação do poder discriminatório de variáveis in-
dependentes por causa de sua natureza correlacional. O
pesquisador ainda deve ser cuidadoso ao usar cargas para
interpretar funções discriminantes.

#### Valores F parciais

```
Como anteriormente discutido, duas abordagens compu-
tacionais – simultânea e stepwise – podem ser utilizadas
para determinar funções discriminantes. Quando o mé-
todo stepwise é selecionado, um meio adicional de inter-
pretar o poder discriminatório relativo das variáveis inde-
pendentes está disponível pelo uso de valores F parciais.
Isso é obtido examinando-se os tamanhos absolutos dos
valores F signifi cantes e ordenando-os. Valores F grandes
indicam maior poder discriminatório. Na prática, as or-
denações que usam a abordagem dos valores F são iguais
à ordenação determinada a partir do uso de pesos discri-
minantes, mas os valores F indicam o nível associado de
signifi cância para cada variável.
```
#### Interpretação de duas ou mais funções

```
Quando há duas ou mais funções discriminantes signi-
fi cantes, temos problemas adicionais de interpretação.
Primeiro, podemos simplifi car os pesos ou cargas discri-
minantes para facilitar a determinação do perfi l de cada
função? Segundo, como representamos o impacto de cada
variável nas funções? Esses problemas ocorrem tanto na
medida dos efeitos discriminantes totais das funções quan-
to na avaliação do papel de cada variável no perfi l de cada
função separadamente. Tratamos dessas duas questões
introduzindo os conceitos de rotação das funções, o índice
de potência, e representações de vetores expandidos.
```
##### Rotação das funções discriminantes

```
Depois que as funções discriminantes foram desenvolvi-
das, elas podem ser rotacionadas para redistribuir a va-
riância. (O conceito é melhor explicado no Capítulo 3.)
Basicamente, a rotação preserva a estrutura original e a
confi abilidade da solução discriminante, ao passo que tor-
na as funções muito mais fáceis de interpretar. Na maio-
ria dos casos, a rotação VARIMAX é empregada como a
base para a rotação.
```
##### Índice de potência

```
Anteriormente discutimos o uso de pesos padronizados ou
cargas discriminantes como medidas da contribuição de
uma variável a uma função discriminante. Quando duas
ou mais funções são determinadas, contudo, uma medida
resumo ou composta é útil para descrever as contribuições
de uma variável em todas as funções signifi cantes. O índice
de potência é uma medida relativa entre todas as variáveis
que é indicativa do poder discriminante de cada variável
[18]. Ele inclui a contribuição de uma variável a uma fun-
ção discriminante (sua carga discriminante) e a contribui-
ção relativa da função para a solução geral (uma medida
relativa entre as funções com base nos autovalores). A
composição é simplesmente a soma dos índices de potência
individuais em todas as funções discriminantes signifi can-
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 249

tes. A interpretação da medida composta é limitada, contu-
do, pelo fato de que é útil apenas na representação da po-
sição relativa (como o oposto de uma ordenação) de cada
variável, e o valor absoluto não tem qualquer signifi cado
real. O índice de potência é calculado por um processo de
dois passos:

**Passo 1:** _Calcular um valor de potência para cada função sig-
nifi cante._ No primeiro passo, o poder discriminatório
de uma variável, representado pelo quadrado da carga
discriminante não-rotacionada, é “ponderado” pela
contribuição relativa da função discriminante para a
solução geral. Primeiro, a medida do autovalor relativo
para cada função discriminante signifi cante é calculada
simplesmente como:

```
O valor potência de cada variável em uma função dis-
criminante é então:
```
**Passo 2:** _Calcular um índice de potência composto em todas as
funções signifi cantes._ Uma vez que um valor potência
tenha sido calculado para cada função, o índice de po-
tência composto para cada variável é calculado como:

O índice de potência agora representa o efeito discrimi-
nante total da variável em todas as funções discriminantes
signifi cantes. É apenas uma medida relativa, contudo, e seu
valor absoluto não tem qualquer signifi cado importante.
Uma ilustração de cálculo de índice de potência é forneci-
da no exemplo para análise discriminante de três grupos.

##### Disposição gráfi ca de escores e

##### cargas discriminantes

Para representar diferenças nos grupos nas variáveis
preditoras, o pesquisador pode usar dois diferentes tra-
tamentos para representação gráfi ca. O mapa territorial
representa grafi camente os casos individuais de funções
discriminantes signifi cantes para permitir ao pesquisador
uma avaliação da posição relativa de cada observação
com base nos escores da função discriminante. A segunda
abordagem é representar grafi camente as cargas discrimi-
nantes para entender o agrupamento relativo e a magnitu-
de de cada carga sobre cada função. Cada abordagem será
discutida detalhadamente na próxima seção.

**Mapa territorial.** O método gráfi co mais comum é o
mapa territorial, no qual cada observação é impressa em

```
um gráfi co com base nos escores Z da função discrimi-
nante das observações. Por exemplo, considere que uma
análise discriminante de três grupos tem duas funções
discriminantes signifi cantes. Um mapa territorial é criado
fazendo-se o gráfi co dos escores Z discriminantes de cada
observação para a primeira função discriminante sobre o
eixo X e os escores para a segunda função discriminante
sobre o eixo Y. Desse modo, isso fornece diversas pers-
pectivas de análise:
```
- O gráfi co dos membros de cada grupo com diferentes sím-
    bolos permite um retrato fácil das diferenças de cada grupo,
    bem como suas sobreposições um com o outro.
- O gráfi co dos centróides de cada grupo fornece uma manei-
    ra de avaliar cada membro de grupo relativamente ao seu
    centróide. Este procedimento é particularmente útil na ava-
    liação da possibilidade de grandes medidas de Mahalanobis
    _D_^2 conduzirem a classifi cações ruins.
- Retas representando os escores de corte também podem ser
    grafi camente representadas, denotando fronteiras que re-
    presentam os intervalos de escores discriminantes previstos
    em cada grupo. Quaisquer membros de grupos que estejam
    fora dessas fronteiras são mal classifi cados. Denotar os casos
    mal classifi cados permite uma avaliação sobre qual função
    discriminante foi mais responsável pela má classifi cação, e
    sobre o grau em que um caso é mal classifi cado.

```
Gráfi co vetorial de cargas discriminantes. A abordagem
gráfi ca mais simples é representar cargas reais rotaciona-
das ou não-rotacionadas. A abordagem preferencial seria
com cargas rotacionadas. Semelhante ao gráfi co de cargas
fatoriais (ver Capítulo 3), este método representa o grau
em que cada variável é associada com cada função discri-
minante.
Uma técnica ainda mais precisa, porém, envolve o
gráfi co de cargas bem como vetores para cada carga e
centróide de grupo. Um vetor é meramente uma reta de-
senhada a partir da origem (centro) de um gráfi co até as
coordenadas das cargas de uma variável particular ou um
centróide de grupo. Com a representação de um vetor ex-
pandido , o comprimento de cada vetor se torna indicativo
da importância relativa de cada variável na discriminação
entre os grupos. O procedimento gráfi co segue em três
passos:
```
**1.** _Seleção de variáveis:_ Todas as variáveis, sejam incluídas
    no modelo ou não, podem ser grafi camente representadas
    como vetores. Desse modo, a importância de variáveis co-
    lineares que não estão incluídas, como em _stepwise_ , ainda
    pode ser retratada.
**2.** _Expansão de vetores:_ As cargas discriminantes de cada va-
    riável são expandidas multiplicando-se a carga discriminan-
    te (preferencialmente após a rotação) por seu respectivo va-
    lor _F_ univariado. Notamos que os vetores apontam para os
    grupos com a maior média sobre o preditor respectivo e na
    direção oposta dos grupos com os menores escores médios.
**3.** _Gráfi co dos centróides de grupos:_ Os centróides de grupo
    também são expandidos nesse procedimento, sendo multi-
    plicados pelo valor _F_ aproximado associado a cada função


##### 250 Análise Multivariada de Dados

```
discriminante. Se as cargas são expandidas, os centróides
também devem ser expandidos para representá-los com
precisão no mesmo gráfi co. Os valores F aproximados para
cada função discriminante são obtidos pela seguinte fór-
mula:
```
```
onde
N Amostra de estimação = tamanho da amostra de estimação
```
```
Por exemplo, considere que a amostra de 50 observações
tenha sido dividida em três grupos. O multiplicador de
cada autovalor seria (50 – 3)/(3 – 1) = 23,5.
```
Quando completado, o pesquisador dispõe de um re-
trato do agrupamento de variáveis em cada função dis-
criminante, a magnitude da importância de cada variável
(representada pelo comprimento de cada vetor) e o perfi l
de cada centróide de grupo (mostrado pela proximidade
de cada vetor). Apesar de este procedimento dever ser
feito manualmente na maioria dos casos, ele dá um retra-
to completo das cargas discriminantes e dos centróides de
grupos. Para mais detalhes sobre esse procedimento, ver
Dillon e Goldstein [4].

#### Qual método interpretativo usar?

Diversos métodos para interpretar a natureza das funções
discriminantes foram discutidos, tanto para soluções de
uma função quanto de múltiplas. Quais métodos devem
ser usados? A abordagem das cargas é mais válida do que
o emprego de pesos e deve ser utilizada sempre que pos-
sível. O uso de valores _F_ parciais e univariados permite
ao pesquisador empregar diversas medidas e procurar
alguma consistência nas avaliações das variáveis. Se duas
ou mais funções são estimadas, então o pesquisador pode
utilizar diversas técnicas gráfi cas e o índice de potência,
que ajuda na interpretação da solução multidimensional.
O ponto mais básico é que o pesquisador deve usar todos
os métodos disponíveis para chegar à interpretação mais
precisa.

#### ESTÁGIO 6: VALIDAÇÃO

#### DOS RESULTADOS

O estágio fi nal de uma análise discriminante envolve a
validação dos resultados discriminantes para garantir que
os resultados têm validade externa e interna. _Com a pro-
pensão da análise discriminante para aumentar a razão de
sucesso se avaliada apenas sobre a amostra de análise, a
validação é um passo essencial._ Além de validar as razões

```
de sucesso, o pesquisador deve usar o perfi l de grupos
para garantir que as médias de grupos sejam indicadores
válidos do modelo conceitual usado na seleção de variá-
veis independentes.
```
#### Procedimentos de validação

```
Validação é um passo crítico em qualquer análise discri-
minante, pois muitas vezes, especialmente com amostras
menores, os resultados podem carecer de generalidade
(validade externa). A técnica mais comum para estabe-
lecer validade externa é a avaliação de razões de suces-
so. Validação pode ocorrer com uma amostra separada
(amostra de teste) ou utilizando-se um procedimento que
repetidamente processa a amostra de estimação. Validade
externa é admitida quando a razão de sucesso da aborda-
gem selecionada excede os padrões de comparação que
representam a precisão preditiva esperada pelo acaso (ver
discussão anterior).
```
##### Utilização de uma amostra de teste

```
Geralmente, a validação das razões de sucesso é execu-
tada criando-se uma amostra de teste, também chamada
de amostra de validação. O propósito de se utilizar uma
amostra de teste para fi ns de validação é ver o quão bem
a função discriminante funciona em uma amostra de ob-
servações não usadas para obter a mesma. Este processo
envolve o desenvolvimento de uma função discriminante
com a amostra de análise e então a sua aplicação na amos-
tra de teste. A justifi cativa para dividir a amostra total em
dois grupos é que um viés ascendente ocorrerá na precisão
preditiva da função discriminante se os indivíduos usados
no desenvolvimento da matriz de classifi cação forem os
mesmos utilizados para computar a função; ou seja, a pre-
cisão de classifi cação será mais alta do que é válido se ela
for aplicada na amostra de estimação.
Outros pesquisadores têm sugerido que uma confi ança
maior ainda poderia ser depositada na validade da função
discriminante seguindo-se esse procedimento diversas ve-
zes [18]. Ao invés de dividir aleatoriamente a amostra to-
tal em grupos de análise e de teste uma vez, o pesquisador
dividiria aleatoriamente a amostra total em amostras de
análise e de teste várias vezes, sempre testando a valida-
de da função discriminante pelo desenvolvimento de uma
matriz de classifi cação e de uma razão de sucesso. Então
as diversas razões de sucesso teriam uma média para se
obter uma única medida.
```
##### Validação cruzada

```
A técnica de validação cruzada para avaliar validade ex-
terna é feita com múltiplos subconjuntos da amostra total
[2,4]. A abordagem mais amplamente usada é o método
jackknife. Validação cruzada é baseada no princípio do
“deixe um de fora”. O uso mais comum desse método é
estimar k – 1 amostras, eliminando-se uma observação
por vez a partir de uma amostra de k casos. Uma fun-
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 251

ção discriminante é calculada para cada subamostra, e
em seguida a pertinência a grupo prevista da observação
eliminada é feita com a função discriminante estimada
sobre os demais casos. Depois que todas as previsões de
pertinência a grupo foram feitas, uma por vez, uma ma-
triz de classifi cação é construída e a razão de sucesso é
calculada.
Validação cruzada é muito sensível a amostras pe-
quenas. Orientações sugerem que ela seja usada somente
quando o tamanho do grupo menor é pelo menos três ve-
zes o número de variáveis preditoras, e a maioria dos pes-
quisadores sugere uma proporção de cinco para um [13].
No entanto, validação cruzada pode representar a única
técnica de validação possível em casos em que a amos-
tra original é muito pequena para dividir em amostras de
análise e de teste, mas ainda excede as orientações já dis-
cutidas. Validação cruzada também está se tornando mais
amplamente usada à medida que os principais programas
de computador a disponibilizam como opção.

#### Diferenças de perfi s de grupos

Uma outra técnica de validação é estabelecer o perfi l dos
grupos sobre as variáveis independentes para garantir
sua correspondência com as bases conceituais usadas na
formulação do modelo original. Depois que o pesquisa-
dor identifi ca as variáveis independentes que oferecem
a maior contribuição à discriminação entre os grupos, o
próximo passo é traçar o perfi l das características dos gru-
pos com base nas médias dos mesmos. Esse perfi l permite
ao pesquisador compreender o caráter de cada grupo de
acordo com as variáveis preditoras.

```
Por exemplo, olhando os dados da pesquisa da Kitchen-
Aid apresentados na Tabela 5-1, percebemos que a ava-
liação média de “durabilidade” para o grupo “compra-
ria” é 7,4, enquanto a avaliação média comparável de
“durabilidade” para o grupo “não compraria” é de 3,2.
Assim, um perfi l desses dois grupos mostra que o grupo
“compraria” avalia a durabilidade percebida do novo
produto bem mais do que o grupo “não compraria”.
```
```
Outra abordagem é estabelecer o perfi l de grupos em
um conjunto separado de variáveis que deve espelhar as
diferenças observadas de grupos. Esse perfi l separado for-
nece uma avaliação de validade externa, de modo que os
grupos variam tanto na(s) variável(eis) independente(s)
quanto no conjunto de variáveis associadas. Essa técnica
é semelhante, em caráter, à validação de agrupamentos
obtidos descrita no Capítulo 8.
```
#### UM EXEMPLO ILUSTRATIVO

#### DE DOIS GRUPOS

```
Para ilustrar a aplicação da análise discriminante de dois
grupos, usamos variáveis obtidas da base de dados HBAT
introduzida no Capítulo 1. Esse exemplo examina cada
um dos seis estágios do processo de construção de modelo
para um problema de pesquisa particularmente adequado
à análise discriminante múltipla.
```
#### Estágio 1: Objetivos da análise discriminante

##### Interpretação e validação de funções

##### discriminantes

- Cargas discriminantes são o método preferido para
    avaliar a contribuição de cada variável em uma função
    discriminante, pois elas são:
    - Uma medida padronizada de importância (variando
       de 0 a 1)
    - Disponíveis para todas as variáveis independentes,
       sejam usadas no processo de estimação ou não
    - Não afetadas por multicolinearidade
- Cargas excedendo ± 0,40 são consideradas substantivas
    para fi ns de interpretação
- No caso de mais de uma função discriminante,
    certifi que-se de:
    - Usar cargas rotacionadas
    - Avaliar a contribuição de cada variável em todas as
       funções com o índice de potência
- A função discriminante deve ser validada com a
    amostra de teste ou um dos procedimentos “deixe um
    de fora”

```
REGRAS PRÁTICAS 5-4 Você lembra que uma das características de cliente obti-
da pela HBAT em sua pesquisa foi uma variável categó-
rica ( X 4 ) que indicava a região na qual a empresa estava
localizada: EUA/América do Norte ou fora. A equipe
administrativa da HBAT está interessada em quaisquer
diferenças de percepções entre aqueles clientes localiza-
dos e servidos por sua equipe de venda nos EUA versus
aqueles fora dos EUA e que são servidos principalmente
por distribuidores independentes. A despeito de diferen-
ças encontradas em termos de suporte de vendas devido
à natureza da equipe de venda servindo cada área geo-
gráfi ca, a equipe administrativa está interessada em ver
se as outras áreas de operação (linha do produto, preço
etc.) são vistas de maneira distinta por estes dois con-
juntos de clientes. Esta indagação segue a óbvia neces-
sidade por parte da administração de sempre procurar
melhor entender seu cliente, neste caso se concentrando
em diferenças que podem ocorrer entre áreas geográfi -
cas. Se quaisquer percepções de HBAT forem notadas
como diferindo signifi cativamente entre fi rmas nessas
duas regiões, a companhia será então capaz de desen-
```

##### 252 Análise Multivariada de Dados

Para tanto, a análise discriminante foi selecionada para
identifi car aquelas percepções da HBAT que melhor dife-
renciam as empresas em cada região geográfi ca.

#### Estágio 2: Projeto de pesquisa

#### para análise discriminante

O estágio de projeto de pesquisa se concentra em três ques-
tões-chave: selecionar variáveis dependente e independen-
tes, avaliar a adequação do tamanho da amostra para a aná-
lise planejada, e dividir a amostra para fi ns de validação.

##### Seleção de variáveis dependente e independentes

A análise discriminante requer uma única medida depen-
dente não-métrica e uma ou mais medidas independentes
métricas que são afetadas para fornecer diferenciação en-
tre os grupos baseados na medida dependente.

```
Como a variável dependente Região ( X 4 ) é uma variá-
vel categórica de dois grupos, a análise discriminante é a
técnica apropriada. O levantamento coletou percepções
da HBAT que agora podem ser usadas para distinguir
entre os dois grupos de fi rmas. A análise discriminante
usa como variáveis independentes as 13 variáveis de per-
cepção a partir do banco de dados ( X 6 a X 18 ) para discri-
minar entre fi rmas em cada área geográfi ca.
```
##### Tamanho da amostra

Dado o tamanho relativamente pequeno da amostra
HBAT (100 observações), questões como tamanho amos-
tral são particularmente importantes, especialmente a di-
visão da amostra em amostras de teste e de análise (ver
discussão na próxima seção).

```
A amostra de 100 observações, quando particionada em
amostras de análise e de teste de 60 e 40 respectivamente,
mal atende à proporção mínima de 5 para 1 de observa-
ções para variáveis independentes (60 observações para
13 variáveis independentes em potencial) sugerida para
a amostra de análise. Apesar de essa proporção crescer
para quase 8 para 1 se a amostra não for dividida, consi-
dera-se mais importante validar os resultados do que au-
mentar o número de observações na amostra de análise.
Os dois grupos de 26 e 34 na amostra de estimação
também excedem o tamanho mínimo de 20 observações
por grupo. Finalmente, os dois grupos são sufi cientemen-
te comparáveis em tamanho para não impactar adversa-
mente os processos de estimação ou de classifi cação.
```
##### Divisão da amostra

```
A discussão anterior enfatizou a necessidade de validar
a função discriminante dividindo a amostra em duas par-
tes, uma usada para estimação e a outra para validação.
Em qualquer momento em que uma amostra de teste é
empregada, o pesquisador deve garantir que os tamanhos
de amostra resultantes sejam sufi cientes para embasar o
número de preditores incluídos na análise.
```
```
A base de dados HBAT tem 100 observações; foi deci-
dido que uma amostra de teste de 40 observações seria
sufi ciente para fi ns de validação. Essa partição deixaria
ainda 60 observações para a estimação da função discri-
minante. Além disso, os tamanhos relativos de grupos na
amostra de estimação (26 e 34 nos dois grupos) permiti-
riam a estimação sem complicações devidas a diferenças
consideráveis de tamanhos de grupos.
```
```
É importante garantir aleatoriedade na seleção da
amostra de validação, de modo que qualquer ordenação
das observações não afete os processos de estimação e de
validação.
```
#### Estágio 3: Suposições da análise discriminante

```
As principais suposições inerentes à análise discrimi-
nante envolvem a formação da variável estatística ou
função discriminante (normalidade, linearidade e mul-
ticolinearidade) e a estimação da função discriminan-
te (matrizes de variância e covariância iguais). Como
examinar as variáveis independentes quanto à norma-
lidade, linearidade e multicolinearidade é explicado
no Capítulo 2. Para fi ns de nossa ilustração da análise
discriminante, essas suposições são atendidas em níveis
aceitáveis.
A maioria dos programas estatísticos tem um ou mais
teste(s) estatístico(s) para a suposição de matrizes de co-
variância ou dispersão iguais abordada no Capítulo 2. O
mais comum é o teste M de Box (para mais detalhes, ver
Capítulo 2).
```
```
Neste exemplo de dois grupos, a signifi cância de dife-
renças nas matrizes de covariância entre os dois gru-
pos é de 0,011. Mesmo que a signifi cância seja menor
que 0,05 (nesse teste o pesquisador procura por valo-
res acima do nível desejado de signifi cância), a sensibi-
lidade do teste a outros fatores que não sejam apenas
diferenças de covariância (p.ex., normalidade das va-
riáveis e tamanho crescente da amostra) faz desse um
nível aceitável.
```
```
Nenhuma ação corretiva adicional faz-se necessária
antes que a estimação da função discriminante possa ser
realizada.
```
```
volver estratégias para remediar quaisquer defi ciências
percebidas e desenvolver estratégias diferenciadas para
acomodar as percepções distintas.
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 253

#### Estágio 4: Estimação do modelo

#### discriminante e avaliação do ajuste geral

O pesquisador tem a escolha de duas técnicas de estima-
ção (simultânea versus _stepwise_ ) para determinar as va-
riáveis independentes incluídas na função discriminante.
Uma vez que a técnica de estimação é escolhida, o pro-
cesso determina a composição da função discriminante
sujeita à exigência de signifi cância estatística especifi cada
pelo pesquisador.

```
O principal objetivo dessa análise é identifi car o con-
junto de variáveis independentes (percepções HBAT)
que diferencia ao máximo entre os dois grupos de
clientes. Se o conjunto de variáveis de percepções fos-
se menor ou a meta fosse simplesmente determinar
as capacidades discriminantes do conjunto inteiro de
variáveis de percepção, sem se preocupar com o im-
pacto de qualquer percepção individual, então a abor-
dagem simultânea de inclusão de todas as variáveis
diretamente na função discriminante seria empregada.
Mas neste caso, mesmo com o conhecimento de mul-
ticolinearidade entre as variáveis de percepção vista
no desempenho da análise fatorial (ver Capítulo 3), a
abordagem stepwise é considerada mais adequada. De-
vemos observar, porém, que multicolinearidade pode
impactar sobre quais variáveis entram na função discri-
minante e assim exigir particular atenção no processo
de interpretação.
```
##### Avaliação de diferenças de grupos

Iniciemos nossa avaliação da análise discriminante de
dois grupos examinando a Tabela 5-5, que mostra as mé-
dias de grupos para cada uma das variáveis independen-
tes, com base nas 60 observações que constituem a amos-
tra de análise.
Para identifi car quais das cinco variáveis, mais alguma
das demais, melhor discrimina entre os grupos, devemos
estimar a função discriminante.

##### Estimação da função discriminante

```
O procedimento stepwise começa com todas as variáveis
excluídas do modelo e então seleciona a variável que:
```
**1.** Mostra diferenças estatisticamente signifi cantes nos grupos
    (0,05 ou menos exigido para entrada)
**2.** Dá a maior distância de Mahalanobis ( _D_^2 ) entre os grupos
    Este processo continua a incluir variáveis na função
discriminante desde que elas forneçam discriminação adi-
cional estatisticamente signifi cante entre os grupos além
daquelas diferenças já explicadas pelas variáveis na fun-
ção discriminante.Esta técnica é semelhante ao processo
_stepwise_ em regressão múltipla (ver Capítulo 4), que adi-
ciona variáveis com aumentos signifi cantes na variância
explicada da variável dependente. Além disso, em casos
nos quais duas ou mais variáveis entram no modelo, as va-
riáveis já presentes são avaliadas para possível remoção.
Uma variável pode ser removida se existir elevada multi-
colinearidade entre ela e as demais variáveis independen-
tes incluídas, de modo que sua signifi cância fi ca abaixo do
nível para remoção (0,10).

```
Ao estabelecer o perfi l dos dois grupos, podemos pri-
meiramente identifi car cinco variáveis com as maio-
res diferenças nas médias de grupo ( X 6 , X 11 , X 12 , X 13 , e
X 17 ). A Tabela 5-5 também exibe o lambda de Wilks e a
ANOVA univariada utilizada para avaliar a signifi cân-
cia entre médias das variáveis independentes para os
dois grupos. Esses testes indicam que as cinco variáveis
de percepção são também as únicas com diferenças uni-
variadas signifi cantes entre os dois grupos. Finalmente,
os valores D^2 de Mahalanobis mínimos são também da-
dos. Este valor é importante porque ele é a medida usa-
da para selecionar variáveis para entrada no processo
de estimação stepwise. Como apenas dois grupos estão
```
```
envolvidos, o maior valor D^2 tem também a diferença
entre grupos mais signifi cante (note que o mesmo fato
não ocorre necessariamente com três ou mais grupos,
nos quais grandes diferenças entre dois grupos quais-
quer podem não resultar nas maiores diferenças gerais
em todos os grupos, como será mostrado no exemplo
de três grupos).
O exame das diferenças de grupos leva à identifi ca-
ção de cinco variáveis de percepção ( X 6 , X 11 , X 12 , X 13 e
X 17 ) como o conjunto mais lógico de candidatos a entra-
rem na análise discriminante. Essa considerável redução
a partir do conjunto maior de 13 variáveis de percepção
reforça a decisão de se usar um processo de estimação
stepwise.
```
```
Estimação stepwise : adição da primeira variável
X 13. A partir de nossa revisão de diferenças de gru-
pos, percebemos que X 13 tinha a maior diferença signi-
fi cante entre grupos e o maior D^2 de Mahalanobis (ver
Tabela 5-5). Logo, X 13 entra como a primeira variável
no procedimento stepwise (ver Tabela 5-6). Como ape-
nas uma variável entra no modelo discriminante neste
momento, os níveis de signifi cância e as medidas de
diferenças de grupos coincidem com aqueles dos testes
univariados.
Depois que X 13 entra no modelo, as demais variáveis
são avaliadas com base em suas habilidades discriminan-
tes incrementais (diferenças de médias de grupos depois
( Continua )
```

##### 254 Análise Multivariada de Dados

```
TABELA 5-5 Estatísticas descritivas de grupo e testes de igualdade para a amostra de estimação na análise discriminante de dois grupos
Médias de grupos da variá-
vel dependente: X 4 Região
```
```
Teste de igualdade de médias de
grupos*
```
```
D^2 de Mahalanobis
mínimo
```
```
Variáveis independentes
```
```
Grupo 0:
EUA/Améri-
ca do Norte
( n = 26)
```
```
Grupo 1:
Fora da Amé-
rica do Norte
( n = 34)
```
```
Lambda
de Wilks Valor F
```
```
Signifi cân-
cia D^2 mínimo
```
```
Entre
grupos
X 6 Qualidade do produto 8,527 7,297 0,801 14,387 0,000 0,976 0 e 1
X 7 Atividades de Comércio eletrônico 3,388 3,626 0,966 2,054 0,157 0,139 0 e 1
X 8 Suporte técnico 5,569 5,050 0,973 1,598 0,211 0,108 0 e 1
X 9 Solução de reclamação 5,577 5,253 0,986 0,849 0,361 0,058 0 e 1
X 10 Anúncio 3,727 3,979 0,987 0,775 0,382 0,053 0 e 1
X 11 Linha do produto 6,785 5,274 0,695 25,500 0,000 1,731 0 e 1
X 12 Imagem da equipe de venda 4,427 5,238 0,856 9,733 0,003 0,661 0 e 1
X 13 Preço competitivo 5,600 7,418 0,645 31,992 0,000 2,171 0 e 1
X 14 Garantia e reclamações 6,050 5,918 0,992 0,453 0,503 0,031 0 e 1
X 15 Novos produtos 4,954 5,276 0,990 0,600 0,442 0,041 0 e 1
X 16 Encomenda e cobrança 4,231 4,153 0,999 0,087 0,769 0,006 0 e 1
X 17 Flexibilidade de preço 3,631 4,932 0,647 31,699 0,000 2,152 0 e 1
X 18 Velocidade de entrega 3,873 3,794 0,997 0,152 0,698 0,010 0 e 1
* Lambda de Wilks (estatística U ) e razão F univariada com 1 e 58 graus de liberdade.
```
```
que a variância associada com X 13 é removida). Nova-
mente, variáveis com níveis de signifi cância maiores que
0,05 são eliminadas de consideração para entrada no
próximo passo.
O exame das diferenças univariadas mostradas na
Tabela 5-5 identifi ca X 17 (Flexibilidade de preço) como
a variável com a segunda maior diferença. No entanto,
o processo stepwise não utiliza esses resultados univa-
riados quando a função discriminante tem uma ou mais
variáveis. Ele calcula os valores D^2 e os testes de signi-
fi cância estatística de diferenças de grupos depois que o
efeito das variáveis nos modelos é removido (neste caso
apenas X 13 está no modelo).
Como mostrado na última parte da Tabela 5-6, três
variáveis ( X 6 , X 11 e X 17 ) claramente atendem ao crité-
rio de nível de signifi cância de 0,05 para consideração no
próximo estágio. X 17 permanece como o próximo melhor
candidato a entrar no modelo porque ela tem o maior
D^2 de Mahalanobis (4,300) e o maior valor F a entrar.
Não obstante, outras variáveis (p.ex., X 11 ) têm substan-
ciais reduções em seu nível de signifi cância e no D^2 de
Mahalanobis em relação ao que se mostra na Tabela 5-5
devido à variável única no modelo ( X 13 ).
```
```
Estimação stepwise : adição da segunda variável X 17. No
passo 2 (ver Tabela 5-7), X 17 entra no modelo, conforme
esperado. O modelo geral é signifi cante ( F = 31,129) e
melhora a discriminação entre grupos, como evidencia-
do pela diminuição no lambda de Wilks de 0,645 para
```
```
0,478. Além disso, o poder discriminante de ambas as va-
riáveis incluídas nesse ponto é também estatisticamente
signifi cante (valores F de 20,113 para X 13 e 19,863 para
X 17 ). Com ambas as variáveis estatisticamente signifi can-
tes, o procedimento se dirige para o exame das variáveis
fora da equação na busca de potenciais candidatos para
inclusão na função discriminante com base em sua dis-
criminação incremental entre os grupos.
X 11 é a próxima variável a atender às exigências para
inclusão, mas seu nível de signifi cância e sua habilida-
de discriminante foram reduzidos substancialmente por
conta da multicolinearidade com X 13 e X 17 já na função
discriminante. Mais notável ainda é o considerável au-
mento no D^2 de Mahalanobis em relação aos resultados
univariados nos quais cada variável é considerada sepa-
radamente. No caso de X 11, o valor D^2 mínimo aumenta
de 1,731 (ver Tabela 5-5) para 5,045 (Tabela 5-7), o que
indica um espalhamento e uma separação dos grupos
por conta de X 13 e X 17 já na função discriminante. Note
que X 18 é quase idêntica em poder discriminante rema-
nescente, mas X 11 entrará no terceiro passo devido à sua
pequena vantagem.
```
```
Estimação stepwise : adição de uma terceira variável
X 11. A Tabela 5-8 revê os resultados do terceiro passo
do processo stepwise , onde X 11 entra na função discri-
minante. Os resultados gerais ainda são estatisticamente
signifi cantes e continuam a melhorar na discriminação,
como evidenciado pela diminuição no valor lambda de
( Continua )
```
```
( Continuação )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 255

**TABELA 5-6** Resultados do passo 1 da análise discriminante _stepwise_ de dois grupos

**Ajuste geral do modelo**

```
Valor Valor F Graus de liberdade Signifi cância
```
Lambda de Wilks 0,645 31,992 1,58 0,000

**Variáveis adicionadas/removidas no passo 1**

```
F
Variável adicionada D^2 mínimo Valor Signifi cância Entre grupos
```
_X_ 13 Preços competitivos 2,171 31,992 0,000 0 e 1

Nota: Em cada passo, a variável que maximiza a distância de Mahalanobis entre os dois grupos mais próximos é adicionada.

**Variáveis na análise após o passo 1**

```
Variável Tolerância F para remover D^2 Entre grupos
```
_X_ 13 Preços competitivos 1,000 31,992

**Variáveis fora da análise após o passo 1**

```
Variável Tolerância Tolerância mínima F para entrar D^2 mínimo Entre grupos
```
_X_ 6 Qualidade de produto 0,965 0,965 4,926 2,699 0 e 1
_X_ 7 Atividades de comércio eletrônico 0,917 0,917 0,026 2,174 0 e 1
_X_ 8 Suporte técnico 0,966 0,966 0,033 2,175 0 e 1
_X_ 9 Solução de reclamação 0,844 0,844 1,292 2,310 0 e 1
_X_ 10 Anúncio 0,992 0,992 0,088 2,181 0 e 1
_X_ 11 Linha de produto 0,849 0,849 6,076 2,822 0 e 1
_X_ 12 Imagem da equipe de venda 0,987 0,987 3,949 2,595 0 e 1
_X_ 14 Garantia e reclamações 0,918 0,918 0,617 2,237 0 e 1
_X_ 15 Novos produtos 1,000 1,000 0,455 2,220 0 e 1
_X_ 16 Encomenda e cobrança 0,836 0,836 3,022 2,495 0 e 1
_X_ 17 Flexibilidade de preço 1,000 1,000 19,863 4,300 0 e 1
_X_ 18 Velocidade de entrega 0,910 0,910 1,196 2,300 0 e 1

**Teste de signifi cância de diferenças de grupos após o passo 1a
EUA/América do Norte**
Fora da América do Norte _F_ 31,992
Sig. 0,000
a1,58 graus de liberdade

```
Wilks (de 0,478 para 0,438). Note, porém, que a queda
foi muito menor do que aquela encontrada quando a
segunda variável ( X 17 ) foi adicionada à função discrimi-
nante. Com X 13 , X 17 e X 11 estatisticamente signifi cantes,
o procedimento se dirige para a identifi cação de candi-
datos remanescentes para inclusão.
Como visto na última parte da Tabela 5-8, nenhuma
das 10 variáveis independentes que sobraram passam
pelo critério de entrada de signifi cância estatística de
0,05. Depois que X 11 entrou na equação, as duas variá-
veis remanescentes que tinham diferenças univariadas
signifi cantes nos grupos ( X 6 e X 12 ) apresentam um po-
der discriminatório adicional relativamente pequeno e
não atendem ao critério de entrada. Assim, o processo
```
```
de estimação pára com as três variáveis ( X 13 , X 17 e X 11 )
constituindo a função discriminante.
```
```
Resumo do processo de estimação stepwise. A Tabela
5-9 fornece os resultados gerais da análise discriminan-
te stepwise depois que todas as variáveis signifi cantes
foram incluídas na estimação da função discriminante.
Essa tabela resumo descreve as três variáveis ( X 11 , X 13 e
X 17 ) que são discriminadores signifi cantes com base em
seus lambda de Wilks e nos valores mínimos de D^2 de
Mahalanobis.
Diversos resultados distintos são dados abordando
tanto o ajuste geral do modelo quanto o impacto de va-
riáveis específi cas.
```
( _Continuação_ )

```
( Continua )
```

##### 256 Análise Multivariada de Dados

- As medidas multivariadas de ajuste geral do modelo
    são relatadas sob a legenda "Funções discriminantes
    canônicas". Observe que a função discriminante é al-
    tamente signifi cante (0,000) e retrata uma correlação
    canônica de 0,749. Interpretamos essa correlação ele-
    vando-a ao quadrado (0,749)^2 = 0,561. Logo, 56,1% da
    variância na variável dependente ( _X_ 4 ) pode ser explica-
    da por este modelo, o qual inclui apenas três variáveis
    independentes.
- Os coefi cientes padronizados da função discriminante
    são fornecidos, mas são menos preferidos para fi ns de
    interpretação do que as cargas discriminantes. Os coe-
    fi cientes discriminantes não-padronizados são usados
    para calcular os escores _Z_ discriminantes que podem
    ser empregados na classifi cação.

```
TABELA 5-7 Resultados do passo 2 da análise discriminante stepwise de dois grupos
Ajuste geral do modelo
Valor Valor F Graus de liberdade Signifi cância
Lambda de Wilks 0,478 31,129 2,57 0,000
Variáveis adicionadas/removidas no passo 2
F
Variável adicionada D^2 mínimo Valor Signifi cância Entre grupos
X 13 Flexibilidade de preço 4,300 31,129 0,000 0 e 1
Nota: Em cada passo, a variável que maximiza a distância de Mahalanobis entre os dois grupos mais próximos é adicionada.
Variáveis na análise após o passo 2
Variável Tolerância F para remover D^2 Entre grupos
X 13 Preços competitivos 1,000 20,113 2,152 0 e 1
X 17 Flexibilidade de preço 1,000 19,863 2,171 0 e 1
```
```
Variáveis fora da análise após o passo 2
Variável Tolerância Tolerância mínima F para entrar D^2 mínimo Entre grupos
X 6 Qualidade de produto 0,884 0,884 0,681 4,400 0 e 1
X 7 Atividades de comércio eletrônico 0,804 0,804 2,486 4,665 0 e 1
X 8 Suporte técnico 0,966 0,966 0,052 4,308 0 e 1
X 9 Solução de reclamação 0,610 0,610 1,479 4,517 0 e 1
X 10 Anúncio 0,901 0,901 0,881 4,429 0 e 1
X 11 Linha de produto 0,848 0,848 5,068 5,045 0 e 1
X 12 Imagem da equipe de venda 0,944 0,944 0,849 4,425 0 e 1
X 14 Garantia e reclamações 0,916 0,916 0,759 4,411 0 e 1
X 15 Novos produtos 0,986 0,986 0,017 4,302 0 e 1
X 16 Encomenda e cobrança 0,625 0,625 0,245 4,336 0 e 1
X 18 Velocidade de entrega 0,519 0,519 4,261 4,927 0 e 1
```
```
Teste de signifi cância de diferenças de grupos após o passo 2a
EUA/América do Norte
Fora da América do Norte F 32,129
Sig. 0,000
a2,57 graus de liberdade
```
- As cargas discriminantes são relatadas sob a legenda
    "Matriz estrutural" e são ordenadas da maior para a
    menor em termos de tamanho da carga. As cargas são
    discutidas depois na fase de interpretação (estágio 5).
- Os coefi cientes da função de classifi cação, também
    conhecidos como funções discriminantes lineares de
    Fisher, são utilizados na classifi cação e discutidos poste-
    riormente.
- Centróides de grupo são também relatados, e eles re-
    presentam a média dos escores individuais da função
    discriminante para cada grupo. Centróides fornecem
    uma medida resumo da posição relativa de cada grupo
    nas funções discriminantes. Neste caso, a Tabela 5-9
    revela que o centróide de grupo para as fi rmas nos
    EUA/América do Norte (grupo 0) é –1,273, enquanto
       ( _Continua_ )

```
( Continuação )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 257

Os resultados do modelo geral são aceitáveis com base
em signifi cância estatística e prática. No entanto, antes de
proceder com uma interpretação dos resultados, o pesqui-
sador precisa avaliar a precisão de classifi cação e exami-
nar os resultados caso a caso.

##### Avaliação da precisão de classifi cação

Com o modelo geral estatisticamente signifi cante e expli-
cando 56% da variação entre os grupos (ver a discussão

```
anterior e a Tabela 5-9), passamos para a avaliação de
precisão preditiva da função discriminante. Em tal pro-
cesso devemos completar três tarefas:
```
**1.** Calcular o escore de corte, o critério no qual o escore _Z_ dis-
    criminante de cada observação é julgado para determinar
    em qual grupo ela deve ser classifi cada.
**2.** Classifi car cada observação e desenvolver as matrizes de
    classifi cação para as amostras de análise e de teste.
**3.** Avaliar os níveis de precisão preditiva a partir das ma-
    trizes de classifi cação quanto a signifi cância estatística e
    prática.

```
Apesar de o exame da amostra de teste e de sua preci-
são preditiva ser realmente feito no estágio de validação,
os resultados são discutidos agora para facilitar a compa-
ração entre as amostras de estimação e de teste.
```
```
TABELA 5-8 Resultados do passo 3 da análise discriminante stepwise de dois grupos
Ajuste geral do modelo
Valor Valor F Graus de liberdade Signifi cância
Lambda de Wilks 0,438 23,923 3, 56 0,000
Variáveis adicionadas/removidas no passo 3
F
D^2 mínimo Valor Signifi cância Entre grupos
X 11 Linha de produto 5,045 23,923 0,000 0 e 1
Nota: Em cada passo, a variável que maximiza a distância de Mahalanobis entre os dois grupos mais próximos é adicionada.
Variáveis na análise após o passo 3
Variável Tolerância F para remover D^2 Entre grupos
X 13 Preços competitivos 0,849 7,258 4,015 0 e 1
X 17 Flexibilidade de preço 0,999 18,416 2,822 0 e 1
X 11 Linha de produto 0,848 5,068 4,300 0 e 1
```
```
Variáveis fora da análise após o passo 3
Variável Tolerância Tolerância mínima F para entrar D^2 mínimo Entre grupos
X 6 Qualidade de produto 0,802 0,769 0,019 5,048 0 e 1
X 7 Atividades de comércio eletrônico 0,801 0,791 2,672 5,482 0 e 1
X 8 Suporte técnico 0,961 0,832 0,004 5,046 0 e 1
X 9 Solução de reclamação 0,233 0,233 0,719 5,163 0 e 1
X 10 Anúncio 0,900 0,840 0,636 5,149 0 e 1
X 12 Imagem da equipe de venda 0,931 0,829 1,294 5,257 0 e 1
X 14 Garantia e reclamações 0,836 0,775 2,318 5,424 0 e 1
X 15 Novos produtos 0,981 0,844 0,076 5,058 0 e 1
X 16 Encomenda e cobrança 0,400 0,400 1,025 5,213 0 e 1
X 18 Velocidade de entrega 0,031 0,031 0,208 5,079 0 e 1
```
```
Teste de signifi cância de diferenças de grupos após o passo 3a
EUA/América do Norte
Fora da América do Norte F 23,923
Sig. 0,000
a3,56 graus de liberdade
```
```
o centróide para as fi rmas fora da América do Norte
(grupo 1) é 0,973. Para mostrar que a média geral é 0,
multiplique o número em cada grupo por seu centróide
e some ao resultado (p.ex., 26 × –1,273 " 34 × 0,973
! 0,0).
```
```
( Continuação )
```

##### 258 Análise Multivariada de Dados

**Cálculo do escore de corte.** O pesquisador deve primei-
ramente determinar como as probabilidades _a priori_ de
classifi cação são determinadas, ou com base nos tama-
nhos reais dos grupos (assumindo que eles são represen-
tativos da população), ou especifi cadas pelo pesquisador,
sendo que mais freqüentemente são estabelecidas como
iguais em uma postura conservadora do processo de clas-
sifi cação.

```
TABELA 5-9 Estatísticas resumo para análise discriminante de dois grupos
Ajuste geral do modelo: funções discriminantes canônicas
Percentual de variância
```
```
Função Autovalor Função % Cumulativo %
```
```
Correlação
canônica
```
```
Lambda de
Wilks
```
```
Qui-qua-
drado df Signifi cância
1 1,282 100 100 0,749 0,438 46,606 3 0,000
Função discriminante e coefi cientes da função de classifi cação
Funções discriminantes Funções de classifi cação
```
```
Variáveis independentes Não-padronizado Padronizado
```
```
Grupo 0: EUA/América
do Norte
```
```
Grupo 1: Fora da América
do Norte
X 11 Linha de produto –0,363 –0,417 7,725 6,909
X 13 Preços competitivos 0,398 0,490 6,456 7,349
X 17 Flexibilidade de preço 0,749 0,664 4,231 5,912
Constante –3,752 –52,800 –60,623
```
```
Matriz estruturala
Variáveis independentes Função 1
X 13 Preços competitivos 0,656
X 17 Flexibilidade de preço 0,653
X 11 Linha de produto –0,586
X 7 Atividades de comércio eletrônico* 0,429
X 6 Qualidade de produto* –0,418
X 14 Garantia e reclamações* –0,329
X 10 Anúncio* 0,238
X 9 Solução de reclamações* –0,181
X 12 Imagem da equipe de venda* 0,164
X 16 Encomenda e cobrança* –0,149
X 8 Suporte técnico* –0,136
X 18 Velocidade de entrega* –0,060
X 15 Novos produtos* 0,041
*Variável não usada na análise
Médias de grupos (centróides) de funções discriminantes
X 4 Região Função 1
EUA/América do Norte –1,273
Fora da América do Norte 0,973
aCorrelações internas de grupos entre variáveis discriminantes e funções discriminantes canônicas padronizadas ordenadas por tamanho absoluto de correlação
na função,
```
```
Nesta amostra de análise de 60 observações, sabemos
que a variável dependente consiste em dois grupos, 26
empresas localizadas nos EUA e 34 empresas fora do
país. Se não estamos certos de que as proporções da po-
```
```
pulação são representadas pela amostra, então devemos
empregar probabilidades iguais. No entanto, como nos-
sa amostra de empresas é aleatoriamente extraída, po-
demos estar razoavelmente certos de que essa amostra
refl ete as proporções da população. Logo, essa análise
discriminante usa as proporções da amostra para especi-
fi car as probabilidades a priori para fi ns de classifi cação.
Tendo especifi cado as probabilidades a priori , o escore
de corte ótimo pode ser calculado. Como nesta situação
os grupos são considerados representativos, o cálculo
se torna uma média ponderada dos dois centróides de
grupos:
( Continua )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 259

**Classifi cação de observações e construção de matrizes de
classifi cação.** Uma vez que o escore de corte tenha sido
calculado, cada observação pode ser classifi cada compa-
rando seu escore discriminante com o de corte.

```
O procedimento para classifi car empresas com o escore
de corte ótimo é o seguinte:
```
- Classifi que uma empresa como sendo do grupo 0 (Esta-
    dos Unidos/América do Norte) se seu escore discrimi-
    nante for menor que –0,2997.
- Classifi que uma empresa como sendo do grupo 1 (Fora
    dos Estados Unidos) se seu escore discriminante for
    maior que –0,2997.
       Matrizes de classifi cação para as observações nas
amostras de análise e de validação foram calculadas, e
os resultados são exibidos na Tabela 5-10. A amostra de
análise tem 86,7% de precisão de previsão, que é ligeira-
mente maior que a precisão de 85% da amostra de teste,
como já antecipado. Além disso, a amostra que passou
por validação cruzada conseguiu uma precisão preditiva
de 83,3%.

**Avaliação da precisão de classifi cação atingida.** Ainda
que todas as medidas de precisão de classifi cação sejam

```
bastante altas, o processo de avaliação requer uma com-
paração com a precisão de classifi cação em uma série de
medidas baseadas em chances. Essas medidas refl etem
a melhora do modelo discriminante quando se compara
com a classifi cação de indivíduos sem o uso da função dis-
criminante. Sabendo-se que a amostra geral é de 100 ob-
servações e que os grupos de teste/validação são menores
do que 20, usaremos a amostra geral para estabelecer os
padrões de comparação.
A primeira medida é o critério de chance proporcio-
nal, o qual considera que os custos da má classifi cação são
iguais (ou seja, queremos identifi car os membros de cada
grupo igualmente bem). O critério de chance proporcio-
nal é:
C PRO! p^2 " (1 $ p )^2
onde
C PRO = critério de chance proporcional
p = proporção de empresas no grupo 0
1 – p = proporção de empresas no grupo 1
```
```
O grupo de clientes localizados nos Estados Unidos
(grupo 0) constitui 39,0% da amostra de análise (39/100),
com o segundo grupo representando clientes localizados
fora dos Estados Unidos (grupo 1) formando os 61,0%
restantes. O valor calculado de chance proporcional é de
0,524 (0,390^2 " 0,610^2! 0,524).
```
```
O critério de chance máxima é simplesmente o per-
centual corretamente classifi cado se todas as observações
fossem colocadas no grupo com a maior probabilidade
de ocorrência. Ele refl ete nosso padrão mais conserva-
```
```
Substituindo os valores apropriados na fórmula, po-
demos obter o escore de corte crítico (assumindo custos
iguais de má classifi cação) de Z CS^! $0,2997.
```
```
TABELA 5-10 Resultados de classifi cação para análise discriminante de dois grupos
Resultados de classifi cação a, b, c^
Pertinência prevista em grupo
Amostra Grupo real EUA/América do Norte Fora da América do Norte Total
Amostra de estimação EUA/América do Norte 25 1 26
96,2% 3,8%
Fora da América do Norte 7 27 34
20,6% 79,4%
Amostra de validação cruzadad EUA/América do Norte 24 2 26
92,3 7,7
Fora da América do Norte 8 26 34
23,5 76,5
Amostra de teste EUA/América do Norte 9 4 13
69,2 30,8
Fora da América do Norte 2 25 27
7,4 92,6
ab86,7% dos casos originais selecionados e agrupados (amostra de estimação) corretamente classifi cados.
c85,0% dos casos originais não-selecionados e agrupados (amostra de validação) corretamente classifi cados.
d83,3% dos casos selecionados validados por cruzamento corretamente classifi cados.
Validação cruzada é feita somente para aqueles casos da análise (amostra de estimação). Em validação cruzada, cada caso é classifi cado pelas funções
derivadas de todos os casos distintos daquele.
```
```
( Continuação )
```

##### 260 Análise Multivariada de Dados

dor e assume nenhuma diferença no custo de uma má
classifi cação.

```
Como o grupo 1 (clientes fora dos Estados Unidos) é o
maior, com 61% da amostra, estaríamos corretos 61,0%
do tempo se designássemos todas as observações a esse
grupo. Se escolhemos o critério de chance máxima como
o padrão de avaliação, nosso modelo deve ter um de-
sempenho superior a 61% de precisão de classifi cação
para ser aceitável.
```
Para tentar garantir signifi cância prática, a precisão de
classifi cação alcançada deve exceder o padrão de compa-
ração escolhido em 25%. Assim, devemos selecionar um
padrão de comparação, calcular o valor de referência e
comparar com a razão de sucesso conseguida.

```
Todos os níveis de precisão de classifi cação (razões
de sucesso) excedem 85%, o que é consideravelmente
maior do que o critério de chance proporcional de 52,4%
ou mesmo do critério de chance máxima de 61,0%.
Todas as três razões também excedem o valor de refe-
rência sugerido desses valores (padrão de comparação
mais 25%), que neste caso é de 65,5% (52,4% × 1,25!
65,5%) para a chance proporcional e 76,3% (61,0% ×
1,25! 76,3%) para a chance máxima. Em todos os casos
(amostra de análise, de teste e de validação cruzada), os
níveis de precisão de classifi cação são substancialmente
maiores do que os valores de referência, indicando um
nível aceitável de precisão de classifi cação. Além disso,
a razão de sucesso para grupos individuais é considerada
adequada também.
```
A medida fi nal de precisão de classifi cação é o _Q_ de
Press, que é uma medida estatística que compara precisão
de classifi cação com um processo aleatório.

```
A partir da discussão anterior, o cálculo para a amostra
de estimação é
```
```
E o cálculo para a amostra de validação é
```
```
Em ambos os casos, os valores calculados excedem o
valor crítico de 6,63. Assim, a precisão de classifi cação para
a amostra de análise e, mais importante, para a amostra de
validação excede em um nível estatisticamente signifi cante
a precisão esperada de classifi cação por chance.
```
```
O pesquisador sempre deve lembrar de tomar cuidado
na aplicação de uma amostra de validação com pequenos
conjuntos de dados. Nesse caso, a pequena amostra de 40
para validação foi adequada, mas tamanhos maiores são
sempre mais desejáveis.
```
##### Diagnósticos por casos

```
Além dos resultados gerais, podemos examinar as obser-
vações individuais no que se refere à precisão preditiva e
identifi car especifi camente os casos mal classifi cados. Nes-
ta operação, podemos encontrar os casos específi cos mal
classifi cados para cada grupo nas amostras de análise e de
teste e ainda promover uma análise adicional na qual se
determine o perfi l dos casos mal classifi cados.
```
```
A Tabela 5-11 contém as previsões de grupo para as
amostras de análise e de validação e nos permite identifi -
car os casos específi cos para cada tipo de má classifi cação
tabulada nas matrizes de classifi cação (ver Tabela 5-10).
Para a amostra de análise, os sete clientes localizados
fora dos Estados Unidos que foram mal classifi cados no
grupo de clientes na América do Norte podem ser iden-
tifi cados como os casos 3, 94, 49, 64, 24, 53 e 32. Ana-
logamente, o único cliente dos Estados Unidos que foi
mal classifi cado é identifi cado como caso 43. Um exame
semelhante pode ser feito para a amostra de validação.
```
```
Assim que os casos mal classifi cados são identifi ca-
dos, uma análise adicional pode ser realizada para com-
preender as razões dessa má classifi cação. Na Tabela
5-12, os casos mal classifi cados são combinados a partir
das amostras de análise e de validação e então compara-
dos com os casos corretamente classifi cados. O objetivo
é identifi car diferenças específi cas nas variáveis indepen-
dentes que possam identifi car novas variáveis a serem
acrescentadas ou características em comum que devam
ser consideradas.
```
```
Os cinco casos (tanto na amostra de análise quanto na de
validação) mal classifi cados entre os clientes dos Estados
Unidos (grupo 0) têm diferenças signifi cantes em duas
das três variáveis independentes na função discriminante
( X 13 e X 17 ), bem como em uma variável não incluída na
função discriminante ( X 6 ). Para tal variável, o perfi l dos
casos mal classifi cados não é semelhante ao seu grupo
correto; logo, não ajuda na classifi cação. Analogamente,
os nove casos mal classifi cados do grupo 1 (fora dos Es-
tados Unidos) mostram quatro diferenças signifi cantes
( X 6 , X 11 , X 13 e X 17 ), mas apenas X 6 não está na função
discriminante. Podemos ver que aqui X 6 funciona contra
a precisão de classifi cação porque os casos mal classifi -
cados são mais semelhantes ao grupo incorreto do que
ao outro.
( Continua )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 261

**TABELA 5-11** Previsões de grupo para casos individuais na análise discriminante de dois grupos

```
Identifi cação
do caso Grupo real
```
```
Escore Z
discriminante Grupo previsto
```
```
Identifi cação
de caso Grupo real
```
```
Escore Z
discriminante Grupo previsto
```
**Amostra de análise**

72 0 –2,10690 0 24 1 –0,60937 0
14 0 –2,03496 0 53 1 –0,45623 0
31 0 –1,98885 0 32 1 –0,36094 0
54 0 –1,98885 0 80 1 –0,14687 1
27 0 –1,76053 0 38 1 –0,04489 1
29 0 –1,76053 0 60 1 –0,04447 1
16 0 –1,71859 0 65 1 0,09785 1
61 0 –1,71859 0 35 1 0,84464 1
79 0 –1,57916 0 1 1 0,98896 1
36 0 –1,57108 0 4 1 1,10834 1
98 0 –1,57108 0 68 1 1,12436 1
58 0 –1,48136 0 44 1 1,34768 1
45 0 –1,33840 0 17 1 1,35578 1
2 0 –1,29645 0 67 1 1,35578 1
52 0 –1,29645 0 33 1 1,42147 1
50 0 –1,24651 0 87 1 1,57544 1
47 0 –1,20903 0 6 1 1,58353 1
88 0 –1,10294 0 46 1 1,60411 1
11 0 –0,74943 0 12 1 1,75931 1
56 0 –0,73978 0 69 1 1,82233 1
95 0 –0,73978 0 86 1 1,82233 1
81 0 –0,72876 0 10 1 1,85847 1
5 0 –0,60845 0 30 1 1,90062 1
37 0 –0,60845 0 15 1 1,91724 1
63 0 –0,38398 0 92 1 1,97960 1
43 0 0,23553 1 7 1 2,09505 1
3 1 –1,65744 0 20 1 2,22839 1
94 1 –1,57916 0 8 1 2,39938 1
49 1 –1,04667 0 100 1 2,62102 1
64 1 –0,67406 0 48 1 2,90178 1

**Amostra de teste**

23 0 22,38834 0 25 1 1,47048 1
93 0 –2,03496 0 18 1 1,60411 1
59 0 –1,20903 0 73 1 1,61002 1
85 0 –1,10294 0 21 1 1,69348 1
83 0 –1,03619 0 90 1 1,69715 1
91 0 –0,89292 0 97 1 1,70398 1
82 0 –0,74943 0 40 1 1,75931 1
76 0 –0,72876 0 77 1 1,86055 1
96 0 –0,57335 0 28 1 1,97494 1
13 0 0,13119 1 71 1 2,22839 1
89 0 0,51418 1 19 1 2,28652 1
42 0 0,63440 1 57 1 2,31456 1
78 0 0,63440 1 9 1 2,36823 1
22 1 –2,73303 0 41 1 2,53652 1
74 1 –1,04667 0 26 1 2,59447 1
51 1 0,09785 1 70 1 2,59447 1
62 1 0,94702 1 66 1 2,90178 1
75 1 0,98896 1 34 1 2,97632 1
99 1 1,13130 1 55 1 2,97632 1
84 1 1,30393 1 39 1 3,21116 1


##### 262 Análise Multivariada de Dados

Pesquisadores devem examinar os padrões em ambos
os grupos com o objetivo de entender as características
comuns a eles em uma tentativa de defi nir os motivos para
a má classifi cação.

#### Estágio 5: Interpretação dos resultados

Após estimar a função, a próxima fase é a interpretação.
Este estágio envolve o exame da função para determinar

```
a importância relativa de cada variável independente na
discriminação entre os grupos, interpretar a função dis-
criminante com base nas cargas discriminantes, e então
fazer o perfi l de cada grupo sobre o padrão de valores
médios para variáveis identifi cadas como discriminadoras
importantes.
```
##### Identifi cação de variáveis discriminantes importantes

```
Como anteriormente discutido, cargas discriminantes são
consideradas a medida mais adequada de poder discrimi-
nante, mas consideraremos também os pesos discriminan-
tes para fi ns de comparação. Os pesos discriminantes, na
forma padronizada ou não, representam a contribuição
de cada variável à função discriminante. Contudo, como
discutiremos, multicolinearidade entre as variáveis inde-
pendentes pode causar impacto na interpretação usando
somente os pesos.
```
```
TABELA 5-12 Perfi l de observações corretamente classifi cadas e mal classifi cadas na análise discriminante de dois grupos
Escores médios Teste t
Variável dependente:
X 4 Região Variáveis (Grupo/Perfi l)
```
```
Corretamente
classifi cada
```
```
Mal
classifi cada Diferença
```
```
Signifi cância
estatística
EUA/América do
Norte ( n! 34) ( n! 5)
X 6 Qualidade do produto 8,612 9,340 –0,728 0,000 b
X 7 Atividades de comércio eletrônico 3,382 4,380 –0,998 0,068 b
X 8 Suporte técnico 5,759 5,280 0,479 0,487
X 9 Solução de reclamação 5,356 6,140 –0,784 0,149
X 10 Anúncio 3,597 4,700 –1,103 0,022
X 11 Linha do produto a 6,726 6,540 0,186 0,345 b
X 12 Imagem da equipe de venda 4,459 5,460 –1,001 0,018
X 13 Preços competitivos a 5,609 8,060 –2,451 0,000
X 14 Garantia e reclamações 6,215 6,060 0,155 0,677
X 15 Novos produtos 5,024 4,420 0,604 0,391
X 16 Encomenda e cobrança 4,188 4,540 –0,352 0,329
X 17 Flexibilidade de preçoa 3,568 4,480 –0,912 0,000 b
X 18 Velocidade de entrega 3,826 4,160 –0,334 0,027 b
Fora da América do
Norte ( n! 52) ( n! 9)
X 6 Qualidade do produto 6,906 9,156 –2,250 0,000
X 7 Atividades de comércio eletrônico 3,860 3,289 0,571 0,159 b
X 8 Suporte técnico 5,085 5,544 –0,460 0,423
X 9 Solução de reclamação 5,365 5,822 –0,457 0,322
X 10 Anúncio 4,229 3,922 0,307 0,470
X 11 Linha do produto a 4,954 6,833 –1,879 0,000
X 12 Imagem da equipe de venda 5,465 5,467 –1,282E$ 03 0,998
X 13 Preços competitivos a 7,960 5,833 2,126 0,000
X 14 Garantia e reclamações 5,867 6,400 –0,533 0,007 b
X 15 Novos produtos 5,194 5,778 –0,584 0,291
X 16 Encomenda e cobrança 4,267 4,533 –0,266 0,481
X 17 Flexibilidade de preçoa 5,458 3,722 1,735 0,000
X 18 Velocidade de entrega 3,881 3,989 –0,108 0,714
Nota a : Casos das amostras de análise e validação incluídos para a amostra total de 100.
bVariáveis incluídas na função discriminante.
Teste t executado com estimativas separadas de variância no lugar de uma estimativa coletiva, pois o teste Levene detectou diferenças signifi cantes nas variações
entre os dois grupos.
```
```
As descobertas sugerem que os casos mal classifi -
cados podem representar um terceiro grupo, pois eles
compartilham perfi s muito semelhantes nessas variáveis,
mais do que acontece nos dois grupos existentes. A ad-
ministração pode analisar esse grupo quanto a variáveis
adicionais ou avaliar se um padrão geográfi co entre os
casos mal classifi cados justifi ca um terceiro grupo.
```
```
( Continuação )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 263

Cargas discriminantes são calculadas para cada va-
riável independente, mesmo para aquelas que não estão
incluídas na função discriminante. Assim, pesos* discri-
minantes representam o único impacto de cada variável
independente e não são restritas apenas ao impacto com-
partilhado devido à multicolinearidade. Além disso, como
elas são relativamente pouco afetadas pela multicolineari-
dade, elas representam mais precisamente a associação de
cada variável com o escore discriminante.

```
A Tabela 5-13 contém o conjunto inteiro de medidas
interpretativas, incluindo pesos discriminantes padro-
nizados e não-padronizados, cargas para a função dis-
criminante, lambda de Wilks e a razão F univariada. As
13 variáveis independentes originais foram examinadas
pelo procedimento stepwise , e três ( X 11 , X 13 e X 17 ) são
sufi cientemente signifi cantes para serem incluídas na
função. Para fi ns de interpretação, ordenamos as variá-
veis independentes em termos de suas cargas e valores F
univariados – ambos indicadores do poder discriminante
de cada variável. Sinais dos pesos ou cargas não afetam a
ordem; eles simplesmente indicam uma relação positiva
ou negativa com a variável dependente.
```
**Análise de lambda de Wilks e o** **_F_** **univariado.** O lambda
de Wilks e o _F_ univariado representam os efeitos sepa-
rados ou univariados de cada variável, não consideran-
do multicolinearidade entre as variáveis independentes.
Análogos às correlações bivariadas da regressão múltipla,
eles indicam a habilidade de cada variável para discrimi-
nar entre os grupos, mas apenas separadamente. Para in-
terpretar qualquer combinação de duas ou mais variáveis

```
independentes, exige-se análise dos pesos ou cargas dis-
criminantes como descrito nas próximas seções.
```
```
A Tabela 5-13 mostra que as variáveis ( X 11 , X 13 e X 17 ) com
os três maiores valores F (e os menores lambdas de Wi-
lks) eram também as variáveis que entraram na função
discriminante. X 6 , porém, tinha um efeito discriminante
signifi cante quando considerada separadamente, mas tal
efeito era compartilhado com as outras três variáveis, de
maneira que sozinha ela não contribuía sufi cientemente
para entrar na função discriminante. Todas as demais va-
riáveis tinham valores F não-signifi cantes e valores lamb-
da de Wilks correspondentemente elevados.
```
```
Análise dos pesos discriminantes. Os pesos discrimi-
nantes estão disponíveis em formas não-padronizadas
e padronizadas. Os pesos não-padronizados (mais a
constante) são usados para calcular o escore discrimi-
nante, mas podem ser afetados pela escala da variável
independente (exatamente como pesos de regressão
múltipla). Assim, os pesos padronizados refl etem mais
verdadeiramente o impacto de cada variável sobre a fun-
ção discriminante e são mais apropriados para fi ns de
interpretação. Se for usada estimação simultânea, mul-
ticolinearidade entre quaisquer variáveis independentes
causará impacto sobre os pesos estimados. No entanto, o
impacto da multicolinearidade pode ser até maior para o
procedimento stepwise , pois ela afeta não somente os pe-
sos mas pode também impedir que uma variável sequer
entre na equação.
```
```
TABELA 5-13 Resumo de medidas interpretativas para análise discriminante de dois grupos
```
```
Coefi cientes discriminantes Cargas discriminantes
```
```
Lambda
de Wilks Razão F univariada
```
```
Variáveis independentes
```
```
Não padroni-
zados Padronizados Carga Ordenação Valor Valor F Sig. Ordenação
X 6 Qualidade do produto NI NI –0,418 5 0,801 14,387 0,000 4
X 7 Atividades de comércio
eletrônico
```
```
NI NI 0,429 4 0,966 2,054 0,157 6
```
```
X 8 Suporte técnico NI NI –0,136 11 0,973 1,598 0,211 7
X 9 Solução de reclamação NI NI –0,181 8 0,986 0,849 0,361 8
X 10 Anúncio NI NI 0,238 7 0,987 0,775 0,382 9
X 11 Linha do produto –0,363 –0,417 –0,586 3 0,695 25,500 0,000 3
X 12 Imagem da equipe de venda NI NI 0,164 9 0,856 9,733 0,003 5
X 13 Preços competitivos 0,398 0,490 0,656 1 0,645 31,992 0,000 1
X 14 Garantia e reclamações NI NI –0,329 6 0,992 0,453 0,503 11
X 15 Novos produtos NI NI 0,041 13 0,990 0,600 0,442 10
X 16 Encomenda e cobrança NI NI –0,149 10 0,999 0,087 0,769 13
X 17 Flexibilidade de preço 0,749 0,664 0,653 2 0,647 31,699 0,000 2
X 18 Velocidade de entrega NI NI –0,060 12 0,997 0,152 0,698 12
NI = Não incluído na função discriminante estimada
```
A Tabela 5-13 fornece os pesos padronizados (coefi cien-
tes) para as três variáveis incluídas na função discrimi-
* N. de R. T.: A palavra correta seria “cargas”.


##### 264 Análise Multivariada de Dados

##### Interpretação da função discriminante

##### com base nas cargas discriminantes

As cargas discriminantes, em contraste com os pesos dis-
criminantes, são menos afetadas pela multicolinearidade e,
portanto, mais úteis para a interpretação. Além disso, como
cargas são calculadas para todas as variáveis, elas fornecem
uma medida interpretativa até mesmo para variáveis não
incluídas na função discriminante. Uma regra prática ante-
rior indicava que cargas acima de ± 0,40 deveriam ser usa-
das para identifi car variáveis discriminantes importantes.

```
As cargas das três variáveis da função discriminante (ver
Tabela 5-13) são as três maiores, e todas excedem ± 0,40,
garantindo assim inclusão no processo de interpretação.
Duas variáveis adicionais ( X 6 e X 7 ), porém, também têm
cargas acima da referência ± 0,40. A inclusão de X 6 não é
inesperada, como era a quarta variável com efeito discri-
minante univariado, mas não foi incluída na função dis-
criminante devido à multicolinearidade (como mostrado
no Capítulo 3, Análise Fatorial, onde X 6 e X 13 formavam
um fator). X 7 , porém, apresenta outra situação; ela não
tinha um efeito univariado signifi cante. A combinação
das três variáveis na função discriminante criou um efeito
que é associado com X 7 , mas X 7 não acrescenta qualquer
poder discriminante adicional. Com relação a isso, X 7 é
descritiva da função discriminante mesmo não sendo in-
cluída nem tendo um efeito univariado signifi cante.
```
Interpretar a função discriminante e sua discriminação
entre esses dois grupos exige que o pesquisador considere
todas essas cinco variáveis. Na medida em que elas carac-
terizam ou descrevem a função discriminante, todas re-
presentam algum componente da mesma.
Com as variáveis discriminantes identifi cadas e a função
discriminante descrita em termos daquelas variáveis com

```
cargas sufi cientemente elevadas, o pesquisador prossegue
então para o perfi l de cada grupo sobre essas variáveis
para compreender as diferenças entre as mesmas.
```
##### Perfi l das variáveis discriminantes

```
O pesquisador está interessado em interpretações das va-
riáveis individuais que têm signifi cância estatística e prá-
tica. Tais interpretações são conseguidas primeiramente
identifi cando-se as variáveis com substantivo poder dis-
criminatório (ver a discussão anterior) e em seguida en-
tendendo-se o que o grupo distinto diz cada variável in-
dicada.
```
```
Como descrito no Capítulo 1, escores maiores nas variá-
veis independentes indicam percepções mais favoráveis
da HBAT sobre aquele atributo (exceto para X 13 , onde
escores menores são preferíveis). Retornando à Tabela
5-5, vemos diversos perfi s entre os dois grupos sobre es-
sas cinco variáveis.
```
- O grupo 0 (clientes nos Estados Unidos/América do
    Norte) têm percepções maiores sobre três variáveis: _X_ 6
    (Qualidade do produto), _X_ 13 * (Preços competitivos) e
    _X_ 11 (Linha do produto).
- O grupo 1 (clientes fora da América do Norte) têm
    percepções maiores nas outras duas variáveis: _X_ 7 (Ati-
    vidades de comércio eletrônico) e _X_ 17 (Flexibilidade de
    preço).
       Olhando esses dois perfi s, podemos perceber que os
clientes dos EUA/América do Norte têm percepções
muito melhores dos produtos HBAT, enquanto os de-
mais clientes se sentem melhor com questões sobre pre-
ço e comércio eletrônico. Note que _X_ 6 e _X_ 13 , ambas com
percepções mais elevadas entre os clientes dos EUA/
América do Norte, formam o fator Valor do produto
desenvolvido no Capítulo 3. A administração deveria
usar esses resultados para desenvolver estratégias que
acentuem esses pontos fortes e desenvolver outras van-
tagens para fi ns de complementação.
    O perfi l médio também ilustra a interpretação dos
sinais (positivos e negativos) nos pesos e as cargas dis-
criminantes. Os sinais refl etem o perfi l médio relativo
dos dois grupos. Os sinais positivos, neste exemplo, são
associados com variáveis que têm escores maiores para
o grupo 1. Os pesos e cargas negativas são para aque-
las variáveis com o padrão oposto (i.e., valores maiores
no grupo 0). Logo, os sinais indicam o padrão entre os
grupos.

```
nante. O impacto da multicolinearidade sobre os pesos
pode ser visto ao se examinar X 13 e X 17. Essas duas variá-
veis têm poder discriminante essencialmente equivalen-
te quando vistas nos testes lambda de Wilks e F univa-
riado. Seus pesos discriminantes, contudo, refl etem um
impacto sensivelmente maior para X 17 do que para X 13 ,
que agora é mais comparável com X 11. Essa mudança em
importância relativa é devida à multicolinearidade entre
X 13 e X 11 , o que reduz o efeito único de X 13 e assim dimi-
nui os pesos discriminantes também.
```
```
Os três efeitos mais fortes na função discriminante, que
são geralmente comparáveis com base nos valores de car-
ga, são X 13 (Preços competitivos), X 17 (Flexibilidade de
preço) e X 11 (Linha do produto). X 7 (Atividades de co-
mércio eletrônico) e o efeito de X 6 (Qualidade do produ-
to) podem ser adicionados aos efeitos de X 13. Obviamente,
```
```
diversos fatores diferentes estão sendo combinados para
diferenciar entre os grupos, exigindo assim mais defi nição
de perfi l dos grupos para se entenderem as diferenças.
```
```
* N. de R. T.: A tabela indica o contrário, ou seja, a média de X 13 é
maior no grupo 1 (7,418 versus 5,600).
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 265

#### Estágio 6: Validação dos resultados

O estágio fi nal aborda a validade interna e externa da fun-
ção discriminante. O principal meio de validação é pelo
uso da amostra de validação e a avaliação de sua precisão
preditiva. Desse modo, a validade é estabelecida se a fun-
ção discriminante classifi ca, em um nível aceitável, obser-
vações que não foram usadas no processo de estimação.
Se a amostra de validação é obtida a partir da amostra
original, então essa abordagem estabelece validade inter-
na. Se uma outra amostra separada, talvez de uma outra
população ou de outro segmento da população, forma a
amostra de validação, então isso corresponde a uma vali-
dação externa dos resultados discriminantes.

```
Em nosso exemplo, a amostra de teste surge a partir da
amostra original. Como anteriormente discutido, a preci-
são de classifi cação (razões de sucesso) para as amostras
de teste e de validação cruzada estava muito acima das
referências em todas as medidas de precisão preditiva.
Como tal, a análise estabelece validade interna. Para o
propósito de validade externa, amostras adicionais de-
vem ser extraídas de populações relevantes e a precisão
de classifi cação deve ser avaliada em tantas situações
quanto possível.
```
O pesquisador é encorajado a estender o processo de
validação por meio de perfi s expandidos dos grupos e o
possível uso de amostras adicionais para estabelecer a va-
lidade externa. Idéias adicionais da análise de casos mal
classifi cados podem sugerir variáveis extras que podem
melhorar ainda mais o modelo discriminante.

#### Uma visão gerencial

A análise discriminante de clientes HBAT, baseada em
localização geográfi ca (dentro ou fora da América do
Norte), identifi cou um conjunto de diferenças em percep-
ção que pode fornecer uma distinção mais sucinta e pode-
rosa entre os dois grupos. Várias descobertas importantes
incluem as seguintes:

#### UM EXEMPLO ILUSTRATIVO

#### DE TRÊS GRUPOS

```
Para ilustrar a aplicação de uma análise discriminante de
três grupos, novamente usamos a base de dados HBAT.
No exemplo anterior, estávamos interessados na discrimi-
nação entre apenas dois grupos, de modo que conseguimos
desenvolver uma única função discriminante e um escore
de corte para dividir os dois grupos. No exemplo de três
grupos, é necessário desenvolver duas funções discriminan-
tes separadas para distinguir entre os três grupos. A pri-
meira função separa um grupo dos outros dois, e a segunda
separa os dois grupos restantes. Como no exemplo ante-
rior, os seis estágios do processo de construção do modelo
são discutidos.
```
#### Estágio 1: Objetivos da análise discriminante

```
O objetivo da HBAT nessa pesquisa é determinar a relação
entre as percepções que as empresas têm da HBAT e o pe-
ríodo de tempo em que uma empresa é cliente de HBAT.
```
- Diferenças são encontradas em um subconjunto de ape-
    nas cinco percepções, o que permite uma concentração
    sobre as variáveis-chave, não tendo que se lidar com o
    conjunto inteiro. As variáveis identifi cadas como discri-
    minantes entre os grupos (listadas em ordem de impor-
    tância) são _X_ 13 (Preços competitivos), _X_ 17 (Flexibilidade
    de preço), _X_ 11 (Linha do produto), _X_ 7 (Atividades de
    comércio eletrônico) e _X_ 6 (Qualidade do produto).
- Os resultados também indicam que as empresas loca-
    lizadas nos Estados Unidos têm melhores percepções
    da HBAT do que suas contrapartes internacionais em
    termos de valor e linha de produto, enquanto os clientes
    que não são norte-americanos têm uma percepção mais
    favorável sobre fl exibilidade de preço e atividades de

```
comércio eletrônico. Essas percepções podem resultar
de uma maior similaridade entre compradores norte-
americanos, enquanto clientes internacionais acham a
política de preços em sintonia com suas necessidades.
```
- Os resultados, que são altamente signifi cantes, forne-
    cem ao pesquisador a habilidade de identifi car correta-
    mente a estratégia de compra usada, com base nessas
    percepções, 85% do tempo. Esse elevado grau de con-
    sistência gera confi ança no desenvolvimento de estraté-
    gias baseadas em tais resultados.
- A análise das empresas mal classifi cadas revelou um pe-
    queno número de empresas que pareciam “deslocadas”.
    Identifi car tais empresas pode identifi car associações
    não tratadas por localização geográfi ca (p.ex., mercados
    no lugar de apenas localização física) ou outras caracte-
    rísticas de fi rmas ou de mercado que são associadas com
    localização geográfi ca.
       Portanto, conhecer a localização de uma fi rma dá
idéias-chave sobre suas percepções da HBAT e, mais im-
portante, como os dois grupos de clientes diferem, de for-
ma que a administração pode empregar uma estratégia
para acentuar as percepções positivas em suas negocia-
ções com esses clientes e assim solidifi car sua posição.

```
Um dos paradigmas emergentes em marketing é o con-
ceito de uma relação com cliente, baseada no estabeleci-
mento de uma mútua parceria entre empresas ao longo
de repetidas transações. O processo de desenvolvimento
de uma relação implica a formação de metas e valores
compartilhados, que devem coincidir com percepções
melhoradas de HBAT. Portanto, a formação bem-suce-
dida de uma relação deve ser entendida por meio de per-
( Continua )
```

##### 266 Análise Multivariada de Dados

#### Estágio 2: Projeto de pesquisa

#### para análise discriminante

Para testar essa relação, uma análise discriminante é exe-
cutada para estabelecer se existem diferenças em percep-
ções entre grupos de clientes com base na extensão da
relação de clientela. Se for o caso, a HBAT estará então
interessada em ver se diferentes perfi s justifi cam a propo-
sição de que a HBAT teve sucesso no melhoramento de
percepções entre clientes estabelecidos, um passo neces-
sário na formação de relações com a clientela.

##### Seleção de variáveis dependente e independentes

Além das variáveis dependentes não-métricas (categóri-
cas) defi nindo grupos de interesse, a análise discriminante
também requer um conjunto de variáveis independentes
métricas que são consideradas fornecedoras de base para
discriminação ou diferenciação entre os grupos.

```
Uma análise discriminante de três grupos é realizada
usando X 1 (Tipo de cliente) como a variável dependente
e as percepções de HBAT por parte dessas fi rmas (X 6 a
X 18 ) como as variáveis independentes. Note que X 1 dife-
re da variável dependente no exemplo de dois grupos no
sentido de que ela tem três categorias nas quais classifi -
car o tempo de permanência como cliente de HBAT (1 =
menos que 1 ano, 2 = 1 a 5 anos, e 3 = mais de 5 anos).
```
##### Tamanho amostral e divisão da amostra

Questões relativas ao tamanho da amostra são particular-
mente importantes com análise discriminante devido ao
foco não apenas no tamanho geral da amostra, mas tam-
bém no tamanho amostral por grupo. Juntamente com a
necessidade de uma divisão da amostra para obter uma
amostra de validação, o pesquisador deve considerar cui-
dadosamente o impacto da divisão amostral em termos do
tamanho geral e do tamanho de cada um dos grupos.

#### Estágio 3: Suposições da análise discriminante

```
Como no caso do exemplo de dois grupos, as suposições
de normalidade, linearidade e colinearidade das variáveis
independentes já foram discutidas detalhadamente no Ca-
pítulo 2. A análise feita no Capítulo 2 indicou que as va-
riáveis independentes atendem essas suposições em níveis
adequados para viabilizar a continuidade da análise sem
ações corretivas adicionais. A suposição remanescente, a
igualdade de matrizes de variância/covariância ou de dis-
persão, também é abordada no Capítulo 2.
```
```
O teste M de Box avalia a similaridade das matrizes de
dispersão das variáveis independentes entre os três gru-
pos (categorias). O teste estatístico indicou diferenças
no nível de signifi cância de 0,09. Neste caso, as diferen-
ças entre grupos são não-signifi cantes e nenhuma ação
corretiva se faz necessária. Além disso, não se espera
qualquer impacto sobre os processos de estimação e
classifi cação.
```
#### Estágio 4: Estimação do modelo

#### discriminante e avaliação do ajuste geral

```
Como no exemplo anterior, começamos nossa análise revi-
sando as médias de grupo e os desvios-padrão para ver se os
grupos são signifi cantemente diferentes em alguma variável.
Com essas diferenças em mente, empregamos em seguida
um processo de estimação stepwise para obter as funções
discriminantes e completamos o processo avaliando preci-
são de classifi cação com diagnósticos gerais e por casos.
```
##### Avaliação de diferenças de grupos

```
Identifi car as variáveis mais discriminantes com três ou
mais grupos é mais problemático do que na situação com
dois grupos. Para três ou mais grupos, as medidas típicas
de signifi cância para diferenças em grupos (ou seja, lamb-
da de Wilks e o teste F ) avaliam apenas as diferenças ge-
rais e não garantem que cada grupo é signifi cante em rela-
ção aos demais. Assim, quando examinar variáveis quanto
a suas diferenças gerais entre os grupos, certifi que-se tam-
bém de tratar das diferenças individuais de grupos.
```
```
cepções melhores de HBAT ao longo do tempo. Nessa
análise, as fi rmas são agrupadas conforme sua situação
como clientes HBAT. Se HBAT foi bem-sucedida no
estabelecimento de relações com seus clientes, então as
percepções sobre a HBAT irão melhorar em cada situa-
ção como cliente HBAT.
```
```
A base de dados da HBAT tem uma amostra de 100, a
qual será novamente particionada em amostras de aná-
lise e de validação de 60 e 40 casos, respectivamente. Na
amostra de análise, a proporção de casos por variáveis
independentes é quase 5:1, o limite inferior recomenda-
do. Mais importante, na amostra de análise, apenas um
grupo, com 13 observações, fi ca abaixo do nível reco-
mendado de 20 casos por grupo. Apesar de o tamanho
```
```
do grupo exceder 20 se a amostra inteira for usada na
fase de análise, a necessidade de validação dita a criação
da amostra de teste. Os três grupos são de tamanhos re-
lativamente iguais (22, 13 e 25), evitando assim qualquer
necessidade de igualar os tamanhos dos grupos. A análi-
se procede com atenção para a classifi cação e interpreta-
ção desse pequeno grupo de 13 observações.
```
```
A Tabela 5-14 dá as médias de grupos, lambda de Wilks,
razões F univariadas (ANOVAs simples) e D^2 mínimo
( Continua )
```
```
( Continuação )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 267

```
Todas essas medidas se combinam para ajudar a iden-
tifi car os conjuntos de variáveis que formam as funções
discriminantes, como descritos na próxima seção. Quando
mais de uma função é criada, cada uma fornece discrimi-
nação entre conjuntos de grupos. No exemplo simples do
início deste capítulo, uma variável discriminou entre os
grupos 1 versus 2 e 3, sendo que a outra discriminou entre
os grupos 2 versus 3 e 1. Esse é um dos principais benefí-
cios que surgem do uso da análise discriminante.
```
##### Estimação da função discriminante

```
O procedimento stepwise é realizado da mesma manei-
ra do exemplo de dois grupos, com todas as variáveis ini-
cialmente excluídas do modelo. O procedimento então se-
leciona a variável que tem uma diferença estatisticamente
signifi cante nos grupos enquanto maximiza a distância de
Mahalanobis ( D^2 ) entre os dois grupos mais próximos.
Desta maneira, variáveis estatisticamente signifi cantes
são selecionadas de modo a maximizarem a discriminação
entre os grupos mais semelhantes em cada estágio.
Este processo continua enquanto variáveis adicionais
fornecerem discriminação estatisticamente signifi cante
além daquelas diferenças já explicadas pelas variáveis na
função discriminante. Uma variável pode ser removida se
alta multicolinearidade com variáveis independentes na
função discriminante faz com que sua signifi cância caia
abaixo do nível para remoção (0,10).
```
```
de Mahalanobis para cada variável independente. A re-
visão dessas medidas revela o seguinte:
```
- Sobre uma base univariada, aproximadamente metade
    (7 entre 13) das variáveis exibe diferenças signifi cantes
    entre as médias dos grupos. As variáveis com diferenças
    signifi cantes incluem _X_ 6 , _X_ 9 , _X_ 11 , _X_ 13 , _X_ 16 , _X_ 17 e _X_ 18.
- Apesar de maior signifi cância estatística corresponder
    a uma maior discriminação geral (ou seja, as variáveis
    mais signifi cantes têm os menores lambdas de Wilks),
    ela nem sempre corresponde à maior discriminação en-
    tre todos os grupos.
    - A inspeção visual das médias dos grupos revela que
       quatro das variáveis com diferenças signifi cantes
       ( _X_ 13 , _X_ 16 , _X_ 17 e _X_ 18 ) diferenciam apenas um grupo
       versus os outros dois grupos [p.ex., _X_ 18 tem
       diferenças signifi cantes somente nas médias entre o
       grupo 1 (3,059) versus grupos 2 (4,246) e 3 (4,288)].
       Essas variáveis têm um papel limitado em análise
       discriminante por fornecerem discriminação apenas
       em um subconjunto de grupos.
    - Três variáveis ( _X_ 6 , _X_ 9 e _X_ 11 ) fornecem alguma
       discriminação, em vários graus, entre todos os grupos
       simultaneamente. Uma ou mais dessas variáveis
       podem ser usadas em combinação com as quatro
       variáveis precedentes para criar uma variável
       estatística com discriminação máxima.
- O valor _D_^2 de Mahalanobis fornece uma medida do
    grau de discriminação entre grupos. Para cada variável,
    o _D_^2 mínimo de Mahalanobis é a distância entre os dois
    grupos mais próximos. Por exemplo, _X_ 11 tem o maior
    valor _D_^2 e é a variável com as maiores diferenças entre
    todos os três grupos. Analogamente, _X_ 18 , uma variável
    com pequenas diferenças entre dois dos grupos, tem um
    pequeno valor _D_^2. Com três ou mais grupos, o _D_^2 mí-

```
TABELA 5-14 Estatísticas descritivas de grupos e testes de igualdade para a amostra de estimação na análise discriminante de três grupos
Médias de grupo da variável
dependente: X 1 Tipo de cliente
```
```
Teste de igualdade de
médias de gruposa
```
```
D^2 mínimo de
Mahalanobis
```
```
Variáveis independentes
```
```
Grupo 1:
Menos que 1
ano ( n = 22)
```
```
Grupo 2: 1
a 5 anos
( n = 13)
```
```
Grupo 3:
Mais de 5
anos ( n = 25)
```
```
Lambda
de Wilks Valor F Signifi cância D^2 mínimo
```
```
Entre
grupos
X 6 Qualidade do produto 7,118 6,785 9,000 0,469 32,311 0,000 0,121 1 e 2
X 7 Atividades de comércio ele-
trônico
```
```
3,514 3,754 3,412 0,959 1,221 0,303 0,025 1 e 3
```
```
X 8 Suporte técnico 4,959 5,615 5,376 0,973 0,782 0,462 0,023 2 e 3
X 9 Solução de reclamação 4,064 5,900 6,300 0,414 40,292 0,000 0,205 2 e 3
X 10 Anúncio 3,745 4,277 3,768 0,961 1,147 0,325 0,000 1 e 3
X 11 Linha do produto 4,855 5,577 7,056 0,467 32,583 0,000 0,579 1 e 2
X 12 Imagem da equipe de venda 4,673 5,346 4,836 0,943 1,708 0,190 0,024 1 e 3
X 13 Preços competitivos 7,345 7,123 5,744 0,751 9,432 0,000 0,027 1 e 2
X 14 Garantia e reclamações 5,705 6,246 6,072 0,916 2,619 0,082 0,057 2 e 3
X 15 Novos produtos 4,986 5,092 5,292 0,992 0,216 0,807 0,004 1 e 2
X 16 Encomenda e cobrança 3,291 4,715 4,700 0,532 25,048 0,000 0,000 2 e 3
X 17 Flexibilidade de preço 4,018 5,508 4,084 0,694 12,551 0,000 0,005 1 e 3
X 18 Velocidade de entrega 3,059 4,246 4,288 0,415 40,176 0,000 0,007 2 e 3
aLambda de Wilks (estatística U ) e razão F univariada com 2 e 57 graus de liberdade.
```
```
nimo de Mahalanobis é importante na identifi cação da
variável que dá a maior diferença entre os dois grupos
mais parecidos.
```
( _Continuação_ )


##### 268 Análise Multivariada de Dados

```
Estimação stepwise : adição da primeira variável,
X 11. Os dados na Tabela 5-14 mostram que a primeira
variável a entrar no modelo é X 11 (Linha do produto),
pois ela atende aos critérios para diferenças estatistica-
mente signifi cantes nos grupos e tem o maior valor D^2 (o
que signifi ca que ela tem a maior separação entre os dois
grupos mais parecidos).
Os resultados de adicionar X 11 como a primeira va-
riável no processo stepwise são mostrados na Tabela
5-15. O ajuste geral do modelo é signifi cante e todos os
grupos são signifi cantemente distintos, apesar de os gru-
pos 1 (menos de um ano) e 2 (de um a cinco anos) terem
```
```
a menor diferença entre eles (ver seção abaixo detalhan-
do as diferenças de grupos).
Com a menor diferença entre os grupos 1 e 2, o pro-
cedimento discriminante selecionará agora uma variável
que maximiza aquela diferença enquanto pelo menos
mantém as demais. Se voltarmos à Tabela 5-14, perce-
beremos que quatro variáveis ( X 9 , X 16 , X 17 e X 18 ) tinham
diferenças signifi cantes, com substanciais distinções en-
tre os grupos 1 e 2. Olhando a Tabela 5-15, vemos que
essas quatro variáveis têm o maior valor D^2 mínimo, e
em cada caso é para a diferença entre os grupos 2 e 3
(o que signifi ca que os grupos 1 e 2 não são os mais pa-
```
```
TABELA 5-15 Resultados do passo 1 da análise discriminante stepwise de três grupos
Ajuste geral do modelo
Valor Valor F Graus de liberdade Signifi cância
Lambda de Wilks 0,467 32,583 2,57 0,000
Variável adicionada/removida no passo 1
F
Variável adicionada D^2 mínimo Valor Signifi cância Entre grupos
X 11 Linha de produto 0,579 4,729 0,000 Menos de 1 ano e de 1 a 5 anos
Nota : Em cada passo, a variável que maximiza a distância Mahalanobis entre os dois grupos mais próximos é adicionada.
Variáveis na análise após o passo 1
Variável Tolerância F para remover D^2 Entre grupos
X 11 Linha de produto 1,000 32,583 NA NA
NA = Não aplicável
Variáveis fora da análise após o passo 1
Variável Tolerância Tolerância mínima F para entrar D^2 mínimo Entre grupos
X 6 Qualidade de produto 1,000 1,000 17,426 0,698 Menos de 1 ano e de 1 a 5 anos
X 7 Atividades de comércio eletrônico 0,950 0,950 1,171 0,892 Menos de 1 ano e de 1 a 5 anos
X 8 Suporte técnico 0,959 0,959 0,733 0,649 Menos de 1 ano e de 1 a 5 anos
X 9 Solução de reclamação 0,847 0,847 15,446 2,455 De 1 a 5 anos e mais de 5 anos
X 10 Anúncio 0,998 0,998 1,113 0,850 Menos de 1 ano e de 1 a 5 anos
X 12 Imagem da equipe de venda 0,932 0,932 3,076 1,328 Menos de 1 ano e de 1 a 5 anos
X 13 Preços competitivos 0,882 0,882 2,299 0,839 Menos de 1 ano e de 1 a 5 anos
X 14 Garantia e reclamações 0,849 0,849 0,647 0,599 Menos de 1 ano e de 1 a 5 anos
X 15 Novos produtos 0,993 0,993 0,415 0,596 Menos de 1 ano e de 1 a 5 anos
X 16 Encomenda e cobrança 0,943 0,943 12,176 2,590 De 1 a 5 anos e mais de 5 anos
X 17 Flexibilidade de preço 0,807 0,807 17,300 3,322 De 1 a 5 anos e mais de 5 anos
X 18 Velocidade de entrega 0,773 0,773 19,020 2,988 De 1 a 5 anos e mais de 5 anos
```
```
Teste de signifi cância de diferenças de grupos após o passo 1a
X 1 Tipo de cliente Menos de 1 ano De 1 a 5 anos
De 1 a 5 anos F 4,729
Sig. 0,034
Mais de 5 anos F 62,893 20,749
Sig. 0,000 0,000
a1 e 57 graus de liberdade.
```
```
( Continua )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 269

```
recidos depois de acrescentar aquela variável). Assim,
adicionar qualquer uma dessas variáveis afeta muito as
diferenças entre os grupos 1 e 2, o par que era mais pa-
recido depois que X 11 foi adicionada no primeiro passo.
O procedimento escolherá X 17 porque ela criará a maior
distância entre os grupos 2 e 3.
```
```
Estimação stepwise : Adição da segunda variável,
X 17. A Tabela 5-16 detalha o segundo passo do proce-
dimento stepwise : o acréscimo de X 17 (Flexibilidade de
```
```
preço) à função discriminante. A discriminação entre
grupos aumentou, como refl etido em um menor valor
lambda de Wilks e no aumento do D^2 mínimo (de 0,467
para 0,288). As diferenças de grupos, geral e individuais,
ainda são estatisticamente signifi cantes. O acréscimo de
X 17 aumentou as distinções entre os grupos 1 e 2 consi-
deravelmente, de forma que agora os dois grupos mais
parecidos são 2 e 3.
Das variáveis fora da equação, apenas X 6 (Qualidade
de produto) satisfaz o nível de signifi cância necessário
```
```
TABELA 5-16 Resultados do passo 2 da análise discriminante stepwise de três grupos
Ajuste geral do modelo
Valor Valor F Graus de liberdade Signifi cância
Lambda de Wilks 0,288 24,139 4, 112 0,000
Variável adicionada/removida no passo 2
F
Variável adicionada D^2 mínimo Valor Signifi cância Entre grupos
X 17 Flexibilidade de preço 3,322 13,958 0,000 De 1 a 5 anos e mais de 5 anos
Nota: Em cada passo, a variável que maximiza a distância Mahalanobis entre os dois grupos mais próximos é adicionada.
Variáveis na análise após o passo 2
Variável Tolerância F para remover D^2 Entre grupos
X 11 Linha de produto 0,807 39,405 0,005 Menos de 1 ano e mais de 5 anos
X 17 Flexibilidade de preço 0,807 17,300 0,579 Menos de 1 ano e de 1 a 5 anos
```
```
Variáveis fora da análise após o passo 2
Variável TolerânciaTolerância mínima F para entrar D^2 mínimo Entre grupos
X 6 Qualidade de produto 0,730 0,589 24,444 6,071 Menos de 1 ano e de 1 a 5 anos
X 7 Atividades de comércio eletrônico 0,880 0,747 0,014 3,327 Menos de 1 ano e de 1 a 5 anos
X 8 Suporte técnico 0,949 0,791 1,023 3,655 Menos de 1 ano e de 1 a 5 anos
X 9 Solução de reclamação 0,520 0,475 3,932 3,608 Menos de 1 ano e de 1 a 5 anos
X 10 Anúncio 0,935 0,756 0,102 3,348 Menos de 1 ano e de 1 a 5 anos
X 12 Imagem da equipe de venda 0,884 0,765 0,662 3,342 Menos de 1 ano e de 1 a 5 anos
X 13 Preços competitivos 0,794 0,750 0,989 3,372 Menos de 1 ano e de 1 a 5 anos
X 14 Garantia e reclamações 0,868 0,750 2,733 4,225 Menos de 1 ano e de 1 a 5 anos
X 15 Novos produtos 0,963 0,782 0,504 3,505 Menos de 1 ano e de 1 a 5 anos
X 16 Encomenda e cobrança 0,754 0,645 2,456 3,323 Menos de 1 ano e de 1 a 5 anos
X 18 Velocidade de entrega 0,067 0,067 3,255 3,598 Menos de 1 ano e de 1 a 5 anos
```
```
Teste de signifi cância de diferenças de grupos após o passo 2a
X 1 Tipo de cliente Menos de 1 ano De 1 a 5 anos
De 1 a 5 anos F 21,054
Sig. 0,000
Mais de 5 anos F 39,360 13,958
Sig. 0,000 0,000
a2 e 56 graus de liberdade.
```
( _Continuação_ )

```
( Continua )
```

##### 270 Análise Multivariada de Dados

```
para consideração. Se acrescentada, o D^2 mínimo será
agora entre os grupos 1 e 2.
```
```
Estimação stepwise : Adição das terceira e quarta variá-
veis, X 6 e X 18. Como anteriormente observado, X 6 se
torna a terceira variável adicionada à função discrimi-
nante. Depois que X 6 foi acrescentada, apenas X 18 exibe
uma signifi cância estatística nos grupos ( Nota : Os deta-
lhes sobre o acréscimo de X 6 no terceiro passo não são
mostrados por questão de espaço).
```
```
A variável fi nal adicionada no passo 4 é X 18 (ver Ta-
bela 5-17), com a função discriminante incluindo agora
quatro variáveis ( X 11 , X 17 , X 6 e X 18 ). O modelo geral é
signifi cante, com o lambda de Wilks diminuindo para
0,127. Além disso, existem diferenças signifi cantes entre
todos os grupos individuais.
Com essas quatro variáveis na função discriminante,
nenhuma outra variável exibe a signifi cância estatísti-
ca necessária para inclusão, e o processo stepwise está
```
```
TABELA 5-17 Resultados do passo 4 da análise discriminante stepwise de três grupos
Ajuste geral do modelo
Valor Valor F Graus de liberdade Signifi cância
Lambda de Wilks 0,127 24,340 8, 108 0,000
Variável adicionada/removida no passo 4
F
Variável adicionada D^2 mínimo Valor Signifi cância Entre grupos
X 18 Velocidade de entrega 6,920 13,393 0,000 Menos de 1 ano e de 1 a 5 anos
Nota: Em cada passo, a variável que maximiza a distância Mahalanobis entre os dois grupos mais próximos é adicionada.
Variáveis na análise após o passo 4
Variável Tolerância F para remover D^2 Entre grupos
X 11 Linha de produto 0,075 0,918 6,830 Menos de 1 ano e de 1 a 5 anos
X 17 Flexibilidade de preço 0,070 1,735 6,916 Menos de 1 ano e de 1 a 5 anos
X 6 Qualidade do produto 0,680 27,701 3,598 De 1 a 5 anos e mais de 5 anos
X 18 Velocidade de entrega 0,063 5,387 6,071 Menos de 1 ano e de 1 a 5 anos
```
```
Variáveis fora da análise após o passo 4
Variável Tolerância Tolerância mínima F para entrar D^2 mínimo Entre grupos
X 7 Atividades de comércio eletrônico 0,870 0,063 0,226 6,931 Menos de 1 ano e de 1 a 5 anos
X 8 Suporte técnico 0,940 0,063 0,793 7,164 Menos de 1 ano e de 1 a 5 anos
X 9 Solução de reclamação 0,453 0,058 0,292 7,019 Menos de 1 ano e de 1 a 5 anos
X 10 Anúncio 0,932 0,063 0,006 6,921 Menos de 1 ano e de 1 a 5 anos
X 12 Imagem da equipe de venda 0,843 0,061 0,315 7,031 Menos de 1 ano e de 1 a 5 anos
X 13 Preços competitivos 0,790 0,063 0,924 7,193 Menos de 1 ano e de 1 a 5 anos
X 14 Garantia e reclamações 0,843 0,063 2,023 7,696 Menos de 1 ano e de 1 a 5 anos
X 15 Novos produtos 0,927 0,062 0,227 7,028 Menos de 1 ano e de 1 a 5 anos
X 16 Encomenda e cobrança 0,671 0,062 1,478 7,210 Menos de 1 ano e de 1 a 5 anos
Teste de signifi cância de diferenças de grupos após o passo 4a
X 1 Tipo de cliente Menos de 1 ano De 1 a 5 anos
De 1 a 5 anos F 13,393
Sig. 0,000
Mais de 5 anos F 56,164 18,477
Sig. 0,000 0,000
a4 e 54 graus de liberdade.
```
```
( Continua )
```
```
( Continuação )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 271

**Resumo do processo de estimação** **_stepwise_****.** As funções
discriminantes estimadas são composições lineares se-
melhantes a uma reta de regressão (ou seja, elas são uma
combinação linear de variáveis). Assim como uma reta de
regressão é uma tentativa de explicar a máxima variação
em sua variável dependente, essas composições lineares
tentam explicar as variações ou diferenças na variável ca-
tegórica dependente. A primeira função discriminante é
desenvolvida para explicar a maior variação (diferença)
nos grupos discriminantes. A segunda função discrimi-
nante, que é ortogonal e independente da primeira, ex-
plica o maior percentual da variância remanescente (re-
sidual) depois que a variância para a primeira função é
removida.

```
A informação fornecida na Tabela 5-19 resume os passos
da análise discriminante de três grupos, com os seguintes
resultados:
```
- _X_ 6 e _X_ 18 são as duas variáveis na função discriminante fi -
    nal, apesar de _X_ 11 e _X_ 17 terem sido acrescentadas nos dois
    primeiros passos e então removidas depois que _X_ 6 e _X_ 18
    foram adicionadas. Os coefi cientes não-padronizados e
    padronizados (pesos) da função discriminante e a matriz
    estrutural das cargas discriminantes, rotacionadas e não-
    rotacionadas, também foram fornecidos. A rotação das
    cargas discriminantes facilita a interpretação da mesma
    maneira que fatores foram simplifi cados para interpreta-
    ção via rotação (ver Capítulo 3 para uma discussão mais
    detalhada sobre rotação). Examinamos em pormenores
    as cargas rotacionadas e não-rotacionadas no passo 5.
- A discriminação aumentou com a adição de cada variá-
    vel (como evidenciado pela diminuição no lambda de
    Wilks), mesmo com apenas duas variáveis restando no
    modelo fi nal. Comparando o lambda de Wilks fi nal para
    a análise discriminante (0,148) com o lambda de Wilks
    (0,414**) para o melhor resultado de uma única variável,
    _X_ 9 **, vemos que uma melhora acentuada é obtida ao se
    usar exatamente duas variáveis nas funções discriminan-
    tes no lugar de uma única variável.
- A qualidade de ajuste geral para o modelo discriminante
    é estatisticamente signifi cante e ambas as funções são
    estatisticamente signifi cantes também. A primeira função
    explica 91,5% da variância explicada pelas duas funções,
    com a variância remanescente (8,5%) devida à segunda
    função. A variância total explicada pela primeira função
    é 0,893^2 , ou 79,7%. A próxima função explica 0,517^2 ou
    26,7% da variância remanescente (20,3%). Portanto,
    a variância total explicada por ambas as funções é de
    85,1% [79,7% + (26,7% × 0,203)] da variação total na
    variável dependente.

```
Ainda que ambas as funções sejam estatisticamente
signifi cantes, o pesquisador sempre deve garantir que as
funções discriminantes forneçam diferenças entre todos
os grupos. É possível ter funções estatisticamente signi-
fi cantes, mas ter pelo menos um par de grupos que não
sejam estatisticamente distintos (i.e., não discriminados
entre eles). Este problema se torna especialmente predo-
minante quando o número de grupos aumenta ou vários
grupos pequenos são incluídos na análise.
```
```
A última seção da Tabela 5-18 fornece os testes de signi-
fi cância para diferenças de grupos entre cada par de gru-
pos (p.ex., grupo 1 versus grupo 2, grupo 1 versus grupo
3 etc.). Todos os pares de grupos mostraram diferenças
estatisticamente signifi cantes, denotando que as funções
discriminantes criaram separação não apenas em um
sentido geral, mas também para cada grupo também.
Examinamos os centróides de grupos grafi camente em
uma seção posterior.
```
```
concluído em termos de acréscimo de variáveis. Porém,
o procedimento inclui também um exame da signifi cân-
cia de cada variável para que a mesma seja mantida na
função discriminante. Neste caso, o “ F para remover”
para X 11 e X 17 é não-signifi cante (0,918 e 1,735, respecti-
vamente), indicando que uma ou ambas são candidatas
para remoção da função discriminante.
```
```
Estimação stepwise : Remoção de X 17 e X 11. Quando
X 18 é adicionada ao modelo no quarto passo (ver a dis-
cussão anterior), X 11 tinha o menor valor “ F para remo-
ver” (0,918), fazendo com que o procedimento stepwise
eliminasse aquela variável da função discriminante no
quinto passo (detalhes sobre este passo 5 são omitidos
por questões de espaço). Agora com três variáveis na
função discriminante ( X 11 , X 6 e X 18 ), o ajuste geral do
modelo ainda é signifi cante e o lambda de Wilks aumen-
tou só um pouco para 0,135. Todos os grupos são signifi -
cantemente diferentes. Nenhuma variável atinge o nível
necessário de signifi cância estatística para ser adicionada
à função discriminante, e mais uma variável ( X 11 *) tem
um valor “ F para remover” de 2,552, o que indica que
ela também pode ser eliminada da função.
A Tabela 5-18 contém os detalhes do passo 6 do
procedimento stepwise , onde X 11 também é removi-
da da função discriminante, restando apenas X 6 e X 18.
Mesmo com a remoção da segunda variável (X 11 ), o
modelo geral ainda é signifi cante e o lambda de Wilks
é consideravelmente pequeno (0,148). Devemos obser-
var que este modelo de duas variáveis, X 6 e X 18 , é um
melhoramento em relação ao primeiro modelo de duas
variáveis, X 11 e X 17 , formado no passo 2 (lambda de Wi-
lks é 0,148 contra o valor do primeiro modelo de 0,288
e todas as diferenças individuais de grupos são muito
maiores). Sem variáveis alcançando o nível necessário
de signifi cância para adição ou remoção, o procedimen-
to stepwise é encerrado.
```
```
( Continuação )
```
* N. de R. T.: Provavelmente trata-se de _X_ 17 , uma vez que _X_ 11 já fora
removida. * N. de R. T.: Na verdade, seria _X_ 11 com lambda de Wilks igual a 0,467.


##### 272 Análise Multivariada de Dados

##### Avaliação da precisão de classifi cação

Como esse é um modelo de análise discriminante de três
grupos, duas funções discriminantes são calculadas para
discriminar entre os três grupos. Valores para cada caso
são inseridos no modelo discriminante e composições li-
neares (escores _Z_ discriminantes) são calculadas. As fun-
ções discriminantes são baseadas somente nas variáveis
incluídas no modelo discriminante.

```
TABELA 5-18 Resultados do passo 6 da análise discriminante stepwise de três grupos
Ajuste geral do modelo
Valor Valor F Graus de liberdade Signifi cância
Lambda de Wilks 0,148 44,774 4, 112 0,000
Variável adicionada/removida no passo 6
F
Variável removida D^2 mínimo Valor Signifi cância Entre grupos
X 11 Linha do produto 6,388 25,642 0,000 Menos de 1 ano e de 1 a 5 anos
Nota: Em cada passo, a variável que maximiza a distância Mahalanobis entre os dois grupos mais próximos é adicionada.
Variáveis na análise após o passo 6
Variável Tolerância F para remover D^2 Entre grupos
X 6 Qualidade do produto 0,754 50,494 0,007 De 1 a 5 anos e mais de 5 anos
X 18 Velocidade de entrega 0,754 60,646 0,121 Menos de 1 ano e de 1 a 5 anos
```
```
Variáveis fora da análise após o passo 6
Variável Tolerância Tolerância mínima F para entrar D^2 mínimo Entre grupos
X 7 Atividades de comércio eletrônico 0,954 0,728 0,177 6,474 Menos de 1 ano e de 1 a 5 anos
X 8 Suporte técnico 0,999 0,753 0,269 6,495 Menos de 1 ano e de 1 a 5 anos
X 9 Solução de reclamação 0,453 0,349 0,376 6,490 Menos de 1 ano e de 1 a 5 anos
X 10 Anúncio 0,954 0,742 0,128 6,402 Menos de 1 ano e de 1 a 5 anos
X 11 Linha do produto 0,701 0,529 2,552 6,916 Menos de 1 ano e de 1 a 5 anos
X 12 Imagem da equipe de venda 0,957 0,730 0,641 6,697 Menos de 1 ano e de 1 a 5 anos
X 13 Preços competitivos 0,994 0,749 1,440 6,408 Menos de 1 ano e de 1 a 5 anos
X 14 Garantia e reclamações 0,991 0,751 0,657 6,694 Menos de 1 ano e de 1 a 5 anos
X 15 Novos produtos 0,984 0,744 0,151 6,428 Menos de 1 ano e de 1 a 5 anos
X 16 Encomenda e cobrança 0,682 0,514 2,397 6,750 Menos de 1 ano e de 1 a 5 anos
X 17 Flexibilidade de preço 0,652 0,628 3,431 6,830 Menos de 1 ano e de 1 a 5 anos
```
```
Teste de signifi cância de diferenças de grupos após o passo 6a
X 1 Tipo de cliente Menos de 1 ano De 1 a 5 anos
De 1 a 5 anos F 25,642
Sig. 0,000
Mais de 5 anos F 110,261 30,756
Sig. 0,000 0,000
a6 e 52 graus de liberdade.
```
```
A Tabela 5-19 fornece os pesos discriminantes de am-
bas as variáveis ( X 6 e X 18 ) e as médias de cada grupo em
```
```
ambas as funções (parte inferior da tabela). Como po-
demos ver examinando as médias de grupos, a primeira
função distingue o grupo 1 (Menos de 1 ano) dos outros
dois grupos (apesar de uma sensível diferença ocorrer
entre os grupos 2 e 3 também), enquanto a segunda fun-
ção separa o grupo 3 (Mais de 5 anos) dos outros dois.
Portanto, a primeira função fornece a maior separação
entre todos os três grupos, mas é complementada pela
segunda função, a qual melhor discrimina (1 e 2 versus
3) onde a primeira função é mais fraca.
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 273

```
TABELA 5-19 Estatísticas resumo para análise discriminante de três grupos
Ajuste geral do modelo: funções discriminantes canônicas
Percentual de variância
```
```
Função Autovalor
```
```
Função
(%)
```
```
Percentual
cumulativo
```
```
Correlação
canônica
```
```
Lambda de
Wilks Qui-quadrado df Signifi cância
1 3,950 91,5 91,5 0,893 0,148 107,932 4 0,000
2 0,365 8,5 100,0 0,517 0,733 17,569 1 0,000
```
```
Coefi cientes da função discriminante e da função de classifi cação
FUNÇÃO DISCRIMINANTE
Função discriminante
não-padronizada
```
```
Função discriminante
padronizada Funções de classifi cação
```
```
Variáveis independentes Função 1 Função 2 Função 1 Função 2
```
```
Menos de
1 ano
```
```
De 1 a 5
anos
```
```
Acima de
5 anos
X 16 Encomenda e cobrança* 0,308 1,159 0,969 0,622 14,382 15,510 18,753
X 18 Velocidade de entrega 2,200 0,584 1,021 –0,533 25,487 31,185 34,401
(Constante) –10,832 –11,313 –91,174 –120,351 –159,022
Matriz estrutural
Cargas discriminantes não-rotacionadasa Cargas discriminantes rotacionadasb
Variáveis independentes Função 1 Função 2 Função 1 Função 2
X 9 Solução de reclamação* 0,572 –0,470 0,739 0,039
X 16 Encomenda e cobrança 0,499 –0,263 0,546 0,143
X 11 Linha do produto* 0,483 –0,256 0,529 0,137
X 15 Novos produtos* 0,125 –0,005 0,096 0,080
X 8 Suporte técnico* 0,030 –0,017 0,033 0,008
X 6 Qualidade do produto* 0,463 0,886 –0,257 0,967
X 18 Velocidade de entrega 0,540 –0,842 0,967 –0,257
X 17 Flexibilidade de preço* 0,106 –0,580 0,470 –0,356
X 10 Anúncio* 0,028 –0,213 0,165 –0,138
X 7 Atividades de comércio eletrônico* –0,095 –0,193 0,061 –0,207
X 12 Imagem da equipe de venda* –0,088 –0,188 0,061 –0,198
X 14 Garantia e reclamações* 0,030 –0,088 0,081 0,044
X 13 Preços competitivos* –0,055 –0,059 –0,001 –0,080
aCorrelações internas de grupos entre variáveis discriminantes e variáveis de funções discriminantes canônicas padronizadas ordenadas por tamanho abso-
luto da correlação dentro da função.b
Correlações internas de grupos entre variáveis discriminantes e funções discriminantes canônicas padronizadas e rotacionadas.
*Esta variável não é usada na análise.
Médias de grupo (centróides) de funções discriminantesc
X 1 Tipo de cliente Função 1 Função**
Menos de 1 ano –1,911 –1,274
De 1 a 5 anos 0,597 –0,968
Mais de 5 anos 1,371 1,625
c Funções discriminantes canônicas não-padronizadas avaliadas nas médias de grupos.
```
**Avaliação da precisão preditiva de pertinência a grupo.** O
passo fi nal para avaliar o ajuste geral do modelo é deter-
minar o nível de precisão preditiva da(s) função(ões)
discriminante(s). Essa determinação é conseguida do

```
mesmo modo que se faz no modelo discriminante de dois
grupos, examinando-se as matrizes de classifi cação e o
percentual corretamente classifi cado (razão de sucesso)
em cada amostra.
```
```
A classifi cação de casos individuais pode ser executada
pelo método de corte descrito no caso de dois grupos
```
* N. de RT.: Na realidade, foi incluída a variável _X_ 6 (Qualidade do
produto).
** N. de RT.: Neste caso, é Função 2.


##### 274 Análise Multivariada de Dados

```
ou usando as funções de classifi cação (ver Tabela 5-19)
onde cada caso é computado em cada função de classifi -
cação e classifi cado no grupo de maior escore.
A Tabela 5-20 mostra que as duas funções discri-
minantes em combinação atingem um grau elevado de
precisão de classifi cação. A proporção de sucesso para
a amostra de análise é de 86,7%. No entanto, a razão de
sucesso para a amostra de teste cai para 55,0%. Esses
resultados demonstram o viés ascendente que é típico
quando se aplica somente à amostra de análise, mas não
a uma amostra de validação.
Ambas as proporções de sucesso devem ser compa-
radas com os critérios de chance máxima e de chance
proporcional para se avaliar sua verdadeira efetividade.
O procedimento de validação cruzada é discutido no
passo 6.
```
- O critério de chance máxima é simplesmente a pro-
    porção de sucesso obtida se designarmos todas as ob-
    servações para o grupo com a maior probabilidade de
    ocorrência. Na presente amostra de 100 observações, 32
    estavam no grupo 1, 35 no grupo 2, e 33 no grupo 3. A
    partir dessa informação, podemos ver que a probabili-
    dade mais alta seria 35% (grupo 2). O valor de referên-
    cia para a chance máxima (35% × 1,25) é 43,74%.
- O critério de chance proporcional é calculado elevando-
    se ao quadrado as proporções de cada grupo, com um
    valor calculado de 33,36% (0,32^2 " 0,35^2 " 0,33^2!

```
0,334) e um valor de referência de 41,7% (33,4% × 1.25
! 41,7%).
As proporções de sucesso para as amostras de aná-
lise e de teste (86,7% e 55,0%, respectivamente) exce-
dem ambos os valores de referência de 43,74% e 41,7%.
Na amostra de estimação, todos os grupos individuais
ultrapassam os dois valores de referência. Na amostra
de teste, porém, o grupo 2 tem uma razão de sucesso de
somente 40,9%, e aumenta apenas para 53,8% na amos-
tra de análise. Tais resultados mostram que o grupo 2
deve ser o foco no melhoramento da classifi cação, pos-
sivelmente com a adição de variáveis independentes ou
uma revisão da classifi cação de fi rmas neste grupo para
identifi car as características do mesmo que não estão re-
presentadas na função discriminante.
A medida fi nal de precisão de classifi cação é o Q de
Press, calculado para as amostras de análise e de valida-
ção. Ele testa a signifi cância estatística de que a precisão
de classifi cação é melhor do que o acaso (chance).
```
```
E o cálculo para a amostra de teste é
```
```
TABELA 5-20 Resultados de classifi cação para a análise discriminante de três grupos
Resultados de classifi cação a, b, c^
Pertinência prevista em grupo
Grupo real Menos do que 1 ano De 1 a 5 anos Mais de 5 anos Total
Amostra de estimação Menos de 1 ano 21 1 0 22
95,5 4,5 0,0
De 1 a 5 anos 2 7 4 13
15,4 53,8 30,8
Mais de 5 anos 0 1 24 25
0,0 4,0 96,0
Validação cruzada Menos de 1 ano 21 1 0 22
95,5 4,5 0,0
De 1 a 5 anos 2 7 4 13
15,4 53,8 30,8
Mais de 5 anos 0 1 24 25
0,0 4,0 96,0
Amostra de validação Menos de 1 ano 5 3 2 10
50,0 30,0 20,0
De 1 a 5 anos 1 9 12 22
4,5 40,9 54,5
Mais de 5 anos 0 0 8 8
0,0 0,0 100,0
a86,7% dos casos agrupados originais selecionados corretamente classifi cados.
b55,0% dos casos agrupados originais não-selecionados corretamente classifi cados.
c86,7% dos casos agrupados selecionados e validados por cruzamento corretamente classifi cados.
```
```
( Continua )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 275

Quando completado, podemos concluir que o mode-
lo discriminante é válido e tem níveis adequados de sig-
nifi cância estatística e prática para todos os grupos. Os
valores consideravelmente menores para a amostra de
validação em todos os padrões de comparação, contudo,
justifi cam a preocupação levantada anteriormente sobre
as razões de sucesso específi cas de grupos e geral.

##### Diagnósticos por casos

Além das tabelas de classifi cação mostrando resultados
agregados, informação específi ca de casos também está
disponível detalhando a classifi cação de cada observação.
Essa informação pode detalhar as especifi cidades do pro-
cesso de classifi cação ou representar a classifi cação atra-
vés de um mapa territorial.

**Informação de classifi cação específi ca de caso.** Uma sé-
rie de medidas específi cas de casos está disponível para
identifi cação dos casos mal classifi cados, bem como o
diagnóstico da extensão de cada classifi cação ruim. Usan-
do essa informação, padrões entre os mal classifi cados po-
dem ser identifi cados.

```
O pesquisador deve avaliar a extensão de má classifi -
cação para cada caso. Casos que são classifi cações obvia-
mente ruins devem ser escolhidos para análise adicional
(perfi l, exame de variáveis adicionais etc.), discutida na
análise de dois grupos.
```
```
Mapa territorial. A análise de más classifi cações pode
ser suplementada pelo exame gráfi co das observações in-
dividuais, representando-as com base em seus escores Z
discriminantes.
```
```
Como o valor crítico em um nível de signifi cância
de 0,01 é 6,63, a análise discriminante pode ser descri-
ta como prevendo pertinência a grupo melhor do que o
acaso.
```
```
A Tabela 5-21 contém dados adicionais de classifi cação
para cada caso individual que foi mal classifi cado (in-
formação similar também está disponível para todos os
outros casos, mas foi omitida por problemas de espaço).
Os tipos básicos de informação de classifi cação incluem
o que se segue:
```
- _Pertinência a grupo._ Tanto os grupos reais quanto os
    previstos são exibidos para identifi car cada tipo de má
    classifi cação (p.ex., pertinência real ao grupo 1, mas pre-
    vista no grupo 2). Neste caso, vemos os 8 casos mal clas-
    sifi cados na amostra de análise (verifi que acrescentando
    os valores fora da diagonal na Tabela 5-20) e os 18 casos
    mal classifi cados na amostra de validação.
- _Distância de Mahalanobis ao centróide de grupo previsto._
    Denota a proximidade desses casos mal classifi cados em
    relação ao grupo previsto. Algumas observações, como o
    caso 10, obviamente são semelhantes às observações do
    grupo previsto e não do grupo real. Outras observações,
    como o caso 57 (distância de Mahalanobis de 6,041), são
    possivelmente observações atípicas no grupo previsto e
    no grupo real. O mapa territorial discutido na próxima
    seção retrata grafi camente a posição de cada observação
    e auxilia na interpretação das medidas de distância.
- _Escores discriminantes._ O escore _Z_ discriminante para
    cada caso em cada função discriminante fornece uma
    maneira de comparação direta entre casos e um posicio-
    namento relativo versus as médias de grupos.
       - _Probabilidade de classifi cação._ Derivada do emprego
          das funções discriminantes de classifi cação, a probabili-
          dade de pertinência para cada grupo é dada. Os valores
          de probabilidade viabilizam ao pesquisador avaliar a
          extensão da má classifi cação. Por exemplo, dois casos,
          85 e 89, são do mesmo tipo de má classifi cação (grupo
          real 2 e grupo previsto 3), mas muito diferentes em suas
          classifi cações quando as probabilidades são focadas. O
          caso 85 representa uma classifi cação ruim marginal, pois
          a probabilidade de previsão no grupo real 2 era de 0,462,
          enquanto no grupo 3 incorretamente previsto ela era
          um pouco maior (0,529). Esta má classifi cação contrasta
          com o caso 89, onde a probabilidade do grupo real era
          de 0,032, e a probabilidade prevista para o grupo 3 (o
          mal classifi cado) era 0,966. Em ambas as situações de má
          classifi cação, a extensão ou magnitude varia muito.

```
A Figura 5-9 mostra cada observação baseada em seus
dois escores Z discriminantes rotacionados com uma co-
bertura do mapa territorial que representa as fronteiras
dos escores de corte para cada função. Ao ver a disper-
são de cada grupo em torno do centróide, podemos ob-
servar várias coisas:
```
- O grupo 3 (Mais de 5 anos) é mais concentrado, com
    pouca sobreposição com os outros dois grupos, como se
    mostra na matriz de classifi cação onde apenas uma ob-
    servação foi mal classifi cada (ver Tabela 5-20).
- O grupo 1 (Menos de 1 ano) é o menos compacto, mas o
    domínio de casos não se sobrepõe em grande grau com
    os outros grupos, tornando previsões muito melhores
    do que poderia ser esperado para um grupo tão variado.
    Os únicos casos mal classifi cados que são substancial-
    mente distintos são o caso 10, que é próximo ao centrói-
    de do grupo 2, e o caso 13, que é próximo ao centróide
    do grupo 3. Ambos os casos merecem melhor investiga-
    ção quanto às suas similaridades com outros grupos.
- Estes dois grupos fazem contraste com o grupo 2 (De
    1 a 5 anos), que pode ser visto como tendo substancial
    sobreposição com o grupo 3 e, em menor extensão, com
    o grupo 1 (Menos de 1 ano). Essa sobreposição resulta
    nos mais baixos níveis de precisão de classifi cação nas
    amostras de análise e de teste.
- A sobreposição que ocorre entre os grupos 2 e 3 no
    centro e à direita no gráfi co sugere a possível existência
    de um quarto grupo. Uma análise poderia ser levada

```
( Continuação )
```
```
( Continua )
```

##### 276 Análise Multivariada de Dados

A representação gráfi ca é útil não apenas para identi-
fi car esses casos mal classifi cados que podem formar um
novo grupo, mas também para identifi car observações atí-
picas. A discussão anterior indica possíveis opções para
identifi car observações atípicas (caso 57), bem como a
possibilidade de redefi nição de grupos entre os grupos 2
e 3.

#### Estágio 5: Interpretação dos resultados

#### da análise discriminante de três grupos

O próximo estágio da análise discriminante envolve uma sé-
rie de passos na interpretação das funções discriminantes.

- Calcular as cargas para cada função e rever a rotação das
    funções para fi ns de simplifi cação da interpretação.
- Examinar as contribuições das variáveis preditoras: (a) a
    cada função separadamente (ou seja, cargas discriminan-
    tes), (b) cumulativamente sobre múltiplas funções discri-
    minantes com o índice de potência, e (c) grafi camente em
    uma solução bidimensional para entender a posição relativa
    de cada grupo e a interpretação das variáveis relevantes na
    determinação dessa posição.

##### Cargas discriminantes e suas rotações

```
Uma vez que as funções discriminantes são calculadas,
elas são correlacionadas com todas as variáveis indepen-
dentes, mesmo aquelas não usadas na função discriminan-
te, para desenvolver uma matriz estrutural (de cargas).
Tal procedimento nos permite ver onde a discriminação
ocorreria se todas as variáveis independentes fossem in-
cluídas no modelo (ou seja, se nenhuma fosse excluída por
multicolinearidade ou falta de signifi cância estatística).
```
```
TABELA 5-21 Previsões mal classifi cadas para casos individuais na análise discriminante de três grupos
PERTINÊNCIA A
GRUPO ESCORES DISCRIMINANTES PROBABILIDADE DE CLASSIFICAÇÃO
```
```
Identifi cação
do caso (X 1 ) Real Previsto
```
```
Distância de
Mahalanobis
ao centróidea Função 1 Função 2 Grupo 1 Grupo 2 Grupo 3
Amostra de análise/estimação
10 1 2 0,175 0,81755 –1,32387 0,04173 0,93645 0,02182
8 2 1 1,747 –0,78395 –1,96454 0,75064 0,24904 0,00032
100 2 1 2,820 –0,70077 –0,11060 0,54280 0,39170 0,06550
1 2 3 2,947 –0,07613 0,70175 0,06527 0,28958 0,64515
5 2 3 3,217 –0,36224 1,16458 0,05471 0,13646 0,80884
37 2 3 3,217 –0,36224 1,16458 0,05471 0,13646 0,80884
88 2 3 2,390 0,99763 0,12476 0,00841 0,46212 0,52947
58 3 2 0,727 0,30687 –0,16637 0,07879 0,70022 0,22099
Amostra de teste/validação
25 1 2 1,723 –0,18552 –2,02118 0,40554 0,59341 0,00104
77 1 2 0,813 0,08688 –0,22477 0,13933 0,70042 0,16025
97 1 2 1,180 –0,41466 –0,57343 0,42296 0,54291 0,03412
13 1 3 0,576 1,77156 2,26982 0,00000 0,00184 0,99816
96 1 3 3,428 –0,26535 0,75928 0,09917 0,27855 0,62228
83 2 1 2,940 –1,58531 0,40887 0,89141 0,08200 0,02659
23 2 3 0,972 0,61462 0,99288 0,00399 0,10959 0,88641
34 2 3 1,717 0,86996 0,41413 0,00712 0,31048 0,68240
39 2 3 0,694 1,59148 0,82119 0,00028 0,08306 0,91667
41 2 3 2,220 0,30230 0,58670 0,02733 0,30246 0,67021
42 2 3 0,210 1,08081 1,97869 0,00006 0,00665 0,99330
55 2 3 1,717 0,86996 0,41413 0,00712 0,31048 0,68240
57 2 3 6,041 3,54521 0,47780 0,00000 0,04641 0,95359
62 2 3 4,088 –0,32690 0,52743 0,17066 0,38259 0,44675
75 2 3 2,947 –0,07613 0,70175 0,06527 0,28958 0,64515
78 2 3 0,210 1,08081 1,97869 0,00006 0,00665 0,99330
85 2 3 2,390 0,99763 0,12476 0,00841 0,46212 0,52947
89 2 3 0,689 0,54850 1,51411 0,00119 0,03255 0,96625
aDistância de Mahalanobis ao centróide do grupo previsto
```
```
a cabo para determinar o real intervalo de tempo de
clientes, talvez com clientes com mais de 1 ano divididos
em três grupos ao invés de dois.
```
```
( Continuação )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 277

**Cargas discriminantes.** As cargas não-rotacionadas re-
presentam a associação de cada variável independente
com cada função, mesmo que não esteja incluída na fun-
ção discriminante. Cargas discriminantes, semelhantes às
cargas fatoriais descritas no Capítulo 3, são as correla-
ções entre cada variável independente e o escore discri-
minante.

```
A Tabela 5-19 contém a matriz estrutural de cargas não-
rotacionadas para ambas as funções discriminantes. Se-
lecionando variáveis com cargas de 0,40 ou acima como
descritivas das funções, percebemos que a função 1 tem
cinco variáveis excedendo 0,40 ( X 9 , X 18 , X 16 , X 11 e X 6 ),
enquanto quatro variáveis são descritivas da função 2
( X 6 , X 18 , X 17 e X 9 ). Ainda que pudéssemos usar essas
variáveis para descrever cada função, enfrentaríamos o
problema de que três variáveis ( X 9 , X 6 e X 18 ) têm car-
gas duplas (variáveis selecionadas como descritivas de
ambas as funções). Se fôssemos proceder com as cargas
não-rotacionadas, cada função compartilharia mais va-
riáveis com a outra do que teria feito se fosse única.
```
A falta de distinção das cargas com cada variável des-
critiva de uma só função pode ser abordada com rotação
da matriz estrutural, exatamente como foi feito com car-
gas fatoriais. Para uma descrição mais detalhada do pro-
cesso de rotação, ver Capítulo 3.

**Rotação** Depois que as cargas da função discriminante
são calculadas, elas podem ser rotacionadas para redis-
tribuir a variância (esse conceito é melhor explicado no
Capítulo 3). Basicamente, a rotação preserva a estrutura

```
original e a confi abilidade dos modelos discriminantes e
facilita consideravelmente a sua interpretação.
```
```
Na presente aplicação, escolhemos o procedimento mais
amplamente usado de rotação VARIMAX. A rotação
afeta os coefi cientes da função e as cargas discriminan-
tes, bem como o cálculo dos escores Z discriminantes e
dos centróides de grupo (ver Tabela 5-19). Examinar os
coefi cientes ou as cargas rotacionados versus não-rota-
cionados revela um conjunto de resultados um pouco
mais simples (ou seja, as cargas tendem a se separar em
valores altos versus baixos, em vez de se limitarem a um
domínio intermediário). As cargas rotacionadas permi-
tem interpretações muito mais distintas de cada função:
```
- A função 1 é agora descrita por três variáveis ( _X_ 18 , _X_ 9
    e _X_ 16 ) que formam o fator _Serviço ao Cliente de Pós-_
    _Venda_ durante a análise fatorial (ver Capítulo 3 para
    mais detalhes), mais _X_ 11 e _X_ 17. Assim, o serviço a clien-
    te, mais linha de produto e fl exibilidade de preço são
    descritores da função 1.
- A função 2 mostra apenas uma variável, _X_ 6 (Qualidade
    do produto), que tem uma carga acima de 0,40 para a
    segunda função. Apesar de _X_ 17 ter um valor abaixo da
    referência (–0,356), esta variável tem uma carga maior
    na primeira função, o que a torna um descritor daquela
    função. Logo, a segunda função pode ser descrita pela
    variável de Qualidade do produto.

```
Com duas ou mais funções estimadas, a rotação pode
ser uma poderosa ferramenta que sempre deve ser consi-
derada para aumentar a interpretabilidade dos resultados.
Em nosso exemplo, cada uma das variáveis que entrou no
```
```
X 1 - Tipo de cliente
```
```
Centróides de grupo
```
```
Mais de 5 anos
```
```
Mais de 5 anos
```
```
De 1 a 5 anos
```
```
De 1 a 5 anos
```
```
Menos de 1 ano
```
```
Menos de 1 ano
```
```
Função 2
```
```
Função 1
```
**FIGURA 5-9** Mapa territorial para a análise discriminante de três grupos.


##### 278 Análise Multivariada de Dados

processo _stepwise_ era descritiva de uma das funções discri-
minantes. O que devemos fazer agora é avaliar o impacto
de cada variável em termos da análise discriminante geral
(i.e., em ambas as funções).

##### Avaliação da contribuição de variáveis preditoras

Tendo descrito as funções discriminantes em termos das
variáveis independentes – tanto aquelas que foram usa-
das nas funções discriminantes quanto as que não foram
incluídas – voltamos nossa atenção para conseguir uma
melhor compreensão do impacto das próprias funções, e
então das variáveis individuais.

**Impacto das funções individuais.** A primeira tarefa é
examinar as funções discriminantes em termos de como
elas diferenciam entre os grupos.

```
Começamos examinando os centróides de grupos quan-
to às duas funções como mostrado na Tabela 5-19. Uma
abordagem mais fácil é através do mapa territorial (Fi-
gura 5-9):
```
- Examinando os centróides de grupos e a distribuição
    de casos em cada grupo, percebemos que a função 1
    prioritariamente diferencia entre o grupo 1 e os grupos
    2 e 3, enquanto a função 2 distingue entre o grupo 3 e os
    grupos 1 e 2.
- A sobreposição e a má classifi cação dos casos dos
    grupos 2 e 3 pode ser tratada via o exame da força das
    funções discriminantes e dos grupos diferenciados por
    conta de cada uma. Retomando a Tabela 5-19, a função
    1 era, de longe, o discriminador mais potente, e ela prio-
    ritariamente separava o grupo 1 dos demais. A função 2,
    que separava o grupo 3 dos outros, era muito mais fraca
    em termos de poder discriminante. Não é surpresa que
    a maior sobreposição e má classifi cação ocorreriam en-
    tre os grupos 2 e 3, que são distinguidos principalmente
    pela função 2.

Essa abordagem gráfi ca ilustra as diferenças nos gru-
pos devido às funções discriminantes, mas não fornece
uma base para explicar essas diferenças em termos das
variáveis independentes.
Para avaliar as contribuições das variáveis individuais,
o pesquisador conta com várias medidas – cargas discri-
minantes, razões _F_ univariadas e o índice de potência. As
técnicas envolvidas no uso de cargas discriminantes e de
razões _F_ univariadas foram discutidas no exemplo de dois
grupos. Examinaremos mais detalhadamente o índice de
potência, um método de avaliação da contribuição de uma
variável em múltiplas funções discriminantes.

**Índice de potência.** O índice de potência é uma técnica
adicional de interpretação muito útil em situações com
mais de uma função discriminante. Ele retrata a contribui-
ção de cada variável individual em todas as funções discri-
minantes em termos de uma única medida comparável.

```
O índice de potência refl ete tanto as cargas de cada
variável quanto o poder discriminatório relativo de cada
função. As cargas rotacionadas representam a correlação
entre a variável independente e o escore Z discriminan-
te. Assim, a carga ao quadrado é a variância na variável
independente associada com a função discriminante. Pon-
derando a variância explicada de cada função via poder
discriminatório relativo da função e somando nas funções,
o índice de potência representa o efeito discriminante to-
tal de cada variável ao longo de todas as funções discrimi-
nantes.
```
```
A Tabela 5-22 fornece os detalhes do cálculo do índice
de potência para cada variável independente. A com-
paração das variáveis quanto a seus índices de potência
revela o seguinte:
```
- _X_ 18 (Velocidade de entrega) é a variável independente
    responsável pela maior discriminação entre os três tipos
    de grupos de clientes.
- Ela é seguida em termos de impacto por quatro variá-
    veis não incluídas na função discriminante ( _X_ 9 , _X_ 16 , _X_ 11
    e _X_ 17 ).
- A segunda variável na função discriminante ( _X_ 6 ) tem
    apenas o sexto maior valor de potência.
       Por que _X_ 6 tem somente o sexto maior valor de po-
tência mesmo sendo uma das duas variáveis incluídas na
função discriminante?
- Primeiro, lembre-se que multicolinearidade afeta solu-
    ções _stepwise_ devido à redundância entre variáveis alta-
    mente multicolineares. _X_ 9 e _X_ 16 eram as duas variáveis
    altamente associadas com _X_ 18 (formando o fator Serviço
    a Clientes), e assim seu impacto em um sentido univa-
    riado, refl etido no índice de potência, não era neces-
    sário na função discriminante devido à presença de _X_ 18.
- As outras duas variáveis, _X_ 11 e _X_ 17 , entraram através
    do procedimento _stepwise_ , mas foram removidas uma
    vez que _X_ 6 foi adicionada, novamente devido à multi-
    colinearidade. Assim, seu maior poder discriminante
    está refl etido em seus valores de potência ainda que
    elas não fossem necessárias na função discriminante,
    uma vez que _X_ 6 foi acrescentada com _X_ 18 na função
    discriminante.
- Finalmente, _X_ 6 , a segunda variável na função discrimi-
    nante, tem um baixo valor de potência por ser associada
    com a segunda função discriminante, que tem relativa-
    mente pouco impacto discriminante quando comparada
    com a primeira função. Logo, a despeito de _X_ 6 ser um
    elemento necessário na discriminação entre os três gru-
    pos, seu impacto geral é menor do que aquelas variáveis
    associadas com a primeira função.

```
Lembre-se que os valores de potência podem ser cal-
culados para todas as variáveis independentes, mesmo
que não estejam nas funções discriminantes, pois eles são
baseados em cargas discriminantes. A meta do índice de
potência é fornecer interpretação naqueles casos onde
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 279

**TABELA 5-22**

Cálculo dos índices de potência para a análise discriminante de três grupos

```
Função discriminante
```
```
1
```
```
Função discriminante
```
```
2
```
```
Variáveis independentes
```
```
Carga
```
```
Carga ao quadrado
```
```
Autovalor relativo
```
```
Valor de potência
```
```
Carga
```
```
Carga ao quadrado
```
```
Autovalor relativo
```
```
Valor de potência
```
```
Índice de potência
```
```
X^6
```
```
Qualidade do produto
```
```
–0,257
```
```
0,066
```
```
0,915
```
```
0,060
```
```
0,967
```
```
0,935
```
```
0,085
```
```
0,079
```
```
0,139
```
```
X^7
```
```
Atividades de comércio eletrônico
```
```
0,061
```
```
0,004
```
```
0,915
```
```
0,056
```
```
–0,207
```
```
0,043
```
```
0,085
```
```
0,004
```
```
0,060
```
```
X^8
```
```
Suporte técnico
```
```
0,033
```
```
0,001
```
```
0,915
```
```
0,001
```
```
0,008
```
```
0,000
```
```
0,085
```
```
0,000
```
```
0,001
```
```
X^9
```
```
Solução de reclamação
```
```
0,739
```
```
0,546
```
```
0,915
```
```
0,500
```
```
0,039
```
```
0,002
```
```
0,085
```
```
0,000
```
```
0,500
```
```
X^10
```
```
Anúncio
```
```
0,165
```
```
0,027
```
```
0,915
```
```
0,025
```
```
–0,138
```
```
0,019
```
```
0,085
```
```
0,002
```
```
0,027
```
```
X^11
```
```
Linha do produto
```
```
0,529
```
```
0,280
```
```
0,915
```
```
0,256
```
```
0,137
```
```
0,019
```
```
0,085
```
```
0,002
```
```
0,258
```
```
X^12
```
```
Imagem da equipe de venda
```
```
0,061
```
```
0,004
```
```
0,915
```
```
0,004
```
```
–0,198
```
```
0,039
```
```
0,085
```
```
0,003
```
```
0,007
```
```
X^13
```
```
Preços competitivos
```
```
–0,001
```
```
0,000
```
```
0,915
```
```
0,000
```
```
–0,080
```
```
0,006
```
```
0,085
```
```
0,001
```
```
0,001
```
```
X^14
```
```
Garantia e reclamações
```
```
0,081
```
```
0,007
```
```
0,915
```
```
0,006
```
```
0,044
```
```
0,002
```
```
0,085
```
```
0,000
```
```
0,006
```
```
X^15
```
```
Novos produtos
```
```
0,096
```
```
0,009
```
```
0,915
```
```
0,008
```
```
0,080
```
```
0,006
```
```
0,085
```
```
0,001
```
```
0,009
```
```
X^16
```
```
Encomenda e cobrança
```
```
0,546
```
```
0,298
```
```
0,915
```
```
0,273
```
```
0,143
```
```
0,020
```
```
0,085
```
```
0,002
```
```
0,275
```
```
X^17
```
```
Flexibilidade de preço
```
```
0,470
```
```
0,221
```
```
0,915
```
```
0,202
```
```
–0,356
```
```
0,127
```
```
0,085
```
```
0,011
```
```
0,213
```
```
X^18
```
```
Velocidade de entrega
```
```
0,967
```
```
0,935
```
```
0,915
```
```
0,855
```
```
–0,257
```
```
0,066
```
```
0,085
```
```
0,006
```
```
0,861
```
```
Nota
```
```
: O autovalor relativo de cada função discriminante é calculado como o autovalor de cada função (mostrado na Tabela 5-19 como 3,950 e 0,365 para as funções discriminantes I e II, res-
pectivamente) dividido pelo total dos autovalores (3,950 + 0,365 = 4,315).
```

##### 280 Análise Multivariada de Dados

multicolinearidade ou outros fatores possam ter evitado a
inclusão de uma variável na função discriminante.

**Uma visão geral das medidas empíricas de impacto.**
Como visto nas discussões anteriores, o poder discrimi-
natório de variáveis em análise discriminante é refl etido
em muitas medidas diferentes, cada uma desempenhando
um papel único na interpretação dos resultados discrimi-
nantes. Combinando todas essas medidas em nossa ava-
liação das variáveis, podemos conquistar uma perspectiva
bastante eclética sobre como cada variável se ajusta nos
resultados discriminantes.

```
De particular interesse é a interpretação das duas di-
mensões de discriminação. Essa interpretação pode ser
feita somente através do exame das cargas, mas é comple-
mentada por uma representação gráfi ca das cargas discri-
minantes, como descrito na próxima seção.
```
```
Representação gráfi ca de cargas discriminantes. Para
representar as diferenças em termos das variáveis pre-
ditoras, as cargas e os centróides de grupos podem ser
representados grafi camente em espaço discriminante re-
duzido. Como observado anteriormente, a representação
mais válida é o uso de vetores de atribuição e centróides
de grupos expandidos.
```
```
TABELA 5-23 Resumo de medidas interpretativas para análise discriminante de três grupos
Cargas rotacionadas de
função discriminante
```
```
Função 1 Função 2
```
```
Razão F
univariada
```
```
Índice de
potência
X 6 Qualidade do produto –0,257 0,967 32,311 0,139
X 7 Atividades de comércio eletrônico 0,061 –0,207 1,221 0,060
X 8 Suporte técnico 0,033 0,008 0,782 0,001
X 9 Solução de reclamação 0,739 0,039 40,292 0,500
X 10 Anúncio 0,165 –0,138 1,147 0,027
X 11 Linha do produto 0,529 0,137 32,583 0,258
X 12 Imagem da equipe de venda 0,061 –0,198 1,708 0,007
X 13 Preços competitivos –0,001 –0,080 9,432 0,001
X 14 Garantia e reclamações 0,081 0,044 2,619 0,006
X 15 Novos produtos 0,096 0,080 0,216 0,009
X 16 Encomenda e cobrança 0,546 0,143 25,048 0,275
X 17 Flexibilidade de preço 0,470 –0,356 12,551 0,213
X 18 Velocidade de entrega 0,967 –0,257 40,176 0,861
```
```
A Tabela 5-23 apresenta as três medidas interpretativas
preferidas (cargas rotacionadas, razão F univariada e ín-
dice de potência) para cada variável independente. Os
resultados apóiam a análise stepwise , apesar de ilustra-
rem em diversos casos o impacto de multicolinearidade
sobre os procedimentos e os resultados.
```
- Duas variáveis ( _X_ 9 e _X_ 18 ) têm os maiores impactos indi-
    viduais como evidenciado por seus valores _F_ univaria-
    dos. No entanto, como ambas são altamente associadas
    (como evidenciado por suas inclusões no fator Serviço
    ao cliente do Capítulo 3), apenas uma será incluída em
    uma solução _stepwise_. Ainda que _X_ 9 tenha um valor _F_
    univariado marginalmente maior, a habilidade de _X_ 18
    fornecer uma melhor discriminação entre todos os gru-
    pos (como evidenciado por seu maior valor mínimo _D_^2
    de Mahalanobis descrito anteriormente) fez dela a me-
    lhor candidata para inclusão. Portanto, _X_ 9 , em uma base
    individual, tem um poder discriminante comparável, mas
    _X_ 18 será vista funcionando melhor com outras variáveis.
- Três variáveis adicionais ( _X_ 6 , _X_ 11 e _X_ 16 ) são as próximas
    com maior impacto, mas apenas uma, _X_ 6 , é mantida na
    função discriminante. Note que _X_ 16 é altamente correla-
    cionada com _X_ 18 (ambas parte do fator Serviço ao clien-

```
te) e não incluída na função discriminante, enquanto X 11
entrou na mesma, mas foi uma daquelas variáveis remo-
vidas depois que X 6 foi adicionada.
```
- Finalmente, duas variáveis ( _X_ 17 e _X_ 13 ) tinham quase os
    mesmos efeitos univariados, mas somente _X_ 17 tinha uma
    associação substancial com uma das funções discrimi-
    nantes (uma carga de 0,470 sobre a primeira função). O
    resultado é que mesmo que _X_ 17 possa ser considerada
    descritiva da primeira função e tendo um impacto na
    discriminação baseado nessas funções, _X_ 13 não tem
    qualquer impacto, seja em associação com essas duas
    funções, seja em adição uma vez que estas funções sejam
    explicadas.
- Todas as variáveis remanescentes tinham pequenos
    valores _F_ univariados e pequenos valores de potência, o
    que indica pouco ou nenhum impacto tanto no sentido
    univariado quanto multivariado.

```
A Tabela 5-24 mostra os cálculos para a expansão das
cargas discriminantes (usadas para vetores de atribui-
ção) e de centróides de grupos. O processo de represen-
( Continua )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 281

#### Estágio 6: Validação dos

#### resultados discriminantes

```
As razões de sucesso para as matrizes de classifi cação cru-
zada e de teste podem ser usadas para avaliar a validade
interna e externa, respectivamente, da análise discrimi-
nante. Se as razões de sucesso excederem os valores de
referência nos padrões de comparação, então validade é
estabelecida. Como anteriormente descrito, os valores de
referência são 41,7% para o critério de chance proporcio-
nal e 43,7% para o critério de chance máxima. Os resulta-
dos de classifi cação mostrados na Tabela 5-20 fornecem o
seguinte suporte para validade:
Validade interna é avaliada pelo método de classifi ca-
ção cruzada, onde o modelo discriminante é estimado dei-
xando um caso de fora e então prevendo aquele caso com
o modelo estimado. Este processo é feito em turnos para
cada observação, de modo que uma observação jamais in-
fl uencia o modelo discriminante que prevê sua classifi ca-
ção em algum grupo.
```
```
Como visto na Tabela 5-20, a razão de sucesso geral para
o método de classifi cação cruzada de 86,7 substancialmen-
te excede ambos os padrões, tanto geral quanto para cada
grupo. Contudo, ainda que todos os três grupos também
tenham razões individuais de sucesso acima dos padrões,
a razão de sucesso do grupo 2 (53,8) é consideravelmente
menor do que aquela sobre os outros dois grupos.
```
```
tação gráfi ca sempre envolve todas as variáveis incluídas
no modelo pelo procedimento stepwise (em nosso exem-
plo, X 6 e X 18 ). No entanto, também faremos o gráfi co
das variáveis não incluídas na função discriminante se
suas respectivas razões F univariadas forem signifi can-
tes, o que adiciona X 9 , X 11 e X 16 ao espaço discriminante
reduzido. Esse procedimento mostra a importância de
variáveis colineares que não foram incluídas no modelo
stepwise fi nal, semelhante ao índice de potência.
Os gráfi cos dos vetores de atribuição expandidos
para as cargas discriminantes rotacionadas são exibidos
na Figura 5-10. Os vetores do gráfi co nos quais esse pro-
cedimento foi usado apontam para os grupos que têm a
mais alta média na respectiva variável independente e
para a direção oposta dos grupos que têm os mais baixos
escores médios. Assim, a interpretação do gráfi co na Fi-
gura 5-10 indica o seguinte:
```
- Como observado no mapa territorial e na análise dos
    centróides de grupos, a primeira função discriminante
    distingue entre grupo 1 e grupos 2 e 3, enquanto a se-
    gunda diferencia o grupo 3 dos grupos 1 e 2.
- A correspondência de _X_ 11 , _X_ 16 , _X_ 9 e _X_ 18 com o eixo _X_
    refl ete a associação delas com a primeira função discri-
    minante, enquanto vemos que somente _X_ 6 é associada
    com a segunda função discriminante. A fi gura ilustra
    grafi camente as cargas rotacionadas para cada função e
    distingue as variáveis descritivas de cada função.

```
TABELA 5-24 Cálculo dos vetores de atribuição e dos centróides de grupos expandidos no espaço discriminante reduzido
Cargas da função discrimi-
nante rotacionada
```
```
Coordenadas no
espaço reduzido
```
```
Variáveis independentes Função 1 Função 2
```
```
Razão F
univariada Função 1 Função 2
X 6 Qualidade do produto –0,257 0,967 32,311 –8,303 31,244
X 7 Atividades de comércio eletrônicoa 0,061 –0,207 1,221
X 8 Suporte técnicoa 0,033 0,008 0,782
X 9 Solução de reclamação 0,739 0,039 40,292 29,776 1,571
X 10 Anúncioa 0,165 –0,138 1,147
X 11 Linha do produto 0,529 0,137 32,583 17,236 4,464
X 12 Imagem da equipe de vendaa 0,061 –0,198 1,708
X 13 Preços competitivosa –0,001 –0,080 9,432
X 14 Garantia e reclamaçõesa 0,081 0,044 2,619
X 15 Novos produtosa 0,096 0,080 0,216
X 16 Encomenda e cobrança 0,546 0,143 25,048 13,676 3,581
X 17 Flexibilidade de preçoa 0,470 –0,356 12,551
X 18 Velocidade de entrega 0,967 –0,257 40,176 38,850 –10,325
aVariáveis com razões univariadas não-signifi cantes não são representadas no espaço reduzido.
```
```
Centróides de grupo Valor F aproximado
```
```
Coordenadas no
espaço reduzido
Função 1 Função 2 Função 1 Função 2 Função 1 Função 2
Grupo 1: Menos de 1 ano –1,911 –1,274 66,011 56,954 –126,147 –72,559
Grupo 2: De 1 a 5 anos 0,597 –0,968 66,011 56,954 39,408 –55,131
Grupo 3: Mais de 5 anos 1,371 1,625 66,011 56,954 90,501 92,550
```
( _Continuação_ )


##### 282 Análise Multivariada de Dados

Validade externa é tratada através da amostra de tes-
te, a qual é uma amostra completamente separada que
utiliza as funções discriminantes estimadas com a amostra
de análise para previsão de grupos.

```
Em nosso exemplo, a amostra de teste tem uma ra-
zão geral de sucesso de 55,0%, o que excede ambos
os valores de referência, apesar de isso não ocorrer na
magnitude encontrada na abordagem de classifi cação
cruzada. O grupo 2, contudo, não excedeu qualquer
valor de referência. Quando as classifi cações ruins são
analisadas, percebemos que mais casos são mal classi-
fi cados no grupo 3 do que corretamente classifi cados
no grupo 2, o que sugere que esses casos mal classi-
fi cados sejam examinados diante da possibilidade de
uma redefi nição dos grupos 2 e 3 para que se crie um
novo grupo.
```
O pesquisador também é encorajado a estender o
processo de validação por meio do perfi l dos grupos
quanto a conjuntos adicionais de variáveis ou apli-
cando a função discriminante em outra(s) amostra(s)
representativa(s) da população geral ou de segmentos
da mesma. Além disso, a análise de casos mal classifi -
cados ajudará a estabelecer se são necessárias variáveis
adicionais ou se a classifi cação de grupos dependentes
precisa de revisão.

#### Uma visão gerencial

A análise discriminante teve por meta entender as dife-
renças perceptuais de clientes com base nos intervalos de
tempo como clientes da HBAT. Espera-se que o exame
de diferenças em percepções HBAT baseadas na constân-
cia como clientes identifi que percepções que são críticas

```
ao desenvolvimento de uma relação de clientela, o que é
tipifi cado por aqueles clientes de longo prazo. Três grupos
de clientela foram formados – menos de 1 ano, de 1 a 5
anos, e mais de 5 anos – e as percepções quanto à HBAT
foram medidas sobre 13 variáveis. A análise produziu di-
versas descobertas importantes, tanto em termos dos tipos
de variáveis que distinguiam entre os grupos quanto nos
padrões de mudanças ao longo do tempo:
```
```
Grupo 3
```
```
Função 2
```
```
Função 1
```
```
Grupo 2
Grupo 1
```
**FIGURA 5-10** Gráfi co de vetores de atribuição expandidos (variáveis) no espaço discriminante reduzido.

- Primeiro, há duas dimensões de discriminação entre os
    três grupos de clientes. A primeira dimensão é tipifi cada
    por elevadas percepções de serviço aos clientes (Solu-
    ção de reclamação, Velocidade de entrega e Encomen-
    da e cobrança), juntamente com Linha do produto e
    Flexibilidade de preço. Em contraste, a segunda dimen-
    são é caracterizada somente em termos de Qualidade
    do produto.
- O perfi l dos três grupos quanto a essas duas dimensões
    e variáveis associadas com cada dimensão permite à
    gerência compreender as diferenças perceptuais entre
    eles.
    - O grupo 1, clientes há menos de 1 ano, geralmente
       tem as menores percepções da HBAT. Para as
       três variáveis de serviço à clientela (Solução de
       reclamação, Encomenda e cobrança, e Velocidade
       de entrega), esses clientes têm percepções menores
       do que em qualquer outro grupo. Para Qualidade
       de produto, Linha de produto e Preço competitivo,
       este grupo é comparável com o 2 (de 1 a 5 anos), mas
       ainda tem percepções menores do que clientes há
       mais de 5 anos. Somente para Flexibilidade de preço
       este grupo é comparável com os clientes mais antigos
       e ambos têm valores menores do que os clientes de
       1 a 5 anos. No geral, as percepções desses clientes
       mais recentes seguem o padrão esperado de serem
       menores do que outros da clientela, mas é esperado
          ( _Continua_ )


##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 283

Assim, o gerenciamento leva em conta um _input_ para
planejamento estratégico e tático não apenas dos resul-
tados diretos da análise discriminante, mas também dos
erros de classifi cação.

#### REGRESSÃO LOGÍSTICA:

#### REGRESSÃO COM UMA VARIÁVEL

#### DEPENDENTE BINÁRIA

```
Como discutimos, a análise discriminante é apropriada
quando a variável dependente é não-métrica. No entanto,
quando a variável dependente tem apenas dois grupos, a
regressão logística pode ser preferida por duas razões:
```
- A análise discriminante depende estritamente de se atende-
    rem as suposições de normalidade multivariada e de igual-
    dade entre as matrizes de variância-covariância nos grupos
    - suposições que não são atendidas em muitas situações. A
    regressão logística não depende dessas suposições rígidas e
    é muito mais robusta quando tais pressupostos não são sa-
    tisfeitos, o que torna sua aplicação apropriada em muitas
    situações.
- Mesmo quando os pressupostos são satisfeitos, muitos pes-
    quisadores preferem a regressão logística por ser similar à
    regressão múltipla. Ela tem testes estatísticos diretos, tra-
    tamentos similares para incorporar variáveis métricas e
    não-métricas e efeitos não-lineares, e uma vasta gama de
    diagnósticos.
Por essas e outras razões mais técnicas, a regressão lo-
gística é equivalente à análise discriminante de dois gru-
pos e pode ser mais adequada em muitas situações.
Nossa discussão de regressão logística não cobre cada
um dos seis passos do processo de decisão, mas destaca as
diferenças e semelhanças entre a regressão logística e a
análise discriminante ou a regressão múltipla. Para uma
revisão completa de regressão múltipla, ver o Capítulo 4.

#### Representação da variável dependente binária

```
Em análise discriminante, o caráter não-métrico de uma
variável dependente dicotômica é acomodado fazendo-se
previsões de pertinência a grupo baseadas em escores Z
discriminantes. Isso requer o cálculo de escores de corte e
a designação de observações a grupos.
A regressão logística aborda essa tarefa de uma ma-
neira mais semelhante à encontrada em regressão múlti-
pla. Regressão logística representa os dois grupos de inte-
resse como uma variável binária com valores de 0 e 1. Não
importa qual grupo é designado com o valor de 1 versus
0, mas tal designação deve ser observada para a interpre-
tação dos coefi cientes.
```
- Se os grupos representam características (p.ex., sexo), então
    um grupo pode ser designado com o valor 1 (p.ex., femini-
    no) e o outro grupo com o valor 0 (p.ex., masculino). Em tal
    situação, os coefi cientes refl etiriam o impacto das variáveis
    independentes sobre a probabilidade da pessoa ser do sexo
    feminino (ou seja, o grupo codifi cado como 1).
- Se os grupos representam resultados ou eventos (p.ex., su-
    cesso ou fracasso, compra ou não-compra), a designação dos
    códigos de grupos causa impacto na interpretação também.
    Considere que o grupo com sucesso é codifi cado como 1, e
    aquele com fracasso, como 0. Então, os coefi cientes repre-

```
que melhorem à medida que permanecerem clientes
ao longo do tempo.
```
- O grupo 2, clientes de 1 a 5 anos, tem semelhanças
    com os clientes mais novos e os mais antigos.
    Quanto às três variáveis de serviço à clientela, eles
    são comparáveis ao grupo 3 (mais de 5 anos). Para
    Qualidade de produto, Linha de produto e Preço
    competitivo, suas percepções são mais comparáveis
    com as dos clientes mais novos (e menores do que
    as dos clientes mais antigos). Eles mantêm as mais
    elevadas percepções, dos três grupos, quanto à
    Flexibilidade de preço.
- O grupo 3, representando os clientes há mais de 5
    anos, tem as mais favoráveis percepções da HBAT,
    como o esperado. Apesar de serem comparáveis
    aos clientes do grupo 2 quanto às três variáveis de
    serviço à clientela (com ambos os grupos maiores do
    que o grupo 1), eles são signifi cantemente maiores
    que os clientes nos outros dois grupos em termos
    de Qualidade de produto, Linha de produto e
    Preço competitivo. Assim, este grupo representa
    aqueles clientes que têm percepções positivas e
    têm progredido no estabelecimento de uma relação
    cliente/HBAT através de um fortalecimento de suas
    percepções.
- Usando os três grupos como indicadores no desenvolvi-
mento de relações de clientela, podemos identifi car dois
estágios nos quais as percepções HBAT mudam nesse
processo de desenvolvimento:
- _Estágio 1:_ O primeiro conjunto de percepções a
mudar é aquele relacionado a serviços a clientes
(visto nas diferenças entre os grupos 1 e 2). Este
estágio refl ete a habilidade da HBAT de afetar
positivamente percepções com operações relativas a
serviços.
- _Estágio 2:_ Um desenvolvimento de maior prazo é
necessário para promover melhoras em elementos
mais centrais (Qualidade de produto, Linha de
produto e Preço competitivo). Quando ocorrem
essas mudanças, o cliente deve se tornar mais
comprometido com a relação, como se evidencia por
uma longa permanência com a HBAT.
- Deve ser observado que existe evidência de que vários
clientes fazem a transição através do estágio 2 mais ra-
pidamente do que os cinco anos, como mostrado pelo
considerável número de clientes que têm sido do grupo
entre 1 e 5 anos, ainda que mantenham as mesmas per-
cepções da clientela mais antiga. Assim, HBAT pode
esperar que certos clientes possam se deslocar através
desse processo muito rapidamente, e uma análise mais
detalhada sobre tais clientes pode identifi car caracte-
rísticas que facilitam o desenvolvimento de relações
com a clientela.

```
( Continuação )
```

##### 284 Análise Multivariada de Dados

sentam os impactos sobre a probabilidade de sucesso. De
maneira igualmente fácil, os códigos poderiam ser inverti-
dos (1 agora denota fracasso) e os coefi cientes representa-
riam as forças que aumentam a probabilidade de fracasso.
A regressão logística difere da regressão múltipla, con-
tudo, no sentido de que ela foi especifi camente elaborada
para prever a probabilidade de um evento ocorrer (ou seja, a
probabilidade de uma observação estar no grupo codifi cado
como 1). Apesar de os valores de probabilidade serem me-
didas métricas, há diferenças fundamentais entre regressão
múltipla e logística.

##### Uso da curva logística

Como a variável dependente tem apenas os valores 0 e 1, o
valor previsto (probabilidade) deve ser limitado para cair
dentro do mesmo domínio. Para defi nir uma relação limi-
tada por 0 e 1, a regressão logística usa a **curva logística**
para representar a relação entre as variáveis independen-
tes e dependente (ver Figura 5-11). Em níveis muito bai-
xos da variável independente, a probabilidade se aproxima
de 0, mas nunca alcança tal valor. Analogamente, quan-
do a variável independente aumenta, os valores previstos
crescem para acima da curva, mas em seguida a inclina-
ção começa a diminuir de modo que em qualquer nível da
variável independente a probabilidade se aproximará de
1,0, mas jamais excederá tal valor. Como vimos em nos-
sas discussões sobre regressão, no Capítulo 4, os modelos
lineares de regressão não podem acomodar tal relação, já
que ela é inerentemente não-linear. A relação linear de re-
gressão, mesmo com termos adicionais de transformações
para efeitos não-lineares, não pode garantir que os valores
previstos permaneçam no intervalo de 0 a 1.

##### Natureza única da variável dependente

A natureza binária da variável dependente (0 ou 1) tem
propriedades que violam as suposições da regressão múl-
tipla. Primeiro, o termo de erro de uma variável discreta
segue a distribuição binomial ao invés da normal, invali-
dando assim todos os testes estatísticos que se sustentam

```
nas suposições de normalidade. Segundo, a variância de
uma variável dicotômica não é constante, criando casos
de heteroscedasticidade também. Além disso, nenhuma
violação pode ser remediada por meio de transformações
das variáveis dependente ou independentes.
A regressão logística foi desenvolvida para lidar espe-
cifi camente com essas questões. Não obstante, sua relação
única entre variáveis dependente e independentes exige
uma abordagem um tanto diferente para estimar a variá-
vel estatística, avaliar adequação de ajuste e interpretar os
coefi cientes, quando comparada com regressão múltipla.
```
#### Estimação do modelo de regressão logística

```
A regressão logística tem uma única variável estatística
composta de coefi cientes estimados para cada variável
independente – como na regressão múltipla. Tal variável
estatística é estimada de uma maneira diferente. A regres-
são logística deriva seu nome da transformação logit usa-
da com a variável dependente, criando diversas diferenças
no processo de estimação (bem como o processo de inter-
pretação discutido na próxima seção).
```
##### Transformação da variável dependente

```
Como mostrado anteriormente, o modelo logit usa a for-
ma específi ca da curva logística, que é em forma de S para
fi car no domínio de 0 a 1. Para estimar um modelo de re-
gressão logística, essa curva de valores previstos é ajustada
aos dados reais, exatamente como foi feito com uma rela-
ção linear em regressão múltipla. No entanto, como os va-
lores reais dos dados das variáveis dependentes podem ser
somente 0 ou 1, o processo é de algum modo diferente.
```
```
Nível da variável independente
```
```
Probabilidade do evento(variável dependente)
```
```
Alto
```
**FIGURA 5-11** Forma da relação logística entre variáveis dependente e independentes.

```
A Figura 5-12 retrata dois exemplos hipotéticos de ajus-
te de uma relação logística aos dados da amostra. Os
dados reais representam se um evento acontece ou não
designando valores 1 ou 0 aos resultados (neste caso 1 é
designado quando o evento ocorreu, 0 no caso contrário,
( Continua )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 285

```
Mas como prevemos pertinência a grupo a partir da
curva logística? Para cada observação, a técnica de regres-
são logística prevê um valor de probabilidade entre 0 e
```
1. O gráfi co dos valores previstos para todos os valores
da variável independente gera a curva exibida na Figura
5-12. Tal probabilidade prevista é baseada nos valores das
variáveis independentes e nos coefi cientes estimados. Se a
probabilidade prevista é maior do que 0,50, então a pre-
visão é de que o resultado seja 1 (o evento ocorreu); caso
contrário, o resultado é previsto como sendo 0 (o even-
to não ocorreu). Retornemos ao nosso exemplo para ver
como isso funciona.

```
mas tal atribuição poderia facilmente ser invertida). Ob-
servações são representadas pelos pontos no topo ou na
base do gráfi co. Esses resultados (que aconteceram ou
não) ocorrem em cada valor da variável independente (o
eixo X ). Na parte (a), a curva logística não pode ajustar
bem os dados porque há diversos valores da variável in-
dependente que têm ambos os resultados (1 e 0). Neste
caso, a variável independente não distingue entre os dois
resultados, como se mostra na considerável sobreposi-
ção dos dois grupos.
No entanto, na parte (b), uma relação muito melhor
defi nida está baseada na variável independente. Valores
menores da variável independente correspondem às ob-
servações com 0 para a variável dependente, enquanto
valores maiores correspondem bem àquelas observações
com um valor 1 sobre a variável dependente. Assim, a
curva logística deve ser capaz de ajustar bem os dados.
```
```
(a) Relação pobremente ajustada
```
```
(b) Relação bem definida
```
**FIGURA 5-12** Exemplos de ajuste da curva logística aos dados da amostra.

```
Nas partes (a) e (b) da Figura 5-12, um valor de 6,0 para
X (a variável independente) corresponde a uma proba-
bilidade de 0,50. Na parte (a), podemos ver que diversas
observações de ambos os grupos recaem em ambos os
lados deste valor, resultando em diversas classifi cações
```
```
( Continuação )
```
```
( Continua )
```

##### 286 Análise Multivariada de Dados

Logo, com uma curva logística estimada, podemos es-
timar a probabilidade para qualquer observação com base
em seus valores para as variáveis independentes e então
prever a pertinência a grupo usando 0,50 como valor de
corte. Uma vez que temos a pertinência prevista, podemos
criar uma matriz de classifi cação exatamente como foi fei-
to em análise discriminante e avaliar a precisão preditiva.

##### Estimação dos coefi cientes

De onde vem a curva? Em regressão múltipla, estimamos
uma relação linear que melhor ajusta os dados. Em re-
gressão logística, seguimos o mesmo processo de previ-
são da variável dependente por uma variável estatística
composta dos **coefi cientes logísticos** e as correspondentes
variáveis independentes. No entanto, o que difere é que
em regressão logística os valores previstos jamais podem
estar fora do domínio de 0 a 1. Apesar de uma discussão
completa sobre os aspectos conceituais e estatísticos en-
volvidos no processo de estimação estar além do escopo
deste texto, diversas fontes excelentes com tratamentos
completos sobre tais aspectos estão disponíveis [3,15,17].
Podemos descrever o processo de estimação em dois pas-
sos básicos à medida que introduzimos alguns termos co-
muns e fornecemos uma breve visão geral do processo.

**Transformação de uma probabilidade em razão de desi-
gualdade e valores logit.** Como na regressão múltipla, a
regressão logística prevê uma variável dependente métri-
ca, neste caso valores de probabilidade restritos ao domí-
nio entre 0 e 1. Mas como podemos garantir que valores
estimados não recaiam fora desse domínio? A transfor-
mação logística perfaz este processo em dois passos.

**_Reestabelecimento de uma probabilidade como ra-
zão de desigualdades._** Em sua forma original, probabi-
lidades não são restritas a valores entre 0 e 1. Portanto, o
que aconteceria se reestabelecêssemos a probabilidade de
uma maneira que a nova variável sempre fi casse entre 0
e 1? Fazemos isso expressando uma probabilidade como
razão de **desigualdades** – a razão entre as probabilidades
dos dois resultados ou eventos, Prob _i_ /( _1 –_ Prob _i_ ). Desta
forma, qualquer valor de probabilidade é agora dado em
uma variável métrica que pode ser diretamente estima-
da. Qualquer razão de desigualdade pode ser convertida
reciprocamente em uma probabilidade que fi ca entre 0 e

1. Resolvemos nosso problema de restrição dos valores
previstos entre 0 e 1 prevendo a razão de desigualdades e
então convertendo a mesma em uma probabilidade.

```
Usemos alguns exemplos da probabilidade de sucesso
ou fracasso para ilustrar como a razão de desigualdades
é calculada. Se a probabilidade de sucesso é 0,80, então
sabemos também que a probabilidade do resultado alter-
nativo (ou seja, o fracasso) é 0,20 (0,20 = 1,0 – 0,80). Esta
probabilidade signifi ca que as desigualdades de sucesso
são 4,0 (0,80/0,20), ou que o sucesso é quatro vezes mais
provável de acontecer do que o fracasso. Reciprocamen-
te, podemos estabelecer as desigualdades de fracasso
como 0,25 (0,20/0,80), ou, em outras palavras, o fracasso
acontece a um quarto da taxa de sucesso. Assim, qual-
quer que seja o resultado que busquemos (sucesso ou
fracasso), podemos estabelecer a probabilidade como
uma chance ou uma razão de desigualdades.
```
```
Como você provavelmente já desconfi ou, uma proba-
bilidade de 0,50 resulta em razão de desigualdades de 1,0
(ambos os resultados têm iguais chances de ocorrerem).
Razão de desigualdades inferior a 1,0 representa proba-
bilidades menores do que 0,50, e razão de desigualdades
maior do que 1,0 corresponde a uma probabilidade maior
do que 0,50. Agora temos uma variável métrica que sem-
pre pode ser convertida de volta a uma probabilidade en-
tre 0 e 1.
```
```
Cálculo do valor logit. A variável de razão de desi-
gualdades resolve o problema de fazer estimativas de pro-
babilidade entre 0 e 1, mas temos outro problema: como
fazemos com que as razões de desigualdades fi quem abai-
xo de 0, que é o limite inferior (não há limite superior).
A solução é computar aquilo que é chamado de valor lo-
git – calculado via logaritmo das razões de desigualdades.
Razões menores que 1,0 têm um logit negativo, razões
maiores que 1,0 têm valores logit positivos, e a razão de
desigualdades igual a 1,0 (correspondente a uma proba-
bilidade de 0,5) tem um valor logit de 0. Além disso, não
importa o quão baixo o valor negativo fi que, ele ainda
pode ser transformado tomando-se o anti-logaritmo em
uma razão de desigualdades maior que 0. O que se segue
mostra alguns valores típicos de probabilidade e as razões
de desigualdades correspondentes, bem como valores lo-
garítmicos.
```
```
Probabilidade
```
```
Razão de
desigualdades
```
```
Logaritmo
(Logit)
0,00 0,00 NC
0,10 0,111 –2,197
0,30 0,428 –0,847
0,50 1,000 0,000
0,70 2,333 0,847
0,90 9,000 2,197
1,00 NC NC
NC = Não pode ser calculado
```
```
ruins. As classifi cações ruins são mais perceptíveis para
o grupo com valores 1,0, ainda que diversas observações
no outro grupo (variável dependente = 0,0) também se-
jam mal classifi cadas. Na parte (b), fazemos classifi cação
perfeita dos dois grupos quando usamos o valor de pro-
babilidade de 0,50 como valor de corte.
```
```
( Continuação )
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 287

Com o valor logit, agora temos uma variável métrica
que pode ter valores positivos e negativos, mas que sem-
pre pode ser transformada de volta em um valor de pro-
babilidade entre 0 e 1. Observe, no entanto, que o logit
jamais pode realmente alcançar 0 ou 1. Esse valor agora
se torna a variável dependente do modelo de regressão
logística.

**Estimação do modelo.** Uma vez que compreendemos
como interpretar os valores das razões de desigualdades
ou das medidas logit, podemos proceder com o uso delas
como medida dependente em nossa regressão logística.
O processo de estimação dos coefi cientes logísticos é se-
melhante àquele usado em regressão, apesar de que nes-
te caso somente dois valores reais são empregados para
a variável dependente (0 e 1). Além do mais, em vez de
usar os mínimos quadrados ordinários como meio para
estimar o modelo, o método de verossimilhança máxima
é utilizado.

**_Estimação dos coefi cientes._** Os coefi cientes esti-
mados para as variáveis independentes são estimados
usando-se o valor logit ou a razão de desigualdades como
medida dependente. Cada uma dessas formulações de
modelo é exibida aqui:

ou

Ambas as formulações de modelo são equivalentes,
mas aquela que for escolhida afetará a estimação dos co-
efi cientes. Muitos programas de computador fornecem
os coefi cientes logísticos em ambas as formas, de modo
que o pesquisador deve entender como interpretar cada
forma. Discutimos aspectos interpretativos em uma seção
posterior.
Este processo pode acomodar uma ou mais variáveis
independentes, e estas podem ser métricas ou não-métri-
cas (binárias). Como vemos adiante em nossa discussão
sobre interpretação dos coefi cientes, ambas as formas dos
mesmos refl etem a direção e a magnitude da relação, mas
são interpretadas de maneiras distintas.

**_Uso da máxima verossimilhança para estima-
ção._** Regressão múltipla emprega o método de mínimos
quadrados, que minimiza a soma das diferenças quadradas
entre os valores reais e previstos da variável dependente.
A natureza não-linear da transformação logística requer
que outro procedimento, o da máxima verossimilhança,

```
seja usado de maneira iterativa para que se encontrem as
estimativas mais prováveis para os coefi cientes. No lugar
de minimizar os desvios quadrados (mínimos quadrados),
a regressão logística maximiza a probabilidade de que
um evento ocorra. O valor de probabilidade, ao invés da
soma de quadrados, é em seguida usado quando se calcula
uma medida de ajuste geral do modelo. Usar esta técnica
alternativa de estimação também demanda que avaliemos
o ajuste do modelo de diferentes maneiras.
```
#### Avaliação da qualidade do ajuste

#### do modelo de estimação

```
A qualidade de ajuste para um modelo de regressão lo-
gística pode ser avaliada de duas maneiras. Uma é a ava-
liação de ajuste usando valores “pseudo” R^2 , semelhantes
àqueles encontrados em regressão múltipla. A segunda
abordagem é examinar precisão preditiva (como a matriz
de classifi cação em análise discriminante). As duas técni-
cas examinam ajuste de modelo sob diferentes perspecti-
vas, mas devem conduzir a conclusões semelhantes.
```
##### Ajuste de estimação do modelo

```
A medida básica do quão bem o procedimento de esti-
mação de máxima verossimilhança se ajusta é o valor de
verossimilhança , semelhante aos valores das somas de
quadrados usadas em regressão múltipla. Regressão logís-
tica mede o ajuste da estimação do modelo com o valor –2
vezes o logaritmo do valor da verossimilhança, chamado
de –2 LL ou –2log verossimilhança. O valor mínimo para
–2 LL é 0, o que corresponde a um ajuste perfeito (veros-
similhança = 1 e –2 LL é então 0). Assim, quanto menor
o valor –2 LL , melhor o ajuste do modelo. Como será dis-
cutido na próxima seção, o valor –2 LL pode ser usado
para comparar equações quanto à variação no ajuste ou
ser utilizado para calcular medidas comparáveis ao R^2 em
regressão múltipla.
```
```
Entre comparações de modelos. O valor de verossimi-
lhança pode ser comparado entre equações para avaliar a
diferença em ajuste preditivo de uma equação para outra,
com testes estatísticos para a signifi cância dessas diferen-
ças. O método básico segue três passos:
```
**1.** _Estimar um modelo nulo._ O primeiro passo é calcular um
    modelo nulo, que atua como a referência para fazer com-
    parações de melhoramento no ajuste do modelo. O modelo
    nulo mais comum é um sem variáveis independentes, que
    é semelhante a calcular a soma total de quadrados usando
    somente a média em regressão múltipla. A lógica por trás
    desta forma de modelo nulo é que ele pode atuar como uma
    referência em relação à qual qualquer modelo contendo va-
    riáveis independentes pode ser comparado.
**2.** _Estimar o modelo proposto._ Este modelo contém as variá-
    veis independentes a serem incluídas no modelo de regres-
    são logística. Espera-se que o ajuste melhorará em relação
    ao modelo nulo e que resulte em um valor menor de _–_ 2 _LL_.


##### 288 Análise Multivariada de Dados

```
Qualquer número de modelos propostos pode ser estimado
(p.ex., modelos com uma, duas e três variáveis independen-
tes podem ser propostas distintas).
```
**3.** _Avaliar a diferença –2LL_. O passo fi nal é avaliar a signifi -
    cância estatística do valor _–_ 2 _LL_ entre os dois modelos (nulo
    versus proposto). Se os testes estatísticos suportam diferen-
    ças signifi cantes, então podemos estabelecer que o conjunto
    de variáveis independentes no modelo proposto é signifi -
    cante na melhora do ajuste da estimação do mesmo.
De maneira semelhante, comparações também po-
dem ser feitas entre dois modelos propostos quaisquer.
Em tais casos, a diferença _–_ 2 _LL_ refl ete a diferença em
ajuste de modelo devido a distinções de especifi cações.
Por exemplo, um modelo com duas variáveis indepen-
dentes pode ser comparado com um modelo de três va-
riáveis independentes para que se avalie a melhora pelo
acréscimo de uma variável. Nesses casos, um modelo é
escolhido para atuar como nulo e então é comparado
com outro.

```
Por exemplo, considere que queremos testar a signifi -
cância de um conjunto de variáveis independentes cole-
tivamente para ver se elas melhoram o ajuste do modelo.
O modelo nulo seria especifi cado como um modelo sem
essas variáveis, e o modelo proposto incluiria as variá-
veis a serem avaliadas. A diferença em – 2 LL signifi caria
a melhora a partir do conjunto de variáveis independen-
tes. Poderíamos fazer testes similares das diferenças em
```
_-_ 2 _LL_ entre outros pares de modelos variando o número
de variáveis independentes incluídas em cada um.

O teste do qui-quadrado e o teste associado para sig-
nifi cância estatística são usados para se avaliar a redução
no logaritmo do valor de verossimilhança. No entanto,
esses testes estatísticos são particularmente sensíveis a ta-
manho de amostra (para amostras pequenas é mais difícil
mostrar signifi cância estatística, e vice-versa para grandes
amostras). Portanto, pesquisadores devem ser particular-
mente cuidadosos ao tirarem conclusões com base apenas
na signifi cância do teste do qui-quadrado em regressão
logística.

**Medidas pseudo** **_R_**^2**.** Além dos testes qui-quadrado,
diversas medidas do tipo _R_^2 foram desenvolvidas e são
apresentadas em vários programas estatísticos para repre-
sentarem ajuste geral do modelo. Essas medidas pseudo
_R_^2 são interpretadas de uma maneira parecida com o co-
efi ciente de determinação em regressão múltipla. Um va-
lor **pseudo** **_R_**^2 pode ser facilmente obtido para regressão
logística semelhante ao valor _R_^2 em análise de regressão
[6]. O pseudo _R_^2 para um modelo logit ( _R_^2 logit ) pode ser
calculado como

```
Exatamente como na contraparte da regressão múl-
tipla, o valor R^2 logit varia de 0,0 a 1,0. À medida que o
modelo proposto aumenta o ajuste, o – 2 LL diminui. Um
ajuste perfeito tem um valor de − 2 LL igual a 0,0 e um
R^2 LOGIT de 1,0.
Duas outras medidas são semelhantes ao valor pseudo
R^2 e são geralmente categorizadas também como medidas
pseudo R^2. A medida R^2 de Cox e Snell opera do mes-
mo modo, com valores maiores indicando maior ajuste do
modelo. No entanto, esta medida é limitada no sentido de
que não pode atingir o valor máximo de 1, de forma que
Nagelkerke propôs uma modifi cação que tinha o domínio
de 0 a 1. Essas duas medidas adicionais são interpretadas
como refl etindo a quantia de variação explicada pelo mo-
delo logístico, com 1,0 indicando ajuste perfeito.
```
```
Uma comparação com regressão múltipla. Ao discutir
os procedimentos para avaliação de ajuste de modelo em
regressão logística, fazemos várias referências a similari-
dades com regressão múltipla em termos de diversas me-
didas de ajuste. Na tabela a seguir, mostramos a corres-
pondência entre conceitos usados em regressão múltipla e
suas contrapartes em regressão logística.
```
```
Correspondência de elementos primários de
ajuste de modelo
Regressão múltipla Regressão logística
Soma total de quadrados –2 LL do modelo base
Soma de quadrados do erro–2 LL do modelo proposto
Soma de quadrados da
regressão
```
```
Diferença de – LL* para
modelos base e proposto
Teste F de ajuste de mo-
delo
```
```
Teste de qui-quadrado da
diferença –2 LL
Coefi ciente de determina-
ção ( R^2 )
```
```
Medidas pseudo R^2
```
```
Como podemos ver, os conceitos de regressão múltipla
e regressão logística são semelhantes. Os métodos básicos
para testar ajuste geral do modelo são comparáveis, com
as diferenças surgindo dos métodos de estimação nas duas
técnicas.
```
##### Precisão preditiva

```
Assim como emprestamos o conceito de R^2 da regressão
como uma medida de ajuste geral de modelo, podemos pro-
curar na análise discriminante a medida de precisão prediti-
va geral. As duas técnicas mais comuns são a matriz de clas-
sifi cação e as medidas de ajuste baseadas no qui-quadrado.
```
```
Matriz de classifi cação. Esta técnica de matriz de classi-
fi cação é idêntica àquela usada em análise discriminante,
ou seja, medir o quão bem a pertinência a grupo é prevista
e desenvolver uma razão de sucesso. O caso da regressão
```
```
* N. de R. T.: A frase correta seria “Diferença de –2LL”.
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 289

logística sempre incluirá somente dois grupos, mas todas
as medidas relacionadas a chances (p.ex., chance máxima,
chance proporcional ou _Q_ de Press) usadas anteriormente
são aplicáveis aqui também.

**Medida baseada no qui-quadrado.** Hosmer e Lemeshow
[11] desenvolveram um teste de classifi cação no qual os
casos são primeiramente divididos em aproximadamen-
te 10 classes iguais. Em seguida, os números de eventos
reais e previstos são comparados em cada classe com a
estatística qui-quadrado. Esse teste fornece uma medida
ampla de precisão preditiva que é baseada não no valor
de verossimilhança, mas sim na real previsão da variável
dependente. O uso apropriado desse teste requer um ta-
manho de amostra de pelo menos 50 casos para garantir
que cada classe tenha pelo menos cinco observações e ge-
ralmente até mesmo uma amostra maior, uma vez que o
número de eventos previstos nunca fi ca abaixo de 1. Além
disso, a estatística qui-quadrado é sensível a tamanho da
amostra, permitindo assim que essa medida encontre di-
ferenças muito pequenas, estatisticamente signifi cantes,
quando o tamanho da amostra se torna grande.
Tipicamente examinamos tantas dessas medidas de
ajuste de modelo quanto possível. Espera-se que uma con-
vergência de indicações dessas medidas forneça o suporte
necessário ao pesquisador para a avaliação do ajuste geral
do modelo.

#### Teste da signifi cância dos coefi cientes

A regressão logística testa hipóteses sobre coefi cientes in-
dividuais, como se faz na regressão múltipla. Em regressão
múltipla, o teste estatístico era para ver se o coefi ciente era
signifi cantemente diferente de 0. Um coefi ciente nulo indi-
ca que o mesmo não tem impacto sobre a variável depen-
dente. Em regressão logística, usamos também um teste
estatístico para ver se o coefi ciente logístico é diferente de

0. Lembre, contudo, que em regressão logística usando o
logit como medida dependente, um valor de 0 corresponde
à razão de desigualdade de 1,00 ou uma probabilidade de
0,50 – valores que indicam que a probabilidade é igual para
cada grupo (i.e., novamente nenhum efeito da variável in-
dependente sobre a previsão de pertinência ao grupo).
    Em regressão múltipla, o valor _t_ é utilizado para ava-
liar a signifi cância de cada coefi ciente. Regressão logística
usa uma estatística diferente, a **estatística Wald**. Ela provê
a signifi cância estatística para cada coefi ciente estimado de
forma que testes de hipóteses podem ocorrer exatamente
como se faz em regressão múltipla. Se o coefi ciente logísti-
co é estatisticamente signifi cante, podemos interpretá-lo em
termos de como o mesmo impacta a probabilidade estimada
e conseqüentemente a previsão de pertinência a grupo.

#### Interpretação dos coefi cientes

Uma das vantagens da regressão logística é que precisa-
mos saber apenas se um evento (compra ou não, risco de

```
crédito ou não, falência de empresa ou sucesso) ocorreu
ou não para defi nir um valor dicotômico como nossa va-
riável dependente. No entanto, quando analisamos es-
ses dados usando transformação logística, a regressão e
seus coefi cientes assumem um signifi cado algo diferente
daqueles encontrados na regressão com uma variável de-
pendente métrica. Analogamente, cargas discriminantes
de uma análise discriminante de dois grupos são interpre-
tadas diferentemente a partir de um coefi ciente logístico.
A partir do processo de estimação descrito anterior-
mente, sabemos que os coefi cientes ( B 0 , B 1 , B 2 , ..., Bn )
são na verdade medidas das variações na proporção das
probabilidades (as razões de desigualdades). No entanto,
coefi cientes logísticos são difíceis de interpretar em sua
forma original, pois eles são expressos em termos de lo-
garitmos quando usamos o logit como a medida depen-
dente. Assim, a maioria dos programas de computador
fornece também um coefi ciente logístico exponenciado ,
que é apenas uma transformação (anti-logaritmo) do co-
efi ciente logístico original. Desse modo, podemos usar os
coefi cientes logísticos originais ou exponenciados para a
interpretação. Os dois tipos de coefi cientes logísticos dife-
rem no sentido da relação da variável independente com
as duas formas da dependente, como mostrado aqui:
```
```
Coefi ciente logístico Refl ete mudanças em...
Original Logit (logaritmo da razão
de desigualdades)
Exponenciado Razão de desigualdades
```
```
Discutimos na próxima seção como cada forma do
coefi ciente refl ete direção e magnitude da relação da va-
riável independente, mas requer diferentes métodos de
interpretação.
```
##### Direção da relação

```
A direção da relação (positiva ou negativa) refl ete as mu-
danças na variável dependente associadas com mudanças
na independente. Uma relação positiva signifi ca que um
aumento na variável independente é associado com um
aumento na probabilidade prevista, e vice-versa para uma
relação negativa. Veremos que a direção da relação é re-
fl etida diferentemente nos coefi cientes logísticos original
e exponenciado.
```
```
Interpretação da direção de coefi cientes originais. O si-
nal dos coefi cientes originais (positivo ou negativo) indica
a direção da relação, como foi visto nos coefi cientes de
regressão. Um valor positivo aumenta a probabilidade,
enquanto um negativo diminui a mesma, pois os coefi -
cientes originais são expressos em termos de valores logit,
onde um valor de 0,0 corresponde a um valor de razão de
desigualdade de 1,0 e uma probabilidade de 0,50. Assim,
números negativos são relativos a razões de desigualdades
menores que 1,0 e probabilidades menores que 0,50.
```

##### 290 Análise Multivariada de Dados

**Interpretação da direção de coefi cientes exponenciados.**
Coefi cientes exponenciados devem ser interpretados di-
ferentemente, pois eles são os logaritmos dos coefi cientes
originais. Considerando o logaritmo, estamos na verdade
estabelecendo o coefi ciente exponenciado em termos de
razões de desigualdades, o que signifi ca que exponencia-
dos não terão valores negativos. Como o logaritmo de 0
(sem efeito) é 1,0, um coefi ciente exponenciado igual a
1,0 na verdade corresponde a uma relação sem direção.
Assim, coefi cientes exponenciados acima de 1,0 refl etem
uma relação positiva, e valores menores que 1,0 represen-
tam relações negativas.

**Um exemplo de interpretação.** Examinemos um exem-
plo simples para ver o que queremos dizer em termos de
diferenças entre as duas formas de coefi cientes logísticos.

```
Se Bi (o coefi ciente original) é positivo, sua transforma-
ção (exponencial do coefi ciente) será maior que 1, o que
signifi ca que a razão de desigualdade aumentará para
qualquer variação positiva da variável independente. As-
sim, o modelo tem uma maior probabilidade prevista de
ocorrência. De modo semelhante, se Bi é negativo, o coe-
fi ciente exponenciado é menor que um e a razão de desi-
gualdades diminui. Um coefi ciente de zero se iguala a um
valor de 1,0 no coefi ciente exponenciado, o que resulta
em nenhuma mudança na razão de desigualdades.
```
Uma discussão mais detalhada da interpretação de
coefi cientes, transformação logística e procedimentos de
estimação pode ser encontrada em diversos textos [11].

##### Magnitude da relação

Para determinar quanto da probabilidade mudará dada
uma variação de uma unidade na variável independente,
o valor numérico do coefi ciente deve ser avaliado. Exa-
tamente como na regressão múltipla, os coefi cientes para
variáveis métricas e não-métricas devem ser interpretados
de forma diferenciada, pois cada um refl ete diferentes im-
pactos sobre a variável dependente.

**Interpretação da magnitude de variáveis independentes
métricas.** Para variáveis métricas, a questão é: quanto
a probabilidade estimada varia por conta de uma varia-
ção unitária na variável independente? Em regressão
múltipla, sabíamos que o coefi ciente de regressão era
o coefi ciente angular da relação linear entre a medida
independente e a dependente. Um coefi ciente de 1,35
indicava que a variável dependente aumentava 1,35 uni-
dades cada vez que a variável independente aumentava
uma unidade. Em regressão logística, sabemos que te-
mos uma relação não-linear limitada entre 0 e 1, e assim
os coefi cientes devem ser interpretados de forma dife-
rente. Além disso, temos os dois coefi cientes original e
exponenciado para considerar.

```
Coefi cientes logísticos originais. Apesar de mais
apropriados para determinarem a direção da relação, os
coefi cientes logísticos originais são menos úteis na deter-
minação da magnitude da relação. Eles refl etem a varia-
ção no valor logit (logaritmo da razão de desigualdades),
uma unidade de medida particularmente não compreen-
sível na representação do quanto as probabilidades real-
mente variam.
```
```
Coefi cientes logísticos exponenciados. Coefi cien-
tes exponenciados refl etem diretamente a magnitude da
variação no valor da razão de desigualdades. Por serem
expoentes, eles são interpretados de maneira ligeiramen-
te diferente. Seu impacto é multiplicativo, o que signifi ca
que o efeito do coefi ciente não é adicionado à variável
dependente (a razão de desigualdades), mas multiplica-
do para cada variação unitária na variável independente.
Como tal, um coefi ciente exponenciado de 1,0 denota
mudança nenhuma (1,0 × variável independente = mu-
dança nenhuma). Este resultado corresponde à nossa
discussão anterior, onde coefi cientes exponenciados me-
nores que 1,0 refl etem relações negativas, enquanto va-
lores acima de 1,0 denotam relações positivas.
```
```
Um exemplo de avaliação da magnitude de variação.
Talvez uma abordagem mais fácil para determinar a
quantia de variação na probabilidade a partir desses va-
lores seja como se segue:
Mudança percentual na razão de desigualdades =
(coefi ciente exponenciado i – 1,0) × 100
Os exemplos a seguir ilustram como calcular a varia-
ção de probabilidade devido a uma variação unitária na
variável independente para um domínio de coefi cientes
exponenciados:
```
```
Valor
Coefi ciente expo-
nenciado ( e b i )
```
###### 0,20 0,50 1,0 1,5 1,7

```
e b i – 1,0 $0,80 $0,50 0,0 0,50 0,70
Variação percentu-
al na razão de desi-
gualdades
```
###### $80% $50% 0% 50% 70%

```
Se o coefi ciente exponenciado é 0,20, uma mudança
de uma unidade na variável independente reduzirá a
razão de desigualdades em 80% (o mesmo se a razão
de desigualdades fosse multiplicada por 0,20). Analo-
gamente, um coefi ciente exponenciado de 1,5 denota
um aumento de 50% na razão de desigualdades.
```
```
Um pesquisador que conhece a razão de desigualda-
des existente e deseja calcular o novo valor dessa razão
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 291

para uma mudança na variável independente pode fazê-lo
diretamente através do coefi ciente exponenciado, como
se segue:

Novo valor de razão de desigualdade = Valor antigo
× Coefi ciente exponenciado × Variação na variável
independente
Usemos um exemplo simples para ilustrar a maneira
como o coefi ciente exponenciado afeta o valor da razão
de desigualdades.

```
Considere que a razão de desigualdade é 1,0 (ou seja,
50-50) quando a variável independente tem um valor de
5,5 e o coefi ciente exponenciado é 2,35. Sabemos que se
este coefi ciente for maior do que 1,0, então a relação é
positiva, mas gostaríamos de saber o quanto a razão de
desigualdades mudaria. Se esperamos que o valor da va-
riável independente aumente 1,5 pontos para 7,0, pode-
mos calcular o seguinte:
Nova razão de desigualdades = 1,0 × 2,35
× (7,0 – 5,5)! 3,525
Razões de desigualdades podem ser traduzidas em
termos de valores de probabilidade pela fórmula simples
de Probabilidade = Razão de desigualdades/(1+Razão
de desigualdades). Logo, a razão de 3,525 se traduz em
uma probabilidade de 77,9% (3,25/(1 + 3,25)= 0,779), in-
dicando que um aumento na variável independente de
um ponto e meio aumenta a probabilidade de 50% para
78%, um aumento de 28%.
A natureza não-linear da curva logística é demons-
trada, porém, quando novamente aplicamos o mesmo
aumento à razão de desigualdades. Dessa vez, considere
que a variável independente aumenta mais 1,5 pontos,
para 8,5. Podemos esperar que a probabilidade aumente
outros 28%? Não, pois isso faria a probabilidade ultra-
passar os 100% (78% + 28% = 106%). Assim, o aumen-
to ou diminuição da probabilidade diminui à medida que
a curva se aproxima, mas jamais alcança, os dois pontos
extremos (0 e 1). Neste exemplo, outro aumento de 1,5
cria um novo valor de razão de desigualdades de 12,426,
traduzindo-se como uma razão de desigualdades de
92,6%, um aumento de 14%. Observe que neste caso de
aumento de probabilidade a partir de 78%, o aumento
na mesma para a variação de 1,5 na variável indepen-
dente é metade (14%) daquilo que foi para o mesmo au-
mento quando a probabilidade era de 50%.
```
O pesquisador pode descobrir que coefi cientes expo-
nenciados são bastante úteis não apenas na avaliação do
impacto de uma variável independente, mas no cálculo da
magnitude dos efeitos.

**Interpretação da magnitude para variáveis independentes
não-métricas (dicotômicas).** Como discutimos em re-

```
gressão múltipla, variáveis dicotômicas representam uma
única categoria de uma variável não-métrica (ver Capítulo
4 para uma discussão mais detalhada sobre o tema). Como
tais, elas não são como variáveis métricas que variam em
um intervalo de valores, mas assumem apenas os valores
de 1 ou 0, indicando a presença ou ausência de uma carac-
terística. Como vimos na discussão anterior para variáveis
métricas, os coefi cientes exponenciados são a melhor ma-
neira de interpretar o impacto da variável dicotômica, mas
são interpretados diferentemente das variáveis métricas.
Sempre que uma variável dicotômica é usada, é essen-
cial notar a categoria de referência ou omitida. Em uma
maneira semelhante à interpretação em regressão, o co-
efi ciente exponenciado representa o nível relativo da va-
riável dependente para o grupo representado versus o
grupo omitido. Podemos estabelecer essa relação como se
segue:
```
```
Usemos um exemplo simples de dois grupos para ilus-
trar esses pontos.
```
```
Se a variável não-métrica é sexo, as duas possibilidades
são masculino e feminino. A variável dicotômica pode
ser defi nida como representando homens (i.e., valor 1 se
for homem e 0 se for mulher) ou mulheres (i.e., valor
1 se for mulher e 0 se for homem). Qualquer que seja
o caminho escolhido, porém, ele se determina como o
coefi ciente é interpretado. Consideremos que um valor
1 é dado às mulheres, fazendo com que o coefi ciente
exponenciado represente o percentual da razão de de-
sigualdades de mulheres comparada com homens. Se o
coefi ciente é 1,25, então as mulheres têm uma razão de
desigualdades 25% maior do que os homens (1,25 – 1,0 =
0,25). Analogamente, se o coefi ciente é 0,80, então a ra-
zão de desigualdades para mulheres é 20% menor (0,80
```
- 1,0 = _–_ 0,20) do que para os homens.

##### Cálculo de probabilidades para um valor

##### específi co da variável independente

```
Na discussão anterior da distribuição assumida de possí-
veis variáveis dependentes, descrevemos uma curva em
forma de S, ou logística. Para representar a relação entre
as variáveis dependente e independentes, os coefi cientes
devem, na verdade, representar relações não-lineares
entre as variáveis dependente e independentes. Apesar
de o processo de transformação que envolve logaritmos
fornecer uma linearização da relação, o pesquisador deve
lembrar que os coefi cientes na verdade correspondem a
diferentes coefi cientes angulares na relação ao longo dos
valores da variável independente. Desse modo, a distri-
buição em forma de S pode ser estimada. Se o pesquisa-
```

##### 292 Análise Multivariada de Dados

dor estiver interessado no coefi ciente angular da relação
em vários valores da variável independente, os coefi cien-
tes podem ser calculados e a relação, avaliada [6].

##### Visão geral da interpretação dos coefi cientes

A similaridade dos coefi cientes com aqueles encontrados
em regressão múltipla tem sido uma razão prioritária para
a popularidade da regressão logística. Como vimos na dis-
cussão anterior, muitos aspectos são bastante semelhan-
tes, mas o caráter único da variável dependente (a razão
de desigualdades) e a forma logarítmica da variável esta-
tística (necessitando uso dos coefi cientes exponenciados)
requer uma abordagem de algum modo de interpretação
diferente. O pesquisador, contudo, ainda tem a habilidade
para avaliar a direção e a magnitude do impacto de cada
variável independente sobre a medida dependente e, em
última instância, a precisão de classifi cação do modelo lo-
gístico.

#### Resumo

O pesquisador que se defronta com uma variável depen-
dente dicotômica não precisa apelar para métodos elabo-
rados para acomodar as limitações da regressão múltipla,
e nem precisa ser forçado a empregar a análise discrimi-
nante, especialmente se suas suposições estatísticas são
violadas. A regressão logística aborda esses problemas e
fornece um método desenvolvido para lidar diretamente
com essa situação da maneira mais efi ciente possível.

#### UM EXEMPLO ILUSTRATIVO

#### DE REGRESSÃO LOGÍSTICA

A regressão logística é uma alternativa atraente à análise
discriminante sempre que a variável dependente tem ape-
nas duas categorias. Suas vantagens em relação à análise
discriminante incluem as seguintes:

**1.** É menos afetada do que a análise discriminante pelas de-
    sigualdades de variância-covariância ao longo dos grupos,
    uma suposição básica da análise discriminante.
**2.** Lida facilmente com variáveis independentes categóricas,
    enquanto na análise discriminante o uso de variáveis dico-
    tômicas cria problemas com igualdades de variância-cova-
    riância.
**3.** Os resultados empíricos acompanham paralelamente os da
    regressão múltipla em termos de sua interpretação e das
    medidas diagnósticas de casos disponíveis para exame de
    resíduos.
O exemplo a seguir, idêntico ao da análise discrimi-
nante de dois grupos discutido anteriormente, ilustra essas
vantagens e a similaridade da regressão logística com os
resultados obtidos da regressão múltipla. Como veremos,
ainda que a regressão logística tenha muitas vantagens
como alternativa à análise discriminante, o pesquisador
deve interpretar cuidadosamente os resultados devido aos

```
aspectos ímpares de como a regressão logística lida com a
previsão de probabilidades e de pertinência a grupos.
```
#### Estágios 1, 2 e 3: Objetivos da

#### pesquisa, planejamento de pesquisa

#### e suposições estatísticas

```
As questões abordadas nos primeiros três estágios do pro-
cesso de decisão são idênticas para a análise discriminante
de dois grupos e para a regressão logística.
```
```
O problema de pesquisa ainda é determinar se as dife-
renças de percepções de HBAT ( X 6 a X 18 ) existem entre
os clientes dos EUA/América do Norte e aqueles do res-
to do mundo ( X 4 ). A amostra de 100 clientes é dividida
em uma amostra de análise de 60 observações, com as
40 observações restantes constituindo a amostra de va-
lidação.
```
```
Agora nos concentramos sobre os resultados obtidos
a partir do uso de regressão logística para estimar e com-
preender as diferenças entre esses dois tipos de clientes.
```
#### Estágio 4: Estimação do modelo de regressão

#### logística e avaliação do ajuste geral

```
Antes que comece o processo de estimação, é possível
rever as variáveis individuais e avaliar seus resultados
univariados em termos de diferenciação entre grupos.
Sabendo-se que os objetivos da análise discriminante e da
regressão logística são os mesmos, podemos usar as mes-
```
##### Regressão logística

- Regressão logística é o método preferido para variáveis
    dependentes de dois grupos (binárias) devido à sua
    robustez, facilidade de interpretação e diagnóstico
- Testes de signifi cância de modelo são feitos com um
    teste de qui-quadrado sobre as diferenças no logaritmo
    da verossimilhança ( _–_ 2 _LL_ ) entre dois modelos
- Coefi cientes são expressos em duas formas: original e
    exponenciado, para auxiliar na interpretação
- A interpretação dos coefi cientes quanto a direção e
    magnitude é:
    - Direção pode ser avaliada diretamente nos
       coefi cientes originais (sinais positivos ou negativos)
       ou indiretamente nos exponenciados (menor que 1 é
       negativa e maior que 1 é positiva)
    - Magnitude é avaliada melhor pelo coefi ciente
       exponenciado, com a variação percentual na variável
       dependente mostrada por:
          Variação percentual = (Coefi ciente exponenciado –
             1,0) × 100

###### REGRAS PRÁTICAS 5-5


##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 293

mas medidas de discriminação para avaliar efeitos univa-
riados, como foi feito para a análise discriminante.

```
Se revisarmos nossa discussão a respeito das diferenças
dos grupos quanto às 13 variáveis independentes (olhar
a Tabela 5-5), lembraremos que cinco variáveis ( X 6 , X 11 ,
X 12 , X 13 , e X 17 ) tinham diferenças estatisticamente signi-
fi cantes entre os dois grupos. Se você olhar novamente a
discussão no exemplo de dois grupos, lembre de uma in-
dicação de multicolinearidade entre essas variáveis, pois
ambas X 6 e X 13 eram parte do fator Valor do produto
derivado pela análise fatorial (ver Capítulo 3). A regres-
são logística é afetada por multicolinearidade entre as
variáveis independentes de uma maneira semelhante à
análise discriminante e análise de regressão.
```
Exatamente como em análise discriminante, essas
cinco variáveis seriam as candidatas lógicas para inclu-
são na variável estatística de regressão logística, pois elas
demonstram as maiores diferenças entre grupos. Regres-
são logística pode incluir uma ou mais dessas variáveis no
modelo, bem como outras variáveis que não apresentam
diferenças signifi cantes neste estágio se elas operam em
combinação com outras variáveis para signifi cativamente
melhorar a previsão.

##### Estimação do modelo

A regressão logística é estimada de maneira análoga à re-
gressão múltipla, no sentido de que um modelo base é pri-
meiramente estimado para fornecer um padrão para com-
paração (ver discussão anterior para maiores detalhes).
Em regressão múltipla, a média é usada para estabelecer

```
o modelo base e calcular a soma total de quadrados. Em
regressão logística, o mesmo processo é empregado, com
a média usada no modelo estimado não para estabelecer a
soma de quadrados, mas para estabelecer o valor do loga-
ritmo da verossimilhança. A partir desse modelo, podem
ser estabelecidas as correlações parciais para cada variá-
vel e a variável mais discriminante pode ser escolhida de
acordo com os critérios de seleção.
```
```
Estimação do modelo base. A Tabela 5-25 contém os
resultados do modelo base para a análise de regressão lo-
gística. O valor do logaritmo da verossimilhança (–2 LL )
aqui é 82,108. A estatística escore, uma medida de asso-
ciação usada em regressão logística, é a medida usada
para selecionar variáveis no procedimento stepwise. Di-
versos critérios podem ser empregados para orientar a
entrada: maior redução no valor –2 LL , maior coefi ciente
de Wald, ou maior probabilidade condicional. Em nosso
exemplo, empregamos o critério da redução da razão do
logaritmo da verossimilhança.
Ao revermos a estatística de escores de variáveis não
presentes no modelo neste momento, percebemos que as
mesmas cinco variáveis com diferenças estatisticamente
signifi cantes ( X 6 , X 11 , X 12 , X 13 e X 17 ) também são s únicas
variáveis com estatística de escore signifi cante na Tabela
5-25. Como o procedimento stepwise seleciona a variável
com a maior estatística de escore, X 13 deve ser a variável
adicionada no primeiro passo.
```
```
Estimação stepwise : adição da primeira variável,
X 13. Como esperado, X 13 foi escolhida para entrada
no primeiro passo do processo de estimação (ver Tabela
```
```
TABELA 5-25 Resultados do modelo base da regressão logística
Ajuste geral do modelo: medidas da qualidade do ajuste
Valor
–2 Logaritmo de verossimilhança (–2 LL ) 82,108
```
```
Variáveis fora da equação
Variáveis independentes Estatística de escore Signifi cância
X 6 Qualidade do produto 11,925 0,001
X 7 Atividades de comércio eletrônico 2,052 0,152
X 8 Suporte técnico 1,609 0,205
X 9 Solução de reclamação 0,866 0,352
X 10 Anúncio 0,791 0,374
X 11 Linha do produto 18,323 0,000
X 12 Imagem da equipe de venda 8,622 0,003
X 13 Preços competitivos 21,330 0,000
X 14 Garantia e reclamações 0,465 0,495
X 15 Novos produtos 0,614 0,433
X 16 Encomenda e cobrança 0,090 0,764
X 17 Flexibilidade de preço 21,204 0,000
X 18 Velocidade de entrega 0,157 0,692
```
```
( Continua )
```

##### 294 Análise Multivariada de Dados

```
TABELA 5-26 Estimação stepwise da regressão logística: Adição de X 13 (Preços competitivos)
Ajuste geral do modelo: medidas da qualidade de ajuste
VARIAÇÃO EM –2 LL
Do modelo base Do passo anterior
Valor Variação Signifi cância Variação Signifi cância
–2 Logaritmo de verossimilhança (–2 LL ) 56,971 25,136 0,000 25,136 0,000
R^2 de Cox e Snell 0,342
R^2 de Nagelkerke 0,459
Pseudo R^2 0,306
```
```
Valor Signifi cância
%^2 de Hosmer e Lemeshow 17,329 0,027
```
```
Variáveis na equação
```
```
Variável independente B Erro padrão Wald df Sig. Exp(B)
X 13 Preços competitivos 1,129 0,287 15,471 1 0,000 3,092
Constante –7,008 1,836 14,570 1 0,000 0,001
B = coefi ciente logístico, Exp(B) = coefi ciente exponenciado
```
```
Variáveis fora da equação
Variáveis independentes Estatística de escore Signifi cância
X 6 Qualidade do produto 4,859 0,028
X 7 Atividades de comércio eletrônico 0,132 0,716
X 8 Suporte técnico 0,007 0,932
X 9 Solução de reclamação 1,379 0,240
X 10 Anúncio 0,129 0,719
X 11 Linha do produto 6,154 0,013
X 12 Imagem da equipe de venda 2,745 0,098
X 14 Garantia e reclamações 0,640 0,424
X 15 Novos produtos 0,344 0,557
X 16 Encomenda e cobrança 2,529 0,112
X 17 Flexibilidade de preço 13,723 0,000
X 18 Velocidade de entrega 1,206 0,272
```
```
Matriz de classifi cação
Pertinência prevista em grupoc
AMOSTRA DE ANÁLISEa AMOSTRA DE TESTEb
X 4 Região X 4 Região
```
```
Pertinência real em grupo
```
```
EUA/América
do Norte
```
```
Fora da Amé-
rica do Norte Total
```
```
EUA/América
do Norte
```
```
Fora da Amé-
rica do Norte Total
EUA/América do Norte 19 7 26 4 9 13
(73,1) (30,8)
Fora da América do Norte 9 25 34 1 26 27
(73,5) (96,3)
a73,3% de amostra de análise corretamente classifi cada.
b75,0% da amostra de teste corretamente classifi cada.
cValores entre parênteses são percentuais corretamente classifi cados (razão de sucesso).
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 295

**Estimação** **_stepwise_** **: Adição da segunda variável,** **_X_** **17.** Es-
pera-se que um ou mais passos no procedimento _stepwise_
resulte na inclusão de todas as variáveis independentes
com estatística de escore signifi cante, bem como sejam
atingidas razões aceitáveis de sucesso (geral e específi cas
de grupos) tanto para a amostra de análise quanto para a
de teste.

```
X 17 , com a maior estatística de escore depois de adicionar
X 13 , foi escolhida para entrada no passo 2 (Tabela 5-27).
Melhoras em todas as medidas de ajuste de modelo varia-
ram de uma queda no valor –2 LL até as várias medidas
R^2. Mais importante sob uma perspectiva de estimação
de modelo, nenhuma das variáveis fora da equação tinha
variações estatisticamente signifi cantes de escores.
```
Assim, o modelo logístico de duas variáveis incluindo
_X_ 13 e _X_ 17 será o modelo fi nal a ser usado para fi ns de ava-
liação de ajuste do mesmo, de precisão preditiva e de in-
terpretação dos coefi cientes.

##### Avaliação do ajuste geral do modelo

Ao se fazer uma avaliação do ajuste geral de um mode-
lo logístico de regressão, podemos empregar três abor-
dagens: medidas estatísticas de ajuste geral do modelo,
medidas pseudo _R_^2 , e precisão de classifi cação expressada
na razão de sucesso. Cada uma dessas abordagens será
examinada para os modelos de regressão logística de uma
variável e de duas variáveis que resultaram do procedi-
mento _stepwise_.

**Medidas estatísticas.** A primeira medida estatística é o
teste qui-quadrado para a variação no valor –2 _LL_ do mo-
delo base, que é comparável com o teste _F_ geral em regres-
são múltipla. Valores menores da medida –2 _LL_ indicam um

```
melhor ajuste de modelo, e o teste estatístico está disponí-
vel para avaliar a diferença entre o modelo base e os demais
modelos propostos (em um procedimento stepwise , este tes-
te está sempre baseado na melhora do passo anterior).
```
- No modelo de uma só variável (ver Tabela 5-26), o va-
    lor –2 _LL_ é reduzido a partir do valor do modelo base de
    82,108 para 59,971*, uma queda de 25,136. Este aumen-
    to em ajuste de modelo foi estatisticamente signifi cante
    no nível 0,000.
- No modelo de duas variáveis, o valor –2 _LL_ diminuiu
    mais para 39,960, resultando em quedas signifi cantes não
    apenas do modelo base (42,148), mas também uma queda
    signifi cante do modelo de uma variável (17,011). Ambas
    as melhoras de ajuste foram signifi cantes no nível 0,000.

```
A segunda medida estatística é a de Hosmer e Le-
meshow de ajuste geral [11]. Este teste estatístico mede a
correspondência dos valores reais e previstos da variável
dependente. Neste caso, um ajuste melhor de modelo é
indicado por uma diferença menor na classifi cação obser-
vada e prevista.
```
```
O teste de Hosmer e Lemeshow mostra signifi cância
para o modelo logístico de uma variável (0,027 da Ta-
bela 5-26), indicando que diferenças signifi cantes ainda
permanecem entre valores reais e esperados. O modelo
de duas variáveis, contudo, reduz o nível de signifi cância
para 0,722 (ver Tabela 5-27), um valor não-signifi cante
que aponta para um ajuste aceitável.
```
```
Para o modelo logístico de duas variáveis, ambas as
medidas estatísticas de ajuste geral do modelo indicam
que o mesmo é aceitável e em um nível estatisticamente
signifi cante. No entanto, é necessário examinar as outras
medidas de ajuste geral do modelo para avaliar se os re-
sultados alcançam os níveis necessários de signifi cância
prática também.
```
```
Medidas de pseudo R^2. Três medidas disponíveis são
comparáveis com a medida R^2 em regressão múltipla: R^2
de Cox e Snell, R^2 de Nagelkerke, e a medida pseudo R^2
baseada na redução no valor –2 LL.
```
```
5-26). Ela corresponde à maior estatística de escore em
todas as 13 variáveis de percepções. A entrada de X 13
no modelo de regressão logística conseguiu um razoável
ajuste, com valores pseudo R^2 variando de 0,306 a 0,459
e as razões de sucesso de 73,3% e 75% para as amostras
de análise e de teste, respectivamente.
O exame dos resultados, porém, identifi ca duas razões
para se considerar um estágio extra para adicionar variá-
veis ao modelo de regressão logística:
```
- Três variáveis não presentes no modelo logístico cor-
    rente ( _X_ 17 , _X_ 11 e _X_ 6 ) têm estatísticas de escore estatis-
    ticamente signifi cantes, indicando que a inclusão das
    mesmas melhoraria consideravelmente o ajuste geral do
    modelo.
- A razão de sucesso geral para a amostra de teste é boa
    (75,0%), mas um dos grupos (Clientes dos EUA/Améri-
    ca do Norte) tem uma razão de sucesso inaceitavelmen-
    te baixa de 30,8%.

```
( Continuação )
```
```
Para o modelo de regressão logística de uma variável,
esses valores eram 0,342, 0,459 e 0,306, respectivamen-
te. Combinados, eles indicam que o modelo de regressão
de uma variável explica aproximadamente um terço da
variação na medida dependente. Apesar de o modelo de
uma variável ser considerado estatisticamente signifi can-
te em diversas medidas de ajuste geral, esses valores de
R^2 são um pouco baixos para fi ns de signifi cância prática.
( Continua )
```
```
* N. de R. T.: O número correto é 56,971.
```

##### 296 Análise Multivariada de Dados

```
TABELA 5-27 Estimação stepwise da regressão logística: adição de X 17 (Flexibilidade de preços)
Ajuste geral do modelo: medidas da qualidade de ajuste
VARIAÇÃO EM –2 LL
Do modelo base Do passo anterior
Valor Variação Signifi cância Variação Signifi cância
–2 Logaritmo de verossimilhança (–2 LL ) 39,960 42,148 0,000 17,011 0,000
R^2 de Cox e Snell 0,505
R^2 de Nagelkerke 0,677
Pseudo R^2 0,513
```
```
Valor Signifi cância
%^2 de Hosmer e Lemeshow 5,326 0,722
```
```
Variáveis na equação
```
```
Variável independente B Erro padrão Wald df Sig. Exp(B)
X 13 Preços competitivos 1,079 0,357 9,115 1 0,003 2,942
X 17 Flexibilidade de preços 1,844 0,639 8,331 1 0,004 6,321
Constante –14,192 3,712 14,614 1 0,000 0,000
B = coefi ciente logístico, Exp(B) = coefi ciente exponenciado
```
```
Variáveis fora da equação
Variáveis independentes Estatística de escore Signifi cância
X 6 Qualidade do produto 0,656 0,418
X 7 Atividades de comércio eletrônico 3,501 0,061
X 8 Suporte técnico 0,006 0,937
X 9 Solução de reclamação 0,693 0,405
X 10 Anúncio 0,091 0,762
X 11 Linha do produto 3,409 0,065
X 12 Imagem da equipe de venda 0,849 0,357
X 14 Garantia e reclamações 2,327 0,127
X 15 Novos produtos 0,026 0,873
X 16 Encomenda e cobrança 0,010 0,919
X 18 Velocidade de entrega 2,907 0,088
```
```
Matriz de classifi cação
Pertinência prevista em grupoc
AMOSTRA DE ANÁLISEa AMOSTRA DE TESTEb
X 4 Região X 4 Região
```
```
Pertinência real em grupo
```
```
EUA/América
do Norte
```
```
Fora da Amé-
rica do Norte Total
```
```
EUA/América
do Norte
```
```
Fora da Amé-
rica do Norte Total
EUA/América do Norte 25 1 26 9 4 13
(96,2) (69,2)
Fora da América do Norte 6 28 34 2 25 27
(82,4) (92,6)
a88,3% de amostra de análise corretamente classifi cada.
b85,0% da amostra de teste corretamente classifi cada.
cValores entre parênteses são percentuais corretamente classifi cados (razão de sucesso).
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 297

Os valores _R_^2 do modelo de duas variáveis exibiram
considerável melhora sobre o modelo de uma variável e
indicam bom ajuste quando comparados aos valores _R_^2
geralmente encontrados em regressão múltipla. De acor-
do com as medidas de ajuste de caráter estatístico, o mo-
delo é considerado aceitável em termos de signifi cância
estatística e prática.

**Precisão de classifi cação.** O terceiro exame de ajuste ge-
ral do modelo será para avaliar a precisão de classifi cação
do modelo em uma medida fi nal de signifi cância prática.
As matrizes de classifi cação, idênticas em natureza àque-
las empregadas em análise discriminante, representam os
níveis de precisão preditiva atingidos pelo modelo logís-
tico. A medida de precisão preditiva usada é a razão de
sucesso, o percentual de casos corretamente classifi cados.
Esses valores serão calculados tanto para a amostra de
análise quanto a de teste, e medidas específi cas de grupos
serão examinadas além das medidas gerais. Além disso,
comparações podem ser feitas, como ocorreu em análise
discriminante, com padrões de comparação representan-
do os níveis de precisão preditiva conseguidos por chan-
ces (ver discussão mais detalhada na seção sobre análise
discriminante).

```
Em todos os três dos tipos básicos de medida de
ajuste geral, o modelo de duas variáveis (com X 13 e X 17 )
demonstra níveis aceitáveis de signifi cância estatística e
prática. Com ajuste de modelo geral aceitável, voltamos
nossa atenção para a avaliação dos testes estatísticos dos
coefi cientes logísticos a fi m de identifi car os coefi cien-
tes que têm relações signifi cantes afetando pertinência
a grupo.
```
##### Signifi cância estatística dos coefi cientes

```
Os coefi cientes estimados para as duas variáveis indepen-
dentes e a constante também podem ser avaliados quanto
à signifi cância estatística. A estatística Wald é usada para
avaliar signifi cância de um modo semelhante ao teste t uti-
lizado em regressão múltipla.
```
```
Os coefi cientes logísticos para X 13 (1,079) e X 17 (1,844) e a
constante (–14,190*) são todos signifi cantes no nível 0,01
com base no teste estatístico de Wald. Nenhuma outra
variável consegue entrar no modelo e atingir pelo menos
um nível de signifi cância de 0,05.
```
```
Assim, as variáveis individuais são signifi cantes e po-
dem ser interpretadas para identifi car as relações que
afetam as probabilidades previstas e subseqüentemente a
pertinência a grupo.
```
##### Diagnósticos por casos

```
A análise da má classifi cação de observações individuais
pode fornecer uma melhor visão sobre possíveis melhora-
mentos do modelo. Diagnósticos por casos, como resídu-
os e medidas de infl uências, estão disponíveis, bem como
a análise de perfi l discutida anteriormente para a análise
discriminante.
```
```
O modelo de duas variáveis (ver Tabela 5-27) tem
valores R^2 que são ambos maiores que 0,50, apontando
para um modelo de regressão logística que explica pelo
menos metade da variação entre os dois grupos de clien-
tes. Sempre se deseja melhorar tais valores, mas tal nível
é considerado praticamente signifi cante nesta situação.
```
```
( Continuação )
```
```
Os padrões de comparação para as razões de sucesso
da matriz de classifi cação serão os mesmos que foram
calculados para a análise discriminante de dois grupos.
Os valores são 65,5% para o critério de chance propor-
cional (a medida preferida) e 76,3% para o critério de
chance máxima. Se você não estiver familiarizado com
os métodos de cálculo de tais medidas, veja a discussão
anterior no capítulo que trata de avaliação da precisão
de classifi cação.
```
- As razões de sucesso geral para o modelo logístico de
    uma variável são 73,3% e 75,0% para as amostras de
    análise e de teste, respectivamente. Mesmo que as ra-
    zões de sucesso geral sejam maiores do que o critério
    de chance proporcional e comparáveis com o critério
    de chance máxima, um problema considerável surge
    na amostra de teste para os clientes dos EUA/América
    do Norte, onde a razão de sucesso é de somente 30,8%.
    Este nível está abaixo de ambos os padrões e demanda
    que o modelo logístico seja expandido até o ponto em
    que, espera-se, esta razão de sucesso específi ca de grupo
    exceda os padrões.
- O modelo de duas variáveis exibe melhora substancial
    na razão de sucesso geral e nos valores específi cos de

```
grupos. As razões de sucesso geral subiram para 88,3%
e 85,0% para as amostras de análise e de teste, respec-
tivamente. Além disso, a problemática razão de suces-
so na amostra de teste aumenta para 69,2%, acima do
valor padrão para o critério de chance proporcional.
Com essas melhoras nos níveis geral e específi cos,
o modelo de regressão logística de duas variáveis é
considerado aceitável em termos de precisão de classi-
fi cação.
```
```
Neste caso, apenas 13 casos foram mal classifi cados (7
na amostra de análise e 6 na de teste). Dado o elevado
grau de correspondência entre esses casos e aqueles mal
classifi cados estudados na análise discriminante de dois
grupos, o processo de estabelecimento de perfi l não será
novamente levado adiante (leitores interessados podem
rever o exemplo de dois grupos). Diagnóstico por casos,
```
```
* N. de R. T.: O número correto é -14,192.
```

##### 298 Análise Multivariada de Dados

#### Estágio 5: Interpretação dos resultados

O procedimento de regressão logística _stepwise_ produziu
uma variável estatística muito semelhante àquela da aná-
lise discriminante de dois grupos, apesar de ter uma variá-
vel independente a menos. Examinaremos os coefi cientes
logísticos para avaliarmos a direção e o impacto que cada
variável tem sobre a probabilidade prevista e a pertinên-
cia a grupo.

##### Interpretação dos coefi cientes logísticos

```
O modelo fi nal de regressão logística inclui duas variá-
veis ( X 13 e X 17 ) com coefi cientes de regressão de 1,079
e 1,844, respectivamente, e uma constante de –14,190*
(ver Tabela 5-27). A comparação desses resultados com
a análise discriminante de dois grupos revela resultados
quase idênticos, uma vez que a análise discriminante in-
cluiu três variáveis no modelo de dois grupos – X 13 e X 17
juntamente com X 11.
```
**Direção das relações.** Para avaliar a direção da relação
de cada variável, podemos examinar ou os coefi cientes
logísticos originais, ou os coefi cientes exponenciados. Co-
mecemos com os originais.

```
Se você recordar de nossa discussão anterior, podemos
interpretar a direção da relação diretamente a partir do
sinal dos coefi cientes logísticos originais. Neste caso, am-
bas as variáveis têm sinais positivos, o que aponta para
uma relação positiva entre ambas as variáveis indepen-
dentes e a probabilidade prevista. À medida que os va-
lores de X 13 ou X 17 aumentam, a probabilidade prevista
aumenta, fazendo crescer assim a possibilidade de que
um cliente seja categorizado como residindo fora da
América do Norte.
Voltando nossa atenção para os coefi cientes expoen-
ciados, devemos recordar que valores acima de 1,0 indi-
cam uma relação positiva e valores abaixo de 1,0 apontam
para uma relação negativa. Em nosso caso, os valores de
2,942 e 6,319 também refl etem relações positivas.
```
**Magnitude das relações.** O método mais direto para
avaliar a magnitude da variação na probabilidade devido
a cada variável independente é examinar os coefi cientes
exponenciados. Como você deve lembrar, o coefi ciente
exponenciado menos um é igual à variação percentual da
razão de desigualdades.

```
Em nosso caso, isso signifi ca que um aumento de um
ponto aumenta a razão de desigualdades em 194% para
X 13 e 531% para X 17. Esses números podem exceder
100% de variação porque eles estão aumentando a razão
de desigualdades e não as probabilidades propriamente
ditas. Os impactos são grandes porque o termo constan-
te (–14,190*) defi ne um ponto inicial de quase zero para
os valores de probabilidade. Logo, grandes aumentos na
razão de desigualdades são necessários para se conseguir
valores maiores de probabilidades.
```
```
Outra abordagem na compreensão sobre como os coefi -
cientes logísticos defi nem probabilidade é calcular a proba-
bilidade prevista para qualquer conjunto de valores para as
variáveis independentes.
```
```
Para as variáveis independentes X 13 e X 17 , usemos as
médias para os dois grupos. Dessa maneira podemos ver
qual seria a probabilidade prevista para um membro mé-
dio de cada grupo.
A Tabela 5-28 mostra os cálculos para a previsão da
probabilidade para os dois centróides de grupo. Como
podemos perceber, o centróide para o grupo 0 (clientes
na América do Norte) tem uma probabilidade prevista
de 18,9%, enquanto o centróide para o grupo 1 (fora da
América do Norte) tem uma probabilidade prevista de
94,8%. Este exemplo demonstra que o modelo logístico
cria de fato uma separação entre os dois centróides de
grupo em termos de probabilidade prevista, gerando ex-
celentes resultados de classifi cação conquistados para as
amostras de análise e de teste.
```
```
Os coefi cientes logísticos defi nem relações positivas
para ambas as variáveis independentes e fornecem uma
maneira de avaliar o impacto de uma variação em uma ou
ambas as variáveis sobre a razão de desigualdades e conse-
qüentemente sobre a probabilidade prevista. Fica evidente
por que muitos pesquisadores preferem regressão logística
à análise discriminante quando comparações são feitas so-
bre a informação mais útil disponível nos coefi cientes logís-
ticos em contrapartida com as cargas discriminantes.
```
#### Estágio 6: Validação dos resultados

```
A validação do modelo de regressão logística é consegui-
da neste exemplo através do mesmo método usado em
análise discriminante: criação de amostras de análises e
de teste. Examinando a razão de sucesso para a amostra
de teste, o pesquisador pode avaliar a validade externa e a
signifi cância prática do modelo de regressão logística.
```
```
como resíduos e medidas de infl uência estão disponí-
veis. Dados os baixos níveis de má classifi cação, porém,
nenhuma análise complementar de classifi cação ruim é
executada.
```
```
Para o modelo fi nal de regressão logística de duas va-
riáveis, as razões de sucesso para as amostras de análi-
( Continua )
* N. de R. T.: O número correto é -14,192.
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 299

Esses resultados levam à conclusão de que o modelo
de regressão logística, como também descoberto com o
modelo de análise discriminante, demonstrou validade
externa sufi ciente para a completa aceitação dos resul-
tados.

#### Uma visão gerencial

A regressão logística apresenta uma alternativa à analise
discriminante que pode ser mais confortável para muitos
pesquisadores devido à sua similaridade com regressão
múltipla. Dada a sua robustez diante das condições de
dados que podem afetar negativamente a análise discri-
minante (p.ex., matrizes diferentes de variância-covariân-
cia), a regressão logística é também a técnica preferida de
estimação em muitas aplicações.

```
Quando comparada com análise discriminante, a re-
gressão logística fornece precisão preditiva compa-
rável com uma variável estatística mais simples que
usava a mesma interpretação substancial, apenas
com uma variável a menos. A partir dos resultados
da regressão logística, o pesquisador pode se concen-
trar na competitividade e na fl exibilidade de preços
como as principais variáveis de diferenciação entre
os dois grupos de clientes. A meta nesta análise não
é aumentar probabilidade (como poderia ser o caso
de se analisar sucesso versus fracasso), ainda que a
regressão logística forneça uma técnica direta para a
HBAT compreender o impacto relativo de cada va-
riável independente na criação de diferenças entre os
dois grupos de clientes.
```
#### Resumo

```
A natureza intrínseca, os conceitos e a abordagem para a
análise discriminante múltipla e a regressão logística fo-
ram apresentadas. Orientações básicas para sua aplicação
e interpretação foram incluídas para melhor esclarecer os
conceitos metodológicos. Este capítulo ajuda você a fazer
o seguinte:
```
```
Estabelecer as circunstâncias sob as quais a análise discri-
minante linear ou a regressão logística devem ser usadas
ao invés da regressão múltipla. Ao se escolher uma téc-
nica analítica apropriada, às vezes encontramos um pro-
blema que envolve uma variável dependente categórica
e diversas variáveis independentes métricas. Lembre-se
que a variável dependente em regressão foi medida me-
tricamente. Análise discriminante múltipla e regressão
logística são as técnicas estatísticas apropriadas quando o
problema de pesquisa envolve uma única variável depen-
dente categórica e diversas variáveis independentes mé-
tricas. Em muitos casos, a variável dependente consiste de
dois grupos ou classifi cações, por exemplo, masculino ver-
sus feminino, alto versus baixo, ou bom versus ruim. Em
outros casos, mais de dois grupos estão envolvidos, como
classifi cações baixas, médias e altas. A análise discrimi-
nante e a regressão logística são capazes de lidar com dois
ou múltiplos (três ou mais) grupos. Os resultados de uma
análise discriminante e de uma regressão logística podem
auxiliar no perfi l das características entre-grupos dos indi-
víduos e na correspondência dos mesmos com seus grupos
adequados.
```
```
Identifi car os principais problemas relacionados aos tipos
de variáveis usados e os tamanhos de amostras exigidos na
aplicação de análise discriminante. Para aplicar análise
discriminante, o pesquisador deve primeiramente especi-
fi car quais variáveis devem ser medidas independentes e
qual é a dependente. O pesquisador deve se concentrar
primeiro na variável dependente. O número de grupos da
variável dependente (categorias) pode ser dois ou mais,
mas tais grupos devem ser mutuamente excludentes e
exaustivos. Depois que uma decisão foi tomada sobre a
variável dependente, o pesquisador deve decidir quais
```
```
TABELA 5-28 Cálculo de valores de probabilidade estimada para os centróides
de grupos da região X 4
X 4 (Região)
Grupo 0: EUA/América
do Norte
```
```
Grupo 1: Fora da
América do Norte
Centróide: X 13 5,60 7,42
Centróide: X 17 3,63 4,93
Valor logit a –1,452 2,909
Razão de desigualdades b 0,234 18,332
Probabilidadec 0,189 0,948
```
a bCalculado como: Logit = $14,190 " 1,079 _X_ 13 " 1,844 _X_ (^17)
cCalculada como: Razão de desigualdades = eLogit
Calculada como: Probabilidade = Razão de desigualdades/(1+Razão de desigualdades)
se e de teste excedem todos os padrões de comparação
(critérios de chance proporcional e de chance máxima).
Além disso, todas as razões de sucesso específi cas de
grupos são sufi cientemente grandes para a aceitação.
Esse aspecto é especialmente importante para a amos-
tra de teste, que é o principal indicador de validade ex-
terna.
( _Continuação_ )


##### 300 Análise Multivariada de Dados

variáveis independentes devem ser incluídas na análise.
Variáveis independentes são escolhidas de duas manei-
ras: (1) identifi cando variáveis de pesquisa anterior ou do
modelo teórico inerente à questão de pesquisa, e (2) uti-
lizando o conhecimento e a intuição do pesquisador para
selecionar variáveis para as quais nenhuma pesquisa ou
teoria anterior existem mas que logicamente podem estar
relacionadas com a previsão de grupos da variável depen-
dente.
A análise discriminante, como as demais técnicas mul-
tivariadas, é afetada pelo tamanho da amostra sob análi-
se. Uma proporção de 20 observações para cada variável
preditora é recomendada. Como os resultados se tornam
instáveis à medida que o tamanho da amostra diminui
relativamente ao número de variáveis independentes, o
tamanho mínimo recomendado é de cinco observações
por variável independente. O tamanho amostral de cada
grupo também deve ser considerado. No mínimo, o ta-
manho do menor grupo de uma categoria deve exceder
o número de variáveis independentes. Como orientação
prática, cada categoria deve ter pelo menos 20 observa-
ções. Mesmo que todas as categorias ultrapassem 20 ob-
servações, porém, o pesquisador também deve considerar
os tamanhos relativos dos grupos. Variações grandes nos
tamanhos dos grupos afetam a estimação da função discri-
minante e a classifi cação de observações.

**Compreender as suposições subjacentes à análise discri-
minante na avaliação de sua adequação a um problema
em particular.** As suposições da análise discriminante se
relacionam aos processos estatísticos envolvidos nos pro-
cedimentos de estimação e classifi cação, bem como aos
problemas que afetam a interpretação dos resultados. As
suposições-chave para se obter a função discriminante são
normalidade multivariada das variáveis independentes, e
estruturas (matrizes) desconhecidas (mas iguais) de dis-
persão e covariância para os grupos como defi nidos pela
variável dependente. Se as suposições são violadas, o pes-
quisador deve entender o impacto sobre os resultados que
podem ser esperados e considerar métodos alternativos
para análise (p.ex., regressão logística).

**Descrever as duas abordagens computacionais para análi-
se discriminante e o método para avaliação de ajuste geral
do modelo.** As duas técnicas para análise discriminante
são os métodos simultâneo (direto) e _stepwise_. A estima-
ção simultânea envolve a computação da função discrimi-
nante considerando todas as variáveis independentes ao
mesmo tempo. Portanto, a função discriminante é com-
putada com base no conjunto inteiro de variáveis inde-
pendentes, independentemente do poder discriminante
de cada variável independente. A estimação _stepwise_ é
uma alternativa ao método simultâneo. Ela envolve a en-
trada de variáveis independentes uma por vez com base
no poder discriminante das mesmas. O método _stepwise_
segue um processo seqüencial de adição ou eliminação de

```
variáveis da função discriminante. Depois que esta é esti-
mada, o pesquisador deve avaliar a signifi cância ou ajuste
da mesma. Quando um método simultâneo é empregado,
o lambda de Wilks, o traço de Hotelling e o critério de
Pillai calculam a signifi cância estatística do poder discri-
minatório da função estimada. Se um método stepwise é
usado para estimar a função discriminante, o D^2 de Maha-
lanobis e a medida V de Rao são os mais adequados para
avaliar ajuste.
```
```
Explicar o que é uma matriz de classifi cação e como de-
senvolver uma, e descrever as maneiras de se avaliar a
precisão preditiva da função discriminante. Os testes
estatísticos para avaliar a signifi cância das funções discri-
minantes avaliam apenas o grau de diferença entre grupos
com base nos escores Z discriminantes, mas não indicam
o quão bem as funções prevêem. Para determinar a habi-
lidade preditiva de uma função discriminante, o pesqui-
sador deve construir matrizes de classifi cação. O procedi-
mento da matriz de classifi cação fornece uma perspectiva
sobre signifi cância prática no lugar de signifi cância esta-
tística. Antes que uma matriz de classifi cação possa ser
construída, no entanto, o pesquisador deve determinar o
escore de corte para cada função discriminante. O escore
de corte representa o ponto de divisão utilizado para clas-
sifi car observações em cada um dos grupos, baseado no
escore da função discriminante. O cálculo de um escore
de corte entre dois grupos quaisquer é sustentado pelos
dois centróides de grupo (média dos escores discriminan-
tes) e pelos tamanhos relativos dos dois grupos. Os resul-
tados do procedimento de classifi cação são apresentados
em forma matricial. As entradas na diagonal da matriz
representam o número de indivíduos corretamente clas-
sifi cados. Os números fora da diagonal correspondem a
classifi cações incorretas. O percentual corretamente clas-
sifi cado, também conhecido como razão de sucesso , revela
o quão bem a função discriminante prevê os objetos. Se os
custos da má classifi cação forem aproximadamente iguais
para todos os grupos, o escore de corte ótimo será aquele
que classifi car mal o menor número de objetos ao longo
de todos os grupos. Se os custos de má classifi cação forem
desiguais, o escore de corte ótimo será aquele que mini-
miza os custos de má classifi cação. Para avaliar a razão de
sucesso, devemos olhar para uma classifi cação por chan-
ces. Quando os tamanhos de grupos são iguais, a determi-
nação da classifi cação por chances se baseia no número de
grupos. Quando os tamanhos dos grupos são distintos, o
cálculo da classifi cação por chances pode ser feito de duas
maneiras: chance máxima e chance proporcional.
```
```
Dizer como identifi car variáveis independentes com po-
der discriminatório. Se a função discriminante é estatis-
ticamente signifi cante e a precisão de classifi cação (razão
de sucesso) é aceitável, o pesquisador deve se concentrar
na realização de interpretações substanciais das descober-
tas. Este processo envolve a determinação da importância
```

##### CAPÍTULO 5 Análise Discriminante Múltipla e Regressão Logística 301

relativa de cada variável independente na discriminação
entre os grupos. Três métodos de determinação da impor-
tância relativa foram propostos: (1) pesos discriminan-
tes padronizados, (2) cargas discriminantes (correlações
estruturais) e (3) valores _F_ parciais. A abordagem tradi-
cional para interpretar funções discriminantes examina
o sinal e a magnitude do peso discriminante padronizado
designado para cada variável na computação das funções
discriminantes. Variáveis independentes com pesos re-
lativamente maiores contribuem mais para o poder dis-
criminatório da função do que variáveis com pesos me-
nores. O sinal denota se a variável contribui negativa ou
positivamente. Cargas discriminantes são cada vez mais
usadas como uma base para interpretação por conta das
defi ciências na utilização de pesos. Medindo a correla-
ção linear simples entre cada variável independente e a
função discriminante, as cargas discriminantes refl etem a
variância que as variáveis independentes compartilham
com a função discriminante. Elas podem ser interpretadas
como cargas fatoriais na avaliação da contribuição relati-
va de cada variável independente à função discriminante.
Quando um método de estimação _stepwise_ é usado, uma
maneira adicional de interpretar o poder discriminatório
relativo das variáveis independentes é através do empre-
go de valores _F_ parciais, o que se consegue examinando-se
os tamanhos absolutos dos valores _F_ signifi cantes e orde-
nando-os. Valores _F_ grandes indicam um poder discrimi-
natório maior.

**Justifi car o uso de um método de divisão de amostra para
validação.** O estágio fi nal de uma análise discriminante
envolve a validação dos resultados discriminantes para
fornecer garantias de que os mesmos têm tanto validade
interna quanto externa. Além de validar as razões de su-
cesso, o pesquisador deve usar o perfi l dos grupos para
garantir que as médias deles são indicadores válidos do
modelo conceitual utilizado na seleção das variáveis in-
dependentes. Validação pode ocorrer com uma amostra
separada (de teste) ou utilizando um procedimento que
repetidamente processa a amostra de estimação. Valida-
ção das razões de sucesso é executada muito freqüente-
mente criando-se uma amostra de teste, também chama-
da de amostra de validação. O propósito da utilização de
uma amostra de teste para fi ns de validação é perceber o
quão bem a função discriminante funciona em uma amos-
tra de observações que não foram usadas para obtê-la. Tal
avaliação envolve o desenvolvimento de uma função dis-
criminante com a amostra de análise e então a aplicação
da função à amostra de teste.

**Entender as vantagens e desvantagens da regressão lo-
gística comparada com análise discriminante e regressão
múltipla.** Análise discriminante é apropriada quando a
variável dependente é não-métrica. Se ela tiver apenas
dois grupos, então a regressão logística pode ser prefe-
rível por duas razões. Primeiro, a análise discriminante

```
apóia-se no atendimento estrito das suposições de nor-
malidade multivariada e igualdade entre as matrizes de
variância-covariância nos grupos – premissas que não são
atendidas em muitas situações. A regressão logística não
se depara com tais restrições e é muito mais robusta quan-
do essas suposições não são atendidas, tornando sua apli-
cação adequada em muitos casos. Segundo, mesmo que
as suposições sejam atendidas, muitos pesquisadores pre-
ferem a regressão logística por ser semelhante à regres-
são múltipla. Como tal, ela tem testes estatísticos diretos,
métodos semelhantes para incorporar variáveis métricas e
não-métricas e efeitos não-lineares, bem como uma vasta
gama de diagnósticos. A regressão logística é equivalen-
te à análise discriminante de dois grupos e pode ser mais
adequada em muitas situações.
```
```
Interpretar os resultados de uma análise de regressão lo-
gística, com comparações com regressão múltipla e análise
discriminante. A adequação de ajuste para um modelo
de regressão logística pode ser avaliada de duas maneiras:
(1) usando valores pseudo R^2 , semelhantes àqueles en-
contrados em regressão múltipla, e (2) examinando pre-
cisão preditiva (i.e., a matriz de classifi cação em análise
discriminante). As duas abordagens examinam ajuste de
modelo sob diferentes perspectivas, mas devem conduzir
a resultados semelhantes. Uma das vantagens da regres-
são logística é que precisamos saber apenas se um evento
ocorreu para defi nir um valor dicotômico como nossa va-
riável dependente. Quando analisamos esses dados usan-
do transformação logística, contudo, a regressão logísti-
ca e seus coefi cientes assumem um signifi cado um tanto
diferente daqueles encontrados em regressão com uma
variável dependente métrica. Analogamente, cargas em
análise discriminante são interpretadas diferentemente
de um coefi ciente logístico. Este último refl ete a direção
e a magnitude da relação da variável independente, mas
requer diferentes métodos de interpretação. A direção
da relação (positiva ou negativa) retrata as variações na
variável dependente associadas com mudanças na inde-
pendente. Uma relação positiva signifi ca que um aumento
na variável independente é associado com um aumento
na probabilidade prevista, e vice-versa para uma relação
negativa.Para determinar a magnitude do coefi ciente, ou
o quanto que a probabilidade mudará dada uma unidade
de variação na variável independente, o valor numérico
do coefi ciente deve ser avaliado. Exatamente como em
regressão múltipla, os coefi cientes para variáveis métricas
e não-métricas devem ser interpretados diferentemente
porque cada um refl ete diferentes impactos sobre a variá-
vel dependente.
A análise discriminante múltipla e a regressão logís-
tica ajudam a compreender e explicar problemas de pes-
quisa que envolvem uma variável dependente categórica
e diversas variáveis independentes métricas. Ambas as
técnicas podem ser usadas para estabelecer o perfi l das
```

##### 302 Análise Multivariada de Dados

características entre grupos dos indivíduos e designar os
mesmos a seus grupos apropriados. Aplicações potenciais
dessas duas técnicas tanto em negócios como em outras
áreas são inúmeras.

#### Questões

1. Como você diferenciaria entre análise discriminante múl-
    tipla, análise de regressão, regressão logística e análise de
    variância?
2. Quando você empregaria regressão logística no lugar de
    análise discriminante? Quais são as vantagens e desvanta-
    gens dessa decisão?
3. Quais critérios você poderia usar para decidir se deve parar
    uma análise discriminante depois de estimar a função discri-
    minante? Depois do estágio de interpretação?
4. Qual procedimento você seguiria para dividir sua amostra
    em grupos de análise e de teste? Como você mudaria este
    procedimento se sua amostra consistisse de menos do que
    100 indivíduos ou objetos?
5. Como você determinaria o escore de corte ótimo?
6. Como você determinaria se a precisão de classifi cação da
    função discriminante é sufi cientemente alta relativamente a
    uma classifi cação ao acaso?
7. Como uma análise discriminante de dois grupos difere de
    uma análise de três grupos?
8. Por que um pesquisador deve expandir as cargas e dados
    do centróide ao representar grafi camente uma solução de
    análise discriminante?
9. Como a regressão logística e a análise discriminante lidam
    com a relação das variáveis dependente e independentes?
1 0. Q u a i s s ã o a s d i f e r e n ç a s d e e s t i m a ç ã o e i n t e r p r e t a ç ã o e n t r e
    regressão logística e análise discriminante?
1 1. E x p l i q u e o c o n c e i t o d e r a z ã o d e d e s i g u a l d a d e s e p o r q u e e l a
    é usada para prever probabilidade em um procedimento de
    regressão logística.

#### Leituras sugeridas

Uma lista de leituras sugeridas ilustrando questões e apli-
cações da análise discriminante e regressão logística está
disponível na Web em [http://www.prenhall.com/hair](http://www.prenhall.com/hair) (em inglês).

#### Referências

1. Cohen, J. 1988. _Statistical Power Analysis for the_
    _Behavioral Sciences,_ 2nd ed. Hillsdale, NJ: Lawrence
    Erlbaum Associates.
       2. Crask, M., and W. Perreault. 1977. Validation of
          Discriminant Analysis in Marketing Research. _Journal of_
          _Marketing Research_ 14 (February): 60–68.
       3. Demaris, A. 1995. A Tutorial in Logistic Regression.
          _Journal of Marriage and the Family_ 57: 956–68.
       4. Dillon, W. R., and M. Goldstein. 1984. _Multivariate_
          _Analysis: Methods and Applications._ New York: Wiley.
       5. Frank, R. E., W. E. Massey, and D. G. Morrison. 1965.
          Bias in Multiple Discriminant Analysis. _Journal of_
          _Marketing Research_ 2(3): 250–58.
       6. Gessner, Guy, N. K. Maholtra, W. A. Kamakura, and
          M. E. Zmijewski. 1988. Estimating Models with Binary
          Dependent Variables: Some Theoretical and Empirical
          Observations. _Journal of Business Research_ 16(1): 49–65.
       7. Green, P. E., D. Tull, and G. Albaum. 1988. _Research for_
          _Marketing Decisions._ Upper Saddle River, NJ: Prentice
          Hall.
       8. Green, P. E. 1978. _Analyzing Multivariate Data._ Hinsdale,
          IL: Holt, Rinehart and Winston.
       9. Green, P. E., and J. D. Carroll. 1978. _Mathematical Tools_
          _for Applied Multivariate Analysis._ New York: Academic
          Press.
       1 0. H a r r i s , R. J. 2 0 0 1. _A Primer of Multivariate Statistics,_ 3rd
          ed. Hillsdale, NJ: Lawrence Erlbaum Associates.
       11. Hosmer, D. W., and S. Lemeshow. 2000. _Applied Logistic_
          _Regression,_ 2nd ed. New York: Wiley.
       12. Huberty, C. J. 1984. Issues in the Use and Interpretation
          of Discriminant Analysis. _Psychological Bulletin_ 95: 156–
          71.
       13. Huberty, C. J., J. W. Wisenbaker, and J. C. Smith. 1987.
          Assessing Predictive Accuracy in Discriminant Analysis.
          _Multivariate Behavioral Research_ 22 (July): 307–29.
       14. Johnson, N., and D. Wichern. 2002. _Applied Multivariate_
          _Statistical Analysis,_ 5th ed. Upper Saddle River, NJ:
          Prentice Hall.
       1 5. L o n g , J. S. 1 9 9 7. _Regression Models for Categorical_
          _and-Limited Dependent Variables: Analysis and_
          _Interpretation._ Thousand Oaks, CA:-Sage.
       16. Morrison, D. G. 1969. On the Interpretation of
          Discriminant Analysis. _Journal of Marketing Research_
          6(2): 156–63.
       17. Pampel, F. C. 2000. _Logistic Regression: A Primer,_ Sage
          University Papers Series on Quantitative Applications in
          the Social Sciences, # 07–096. Newbury Park, CA: Sage.
       18. Perreault, W. D., D. N. Behrman, and G. M. Armstrong.
          1979. Alternative Approaches for Interpretation of Multiple
          Discriminant Analysis in Marketing Research. _Journal of_
          _Business Research_ 7: 151–73.


