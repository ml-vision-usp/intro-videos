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

    Assim a situação melhora, nosso erro aumenta sempre que nossa função erra a previsão de algum ponto. Todavia, note que 

    $$
        Erro = \frac{1}{N}\sum_{i=0}^{N} (f(x_i) - y_i)^2
    $$


  
## Conclusão
- O que é machine learning?
- Apresentar o LEARN e o nosso projeto
- Apresentar as pessoas envolvidas na produção dessa aula
- Mencionar o link para o material escrito e as referências
