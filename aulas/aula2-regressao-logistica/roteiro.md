# Aula 2 - Regressão Logística

## Introdução

### O que é regressão logística
- Exemplo:
    - Imagine que você é um banco e um novo possível cliente está com a intenção de pedir um empréstimo em seu sistema. Ele tenta e nesse momento o seu sistema recolhe diferentes informações sobre ele, como renda familiar, histórico de dívidas, escolaridade, e etc. O seu objetivo então é analisar os dados vindos desse possível cliente e analisar se é boa ideia fornecer o dinheiro, ou seja: qual a probabilidade do seu cliente quitar a dívida, isso é, pagar o empréstimo?

A ideia por trás da regressão logística é exatamente essa: inferir a probabilidade de um determinado rótulo dado um conjunto de entrada de dados. No nosso caso, inferir a probabilidade de um determinado cliente pagar ou não pagar.

## Desenvolvimento

Bom, como percebemos, queremos aprender uma distribuição de probabilidade. No caso, queremos aprender $P(y = y_i | \bold{x} = \bold{x}_i)$, isso é: queremos aprender a probabilidade de uma determinada entrada $\bold{x} = \bold{x}_i$ ter como rótulo $y = y_i$. No nosso caso, poderíamos dizer que nosso vetor $\bold{x}$ possui as informações financeiras do cliente, enquanto $y$ pode ser 0, quando o cliente é um mau pagador, e 1 quando o cliente é um bom pagador.

Mas como vamos aprender isso? Bem, nós temos acesso a alguns dados. No caso, temos acesso ao nosso histórico de pagamentos de empréstimos, isso é: para cada cliente que tivemos nos últimos anos, guardamos os seus pares $(\bold{x}_i, y_i)$. Ou seja, guardamos as informações financeiras de cada cliente e se eles honraram suas dívidas ou não. E é com esses dados que vamos estimar a distribuição de probabilidade.

## Caso $y \in \{0,1\}$

Vamos aprender na aula de hoje o caso binário da regressão logística, ou seja: o rótulo $y$ de cada dado no conjunto de aprendizado deve ter apenas um de dois valores possíveis. Por exemplo: zero ou um. 

Nesse caso, podemos escrever:

$$
    P(y = y_i | \bold{x} = \bold{x}_i) = P(y = 1 | \bold{x}_i)^{y_i} P(y = 0 | \bold{x} = \bold{x}_i)^{1-y_i}
$$

$$
    P(y = y_i | \bold{x} = \bold{x}_i) = P(y = 1 | \bold{x}_i)^{y_i} [1 - P(y = 0 | \bold{x} = \bold{x}_i)]^{1-y_i}
$$

Imaginando agora que cada ponto foi gerado de modo independente, a probabilidade de que nós encontremos o conjunto de pares $(\bold{x}_1, y_1), (\bold{x}_2, y_2), ..., (\bold{x}_N, y_N)$ pode ser escrita como o produtório (verossimilhança):

$$
    \prod_{i=1}^{N}P(y = y_i | \bold{x} = \bold{x}_i) = \prod_{i = 1}^{N} P(y = 1 | \bold{x}_i)^{y_i} [1 - P(y = 1 | \bold{x} = \bold{x}_i)]^{1-y_i}
$$

Imaginando que nós temos uma forma de estimar essas probabilidades, nós queremos que essa nossa estimativa maximize a verossimilhança. Ou seja, é como se nós quisessemos estimar as probabilidades de modo que nossa estimativa maximize as chances de encontrar os resultados que nós vimos no nosso conjunto de aprendizado. Mas como podemos estimar $P(y = 1 | \bold{x} = \bold{x}_i$)?

- Conhecendo a sigmoide

    Existe uma família de funções que podem ser usadas para estimar probabilidades, com uma das mais conhecidas sendo a função sigmoide $\theta(s) = \frac{1}{1-e^{-s}}$:

    **imagem do gráfico da função sigmoide aqui**

    Existem algumas coisas muito interessantes sobre essa função e que nos permitem utilizá-la. Para começar, podemos ver no gráfico dessa função que seus valores estão restritos a zero e um, que é o que encontramos nas distribuição de probabilidade. Além disso, a sigmoide é diferenciável em todos os seus pontos, o que será importante mais pra frente. E, por fim, temos que $\theta(-s) = 1 - \theta(s)$, o que será útil mais pra frente.

Assim sendo, podemos escrever a estimativa da nossa verossimilhança como sendo:

$$
    \prod_{i = 1}^{N} P(y = 1 | \bold{x}_i)^{y_i} [1 - P(y = 0 | \bold{x} = \bold{x}_i)^{1-y_i}] 
    \approx
    \prod_{i = 1}^{N} \theta(s_i)^{y_i} [1 - \theta(s_i)]^{1-y_i} 
$$

Mas como definir esse $s_i$? Bom, na regressão logística nós definimos $s_i = \bold{w}^{T}\bold{x}$, com $\bold{w}$ sendo nosso vetor coluna de pesos, que é o que de fato vamos aprender, e $\bold{x}$ sendo o nosso vetor coluna de features (ou características). **talvez desenhar um exemplinho dos vetores?**

Dessa forma, nossa estimativa de verossimilhança fica:

$$
    \prod_{i = 1}^{N} \theta(\bold{w}^{T}\bold{x}_i)^{y_i} [1 - \theta(\bold{w}^{T}\bold{x}_i)]^{1-y_i}
$$

Ou seja, queremos encontrar $\bold{w}$ que maximize essa expressão. 

Maximizar coisas não é muito comum em aprendizado de máquina, geralmente gostamos de minimizar coisas, especilmente erros. Então, vamos transformar nosso problema em uma função de custo que queremos minimizar. Para começar, ... **Fernando, coloca o passo a passo pra chegar na função de custo, pf. Minha fonte principal aqui tá sendo as notas da Nina**

Por fim, chegamos na função de custo:

$$
    Custo(\bold{w}) = -\frac{1}{N}\sum_{i=1}^{N}y_{i}\ln(\theta(\bold{w}^{T}\bold{x}_i)) + (1 - y_i)\ln(1 - \theta(\bold{w}^{T}\bold{x}_i))
$$

Se escrevermos $\theta(\bold{w}^{T}\bold{x}_i) = \hat{y}$, então nossa função assume um formato mais comum:

$$
    Custo(\bold{w}) = -\frac{1}{N}\sum_{i=1}^{N}y_{i}\ln(\hat{y}_i) + (1 - y_i)\ln(1 - \hat{y}_i)
$$

Chamamos essa função de Entropia Cruzada.
## Conclusão
- Apresentar o LEARN e o nosso projeto
- Apresentar as pessoas envolvidas na produção dessa aula
- Mencionar o link para o material escrito e as referências