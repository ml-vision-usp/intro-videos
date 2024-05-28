# Aula 1 - Regressão Linear

## Introdução

### O que é regressão?

- Exemplo
    - Imagine que queremos prever o preço de um produto em determinado dia do ano - arroz, por exemplo - e temos documentados os preços do arroz em todos os dias dos últimos 10 anos. Esses dados estão no formato (dia do ano, preço), ou seja: (1, 4.25), (1, 4.87), (67, 3.40), ...
    ***Seria interessante colocar aqui uma imagem aqui que mostrasse dados assim e eles seguissem um formato que fosse bem aproximado por uma reta, Fernando. - Kaique***
    - Note como uma aparente boa aproximação seria uma reta mais ou menos parecida com essa aqui ***desenha na tela a reta sobre o gráfico***. A ideia da regressão linear é justamente encontrar essa reta, uma reta que aproxime bem nossos dados.
- Conceito
    - Regressão é uma técnica matemática a qual utiliza de determinados métodos para prever valores contínuos baseada nas relações entre diferentes variáveis. O objetivo da regressãso é treinar diferentes algoritmos para encontrarem padrões nos dados de modo que consigamos prever novos dados que ainda não vimos. 

## Desenvolvimento
- Função de erro
    - Para começar nossa busca pela melhor reta primeiro precisamos saber definir o que é uma boa reta. Olhando para a reta desenhada no gráfico, parece óbvio que ela é uma reta melhor que essa, por exemplo ***desenha reta ruim no gráfico***. Bom, imagine que nossa reta possui formato $f(x) = ax+b$, e nossos pontos são $(x_1, y_1), (x_2, y_2)$ e assim por diante. Em primeiro momento podemos pensar em apenas somar os erros que nossa reta possui, isso é:

    $$
        Erro = \sum_{i=1}^{N} (f(x_i) - y_i)
    $$

    Mas, imagina que temos dois pontos (0, 2) e (0, -2), e nossa reta prevê f(0) = 0, observe que, pra nossa função de erro, nossa reta teria erro:

    $$
        Erro = (0 - 2) + (0 + 2) = 0 
    $$

    Ou seja, apesar da nossa reta ter dois erros claros, nossa função de erro diz que a reta possui erro igual a zero, o que não é o que queremos. Para solucionar esse problema, além de facilitar outros cálculos, podemos pegar nossa função antiga e adicionar um quadrado nos termos do somatório:

    $$
    Erro = \sum_{i=1}^{N} (f(x_i) - y_i)^2
    $$

    Assim a situação melhora, nosso erro aumenta sempre que nossa função erra a previsão de algum ponto. Todavia, note que, quanto mais pontos temos, mais tende a subir a nossa função de erro. Às vezes isso não é bom, visto que uma reta aprendida com muitos pontos pode ter um erro maior e ser melhor do que uma reta aprendida com poucos pontos e com um erro menor.

    Dessa forma, para equilibrar melhor a situação, vamos tomar a média do erros como função de erro:

    $$
        Erro = \frac{1}{N}\sum_{i=0}^{N} (f(x_i) - y_i)^2
    $$

Tudo bem, agora temos uma forma de comparar retas. Entre todas as retas que existem, nós queremos aquela que minimiza essa função de custo. Mas, como vamos achar essa reta?

Bem, existem diferentes forma de se encontrar essa reta, nessa aula aprenderemos duas: a forma analítica e a forma iterativa. A forma iterativa acaba sendo mais útil na introdução aos estudos de Aprendizado de Máquina, por isso vamos começar por ela. 

### Forma iterativa (Gradiente Descendente)

Sabemos que o vetor gradiente de uma função aponta para a direção de maior crescimento daquela função. Ou seja, dada uma função assim ... **desenha parábola e marca um ponto**... o vetor gradiente desse ponto seria algo mais ou menos assim ... **desenha uma seta que aproxima o vetor gradiente**. Ou seja, para minimizar nossa função de erro, podemos seguir a direção contrária ao vetor gradiente. Existem alguns detalhes nesse processo, mas antes de chegar neles, primeiro vamos encontrar o vetor gradiente.

Digamos que nossa reta possui configuração $f(x) = ax + b$. Portanto, nossa função de erro possui como parâmetros as variáveis a e b. Desse modo, para encontrar o vetor gradiente, precisamos calcular as derivadas parciais da função de erro em $a$ e em $b$. Vamos começar calculando a derivada parcial em $a$:

$$
    \frac{\partial Erro}{\partial a} = \frac{\partial}{\partial a} [\frac{1}{N}\sum_{i=0}^{N} (f(x_i) - y_i)^2]
$$

$$
    \frac{\partial Erro}{\partial a} = \frac{1}{N} \frac{\partial}{\partial a}[\sum_{i=0}^{N} (f(x_i) - y_i)^2]
$$

$$
    \frac{\partial Erro}{\partial a} = \frac{1}{N}\sum_{i=0}^{N} \frac{\partial}{\partial a}[(f(x_i) - y_i)^2]
$$

$$
    \frac{\partial Erro}{\partial a} = \frac{1}{N}\sum_{i=0}^{N} 2(f(x_i) - y_i)\frac{\partial}{\partial a}[(f(x_i) - y_i)]
$$

$$
    \frac{\partial Erro}{\partial a} = \frac{1}{N}\sum_{i=0}^{N} 2(f(x_i) - y_i)\frac{\partial}{\partial a}[f(x_i)]
$$

$$
    \frac{\partial Erro}{\partial a} = \frac{1}{N}\sum_{i=0}^{N} 2(f(x_i) - y_i)\frac{\partial}{\partial a}[ax_i + b]
$$

$$
    \frac{\partial Erro}{\partial a} = \frac{2}{N}\sum_{i=0}^{N} x_i(f(x_i) - y_i)
$$

Agora para encontrar a derivada parcial em b, basta seguir os mesmos passos, com os dois últimos passos sendo:

$$
    \frac{\partial Erro}{\partial b} = \frac{1}{N}\sum_{i=0}^{N} 2(f(x_i) - y_i)\frac{\partial}{\partial b}[ax_i + b]
$$

$$
    \frac{\partial Erro}{\partial b} = \frac{2}{N}\sum_{i=0}^{N} (f(x_i) - y_i)
$$

Desse modo, agora com as derivadas parciais, conseguimos encontrar o vetor gradiente. Agora, para seguir o caminho contrário do gradiente, basta atualizármos os parâmetros a e b da seguinte forma:

$
    a = a - \alpha \frac{\partial Erro}{\partial a}
$

$
    b = b - \alpha \frac{\partial Erro}{\partial b}
$

Sendo o alfa um valor real positivo, chamado de *learning rate*.

Após um determinado número de iterações, e dependendo do nosso learning rate, chegaremos cada vez mais perto dos valores $a$ e $b$ onde nossa função de erro é mínima.

Esse algoritmo se chama gradiente descendente, e vai ser muito importante em outros tópicos da área de aprendizado de máquina. Existem detalhes nele que podem ser refinados, mas que ficarão para outra aula.

### Forma analítica

**Vale a pena falar sobre?**

## Conclusão
- O que é machine learning?
- Apresentar o LEARN e o nosso projeto
- Apresentar as pessoas envolvidas na produção dessa aula
- Mencionar o link para o material escrito e as referências
