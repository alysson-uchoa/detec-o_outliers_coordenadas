Este projeto tem como objetivo identificar e corrigir inconsistências em coordenadas geográficas (latitude e longitude) utilizando uma abordagem baseada na análise de consistência entre pares de pontos. Em bases de dados com geolocalização, é comum encontrar erros como coordenadas em cidades incorretas, registros em outros estados ou até em outros países. Métodos estatísticos tradicionais, como média e desvio padrão, podem não funcionar adequadamente nesses casos, pois a presença de outliers extremos distorce os cálculos e compromete a identificação correta dos dados inconsistentes.

Para resolver esse problema, foi adotada uma abordagem alternativa baseada na comparação direta entre os pontos de uma mesma cidade. O algoritmo gera todas as combinações possíveis de pares de clientes e calcula o desvio entre eles, utilizando a distância entre as coordenadas. A partir disso, identifica quais pares apresentam comportamento consistente, ou seja, possuem baixo desvio. Em seguida, identifica quais pontos participam desses pares consistentes, formando o grupo válido. Os pontos que não participam de nenhum desses pares são considerados outliers, pois não apresentam coerência com o restante do grupo. Esses outliers são corrigidos substituindo suas coordenadas pela média dos pontos válidos, garantindo uma correção precisa e sem distorções.

Para ilustrar, considere uma cidade com três clientes: A com coordenadas (-8.0476, -34.8770), B com coordenadas (-8.1200, -34.9500) e C com coordenadas (51.5074, -0.1278). Ao comparar os pares, temos que A e B possuem um desvio muito baixo, indicando que estão próximos e pertencem à mesma região. Já os pares envolvendo C apresentam desvios muito altos, indicando que C está completamente fora do padrão da cidade, já que essas coordenadas correspondem a outro país. Como C não forma nenhum par consistente com os demais, ele é identificado como outlier. A correção então é feita substituindo suas coordenadas pela média de A e B, resultando em um valor aproximado de (-8.0838, -34.9135), que representa corretamente a localização daquela cidade.

A principal vantagem dessa abordagem é que ela não depende de uma média global, que pode ser facilmente distorcida por valores extremos. Em vez disso, o método analisa a consistência entre os dados, tornando-se robusto tanto para pequenos conjuntos quanto para volumes maiores. Além disso, evita falsos positivos, pois mantém pontos válidos mesmo que estejam mais afastados dentro da cidade, desde que ainda apresentem consistência com o grupo. O principal insight desse projeto é que um outlier não é necessariamente o ponto mais distante da média, mas sim aquele que não apresenta conexão ou consistência com os demais dados.

Etapas do algoritmo

1. Gerar todas as combinações de pares dentro de cada cidade 
2. Calcular o desvio entre cada par (distância entre coordenadas) 
3. Identificar pares consistentes (com baixo desvio) 
4. Determinar os pontos que participam desses pares 
5. Classificar como outliers os pontos que não se conectam com o grupo 
6. Corrigir os outliers utilizando a média dos pontos consistentes  

Tecnologias utilizadas

- Python 
- Pandas 
- NumPy 
- itertools  
