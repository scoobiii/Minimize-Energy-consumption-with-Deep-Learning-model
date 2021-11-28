# Minimize o consumidor de energia com o modelo DeepLearning
Use o modelo Deep Q-Learning para otimizar o consumo de energia de um data center e sistemas de Refrigeração

Este projeto utiliza um modelo de aprendizado profundo de IA para otimizar e reduzir o consumo de energia de um data center em até 70%.
O modelo AI usa o algoritmo Q-Learning para determinar a melhor ação em cada etapa de tempo.
O Q-Learning é baseado nas equações de Bellman que estão na raiz do Reinforcement Learning.

# Descrição
O projeto visa reduzir o consumo de energia de uma instalação industrial. Um modelo de otimização de aprendizado profundo é usado e comparado com o sistema de resfriamento integrado tradicional. A abordagem é inspirada na redução de 40% alcançada nos data centers do Google usando o modelo DeepMind AI. O projeto faz parte do módulo de Inteligência Artificial para Negócios da Udemy.

Neste cenário, existem duas premissas principais:
- A temperatura intrínseca de um servidor é função da temperatura atmosférica, do número de usuários no servidor e da taxa de transmissão de dados. A relação é aproximada por uma combinação linear dessas 3 variáveis. Os coeficientes são estimados usando análise de regressão.
- A energia gasta para regular a temperatura entre duas etapas de tempo é proporcional à mudança absoluta de temperatura. Usando essa relação linear, podemos estimar o consumo de energia de cada mecanismo para ser proporcional à mudança absoluta de temperatura do servidor. Isso se aplica tanto ao sistema AI quanto ao sistema de resfriamento integrado tradicional.

# Q-Learning
Q-Learning é um algoritmo de aprendizado por reforço para aprender a qualidade das ações, dizendo a um agente que ação tomar em quais circunstâncias. Ele determina o valor de todas as ações possíveis em um determinado estado (ou circunstâncias). Não requer um modelo do ambiente, pois aprende o ambiente ao explorá-lo. Os valores das ações (ou Qualidade das ações) são determinados recursivamente à medida que o algoritmo explora o ambiente e aprende com os resultados obtidos em um grande número de iterações. O Q-learning encontra uma política ótima (sequência de ações) maximizando o valor esperado da recompensa total em todas e quaisquer etapas sucessivas, a partir do estado atual. Em outras palavras, o Q-learning pode identificar uma política de seleção de ação ótima para qualquer processo de decisão Markov finito (não depende do passado, mas apenas das ações futuras), dado o tempo de exploração infinito e uma política parcialmente aleatória.

Lembrete (Wikipedia): A aprendizagem por reforço envolve um agente, um conjunto de estados S e um conjunto A de ações por estado. Ao executar uma ação a em A, o agente faz a transição de um estado para outro. Executar uma ação em um estado específico fornece ao agente uma recompensa (uma pontuação numérica). O objetivo do agente é maximizar sua recompensa total. Ele faz isso adicionando a recompensa máxima atingível em estados futuros à recompensa por atingir seu estado atual, influenciando efetivamente a ação atual pela recompensa futura em potencial. Essa recompensa potencial é uma soma ponderada dos valores esperados das recompensas de todas as etapas futuras a partir do estado atual.

Portanto, a equação de Bellman decompõe o valor em duas partes, a recompensa imediata mais os valores futuros descontados. A equação de Bellman aparece em toda a literatura de Aprendizado por Reforço, sendo um dos elementos centrais de muitos algoritmos de Aprendizado por Reforço.

Neste projeto, a recompensa é definida como a diferença absoluta entre a energia exigida pelo sistema de refrigeração e a energia exigida pelo modelo de IA. Esta é a energia economizada pela IA.

# Modelo de aprendizado profundo

O projeto usa uma rede neural simples composta por 3 camadas totalmente conectadas.
A rede recebe como entrada um vetor normalizado que representa o estado. Neste problema, o estado é representado pela temperatura do servidor, o número de usuários e a taxa de transmissão de dados. O estado é atualizado a cada etapa de tempo.

As 2 camadas ocultas têm 64 e 32 nós, respectivamente.

A camada de saída prevê os valores Q para 5 ações potenciais cobrindo as opções disponíveis para o sistema. Uma função de ativação softmax gera uma distribuição de probabilidade sobre as ações. A probabilidade mais alta corresponde ao valor Q mais alto.

A fase de aprendizagem usa a técnica "Experience Replay" para treinar.

<img src="Brain_Slide.png" width="100" height="100" />

# Resultados

A porcentagem de energia economizada varia de acordo com os experimentos. A porcentagem é determinada simulando um ciclo anual completo. A amostra abaixo atingiu 68% do consumo de energia graças ao AI em comparação com o sistema de resfriamento integrado usual. Ambos os modelos visam manter o servidor dentro de uma faixa de temperatura ideal de 18 ° a 24 ° C. A simulação é realizada em intervalos de tempo de um minuto ao longo de um ano inteiro.

<img src="savings.png" width="100" height="100" />

# Os recursos da rede neural são listados a seguir:

Datacenter 

1. Carga total de TI do servidor [kW]
2. Carga de TI total da sala de rede principal do campus (CCNR) [kW]
3. Número total de bombas de água de processo (PWP) em execução
4. Velocidade média do conversor de frequência variável (VFD) [%]
5. Número total de bombas de água do condensador (CWP) funcionando
6. Velocidade média do conversor de frequência variável (VFD) [%]
7. Número total de torres de resfriamento funcionando
8. Ponto de ajuste médio da temperatura de saída da água da torre de resfriamento (LWT) [F]
9. Número total de chillers funcionando
10. Número total de drycoolers funcionando
11. Número total de bombas de injeção de água gelada funcionando
12. Temperatura média do ponto de ajuste da bomba de injeção de água gelada [F]
13. Temperatura média de aproximação do trocador de calor [F]
14. Temperatura do bulbo úmido do ar externo (WB) [F]
15. Temperatura do bulbo seco do ar externo (DB) [F]
16. Entalpia de ar externo [kJ / kg]
17. Umidade relativa do ar externo (UR) [%]
18. Velocidade do vento externo [mph]
19. Direção do vento externo [deg]

Camaras Frias/Ultra Congeladores (em desenvolvimento)

1. Carga total de mercadoria [kW]
2. Carga de mercadoria total por camara fria (CMT) [kW]
3. Número total de ventiladores de evaporadores (VET) em execução
4. Velocidade média do conversor de frequência variável por compressor/câmara (VFD) [%]
5. Número total de ventiladores do condensador (CWP) funcionando
6. Velocidade média do conversor de frequência variável por compressor (VFC) [%]
7. Velocidade média do conversor de frequência variável por ventilador do condensador (VFCD)
8. Velocidade média do conversor de frequência variável por ventilador do evaporador (VFE)
9. Número total de condesadores em funcionando
10. Ponto de ajuste médio da temperatura de saída do ar dos condensadores (TSC)
11. Número total de maquinas funcionando
12. Número total de condensadores funcionando
13. Número total de ventiladores de evaporador funcionando
14. Temperatura média do ponto de ajuste de temperatura das camaras
15. Temperatura média de aproximação do trocador de calor
16. Temperatura do bulbo úmido do ar externo (TBU) 
17. Temperatura do bulbo seco do ar externo (TBS)
18. Entalpia de ar externo [kJ / kg]
19. Umidade relativa do ar externo (URE) [%]
20. Umidade relativa do ar externo (URI) [%]
21. Indice de CO2 por câmara (PPMI)
22. Indice de CO2 externo(PPME)
23. Indice de O2 externo(PPME)
24.  Indice de O2 interno(PPMI)
25. Velocidade do vento externo [mph]
26. Direção do vento externo [deg]


# Meta
Datacenter PUE 1.0 com redução de consumo de energia de 70%

Refrigeração: redução de consumo de energia de 70%
