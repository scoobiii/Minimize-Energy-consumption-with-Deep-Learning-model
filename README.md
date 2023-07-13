# DeepCool 
Dois métodos diferentes são usados para melhorar a eficiência energética dos data clouds. O primeiro é o controle de autoajustamento (empregado pela Vertiv), que é um tipo de IA que pode ser usado para otimizar o desempenho do sistema de resfriamento de um data cloud. O segundo é o deep learning, aprendizado profundo, para otimizar o uso de energia dos servidores em um data cloud.

Ambos os métodos têm o potencial de reduzir significativamente o consumo de energia dos data clouds. O controle de autoajustamento pode melhorar a eficiência do sistema de resfriamento ajustando automaticamente os parâmetros de resfriamento de acordo com as condições atuais. O aprendizado profundo pode melhorar a eficiência do uso de energia dos servidores otimizando o uso da CPU, memória e armazenamento.

Embora ambos os métodos tenham o potencial de reduzir significativamente o consumo de energia, o aprendizado profundo tem o potencial de ser mais eficaz do que o controle de autoajustamento. O aprendizado profundo pode aprender com os dados históricos para prever as condições futuras e ajustar os parâmetros do sistema de acordo. O controle de autoajustamento, por outro lado, só pode ajustar os parâmetros do sistema de acordo com as condições atuais.

Ambos os métodos são promissores e provavelmente serão usados em conjunto no futuro. O controle de autoajustamento pode ser usado para melhorar a eficiência geral do sistema de resfriamento, enquanto o aprendizado profundo pode ser usado para otimizar o uso de energia dos servidores. Essa combinação de métodos pode levar a uma redução significativa no consumo de energia dos data clouds.

Aqui estão alguns detalhes adicionais sobre os dois métodos:

* **Controle de autoajustamento:** O controle de autoajustamento é um tipo de IA que pode ser usado para otimizar o desempenho do sistema de resfriamento de um data cloud. Ele faz isso monitorando constantemente as condições do ambiente e ajustando os parâmetros de resfriamento de acordo. Por exemplo, se a temperatura do ar aumentar, o controle de autoajustamento pode ligar os chillers ou aumentar a velocidade dos ventiladores. Se a temperatura do ar cair, o controle de autoajustamento pode desligar os chillers ou diminuir a velocidade dos ventiladores.
* **Aprendizado profundo:** O aprendizado profundo é um tipo de IA que pode ser usado para aprender com os dados históricos e prever as condições futuras. Isso pode ser usado para otimizar o uso de energia dos servidores em um data cloud. Por exemplo, o aprendizado profundo pode ser usado para prever a carga de trabalho de um servidor e ajustar o uso da CPU, memória, trafego de dados, temperatura dos nucleos, uso de memoria, consumo de energia por prompt e armazenamento de acordo. Isso pode levar a uma redução no consumo de energia dos servidores impactando o PUE.
 
# DeepCool
Use o modelo Deep Q-Learning para otimizar o consumo de energia de um data cloud e sistemas de Refrigeração

Este projeto utiliza um modelo de aprendizado profundo de IA para otimizar e reduzir o consumo de energia de um data cloud em até 70%.
O modelo AI usa o algoritmo Q-Learning para determinar a melhor ação em cada etapa de tempo.
O Q-Learning é baseado nas equações de Bellman que estão na raiz do Reinforcement Learning.

# Descrição
O projeto visa reduzir o consumo de energia de uma instalação industrial. Um modelo de otimização de aprendizado profundo é usado e comparado com o sistema de resfriamento integrado tradicional. A abordagem é inspirada na redução de 40% alcançada nos data clouds do Google usando o modelo DeepMind AI. O projeto faz parte do módulo de Inteligência Artificial para Negócios da Udemy.

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

<img src="tela principal print.png" width="80%" height="80%" />


<img src="Brain_Slide.png" width="80%" height="80%" />

# Resultados

A porcentagem de energia economizada varia de acordo com os experimentos. A porcentagem é determinada simulando um ciclo anual completo. A amostra abaixo atingiu 68% do consumo de energia graças ao AI em comparação com o sistema de resfriamento integrado usual. Ambos os modelos visam manter o servidor dentro de uma faixa de temperatura ideal de 18 ° a 24 ° C. A simulação é realizada em intervalos de tempo de um minuto ao longo de um ano inteiro.

<img src="savings.png" width="80%" height="80%" />

# Os recursos da rede neural são listados a seguir:

# DeepCloud 

1. Fabricante, modelo, numero de serie do Sistema de Resfriamento (chiller)
2. Fabricante, modelo, numero de serie do sistemas de resfriamento interno (fancoil) ou equivalente
2. Fabricante, modelo, numero de serie do hack U
3. Fabricante, modelo, numero de serie do server, quantidade de nucles
4. Server - Temperatura por nucleos
5. Server - Carga de uso por CPU
6. Server - Carga de uso de memória ram
7. Server - Numero de usuarios
8. Server - Consumo de ernergia por CPU kwh
9. Server - Consumo de ernergia por prompt kwh
10. Server - Consumo de energia por server kwh
11. Carga total de TI do hack U [kW]
12. Carga total de TI do data cloud [kW]
13. Carga de TI total da sala de rede principal do campus (CCNR) [kW]
14. Número total de bombas de água Agua Gelada de processo (PWP) em execução
15. Velocidade média do conversor de frequência variável (VFD) [%]
16. Número total de bombas de água do condensador (CWP) funcionando
17. Velocidade média do conversor de frequência variável (VFD) [%]
18. Número total de torres de resfriamento funcionando
19. Ponto de ajuste médio da temperatura de saída da água da torre de resfriamento (LWT) [F]
20. Número total de chillers funcionando
21. Número total de drycoolers funcionando
22. Número total de bombas de injeção de água gelada funcionando
23. Temperatura média do ponto de ajuste da bomba de injeção de água gelada [F]
24. Temperatura média de aproximação do trocador de calor [F]
25. Temperatura do bulbo úmido do ar externo (WB) [F]
26. Temperatura do bulbo seco do ar externo (DB) [F]
27. Entalpia de ar externo [kJ / kg]
28. Umidade relativa do ar externo (UR) [%]
29. Velocidade do vento externo [mph]
30. Direção do vento externo [deg]
31. Fabricante, modelo, numero de serie, capacidade do gerador a gas natural/H2 (10%), capacidade
32. Fabricante, modelo, numero de serie, capacidade do chiller elétrico
33. Fabricante, modelo, numero de serie, capacidade do chiller não eletrico (absorção)
34. Certificação: PUE
35. Certificação: TIER
36. Certificação: ISO 50001
37. 
38. BenchMark: Gerenciador de unidades de refrigeração Liebert iCOM : O novo sistema Liebert iCOM controla múltiplas unidades de refrigeração ajudando a reduzir o consumo de energia do equipamento de ar condicionado em até 50%. É um ponto único para centralizar os dados de unidades de refrigeração e sensores de temperatura para harmonizar e otimizar o desempenho do sistema térmico em todo o data cloud, obter acesso rápido aos dados acionáveis e automatizar diagnósticos e tendências do sistema.: [https://www.vertiv.com/49f28a/globalassets/shared/liebert-icom-intelligent-communication-and-monitoring-for-liebert-dse-packaged_00.pdf](https://www.vertiv.com/48daea/globalassets/products/thermal-management/thermal-control-and-monitoring/liebert-icom-br-pt-br-latam-sl-18843.pdf) https://www.vertiv.com/490a89/globalassets/products/thermal-management/thermal-control-and-monitoring/liebert-icom-s-user-manual.pdf
39. BenchMark: Unidade de Free-Cooling Evaporativo Indireto Liebert EFC. O Liebert EFC consegue reduzir as temperaturas do ar aplicando o princípio do arrefecimento evaporativo. O processo envolve a evaporação de água que, como consequência, arrefece o ar circundante. Através desta tecnologia, o Liebert EFC consegue atingir níveis de pPUE de 1.2, garantindo a máxima eficiência energética e minimizando os custos operativos
40. BenchMark: Liebert DSE Packaged Free-Cooling Solution, 400-500kW Perimeter Configuration: https://www.vertiv.com/4a4edb/globalassets/shared/liebert-dse400-ds-en-na-sl-18937_209440.pdf
41. BenchMark: Chiller com Free Cooling Adiabático Liebert AFC 500 a 1450 kW: O Liebert® AFC combina os níveis excepcionais de eficiência energética permitidos pelo free cooling com a disponibilidade contínua garantida pelo sistema auxiliar por compressor multi-scroll e o sistema adiabático. Este último umidifica o ar que entra nas serpentinas de free cooling e de condensação, aumentando as horas de operação em free cooling e a eficiência mecânica. https://www.vertiv.com/499942/globalassets/products/thermal-management/free-cooling-chillers/liebert-afc-br-pt-br-latam-mka4l0ukafc-pt-rev.3-11-2014.pdf
42. BenchMark: Liebert HPC-S - Air-cooled, Freecooling and Adiabatic Freecooling Chillers https://www.vertiv.com/499942/globalassets/products/thermal-management/free-cooling-chillers/liebert-afc-br-pt-br-latam-mka4l0ukafc-pt-rev.3-11-2014.pdf
43. BenchMark: https://www.vertiv.com/499942/globalassets/products/thermal-management/free-cooling-chillers/liebert-afc-br-pt-br-latam-mka4l0ukafc-pt-rev.3-11-2014.pdf

# Meta
Datacenter PUE 1.0 com redução de consumo de energia de 70%

# DeepEnergy
Ambos os métodos são promissores e provavelmente serão usados em conjunto no futuro, o objetivo presente, do DeepCool ao ampliar o alcance do MECDLM. A combinação de métodos pode levar a uma redução significativa no consumo de energia dos data clouds validada, mensurada, qualificada e certificada na conta de luz, a ser neutralizada com o uso de geradores de energia ativos, full time, turbinas hibridas com eficiência energética de 85%, a gas natural (90%) e hidrogênio (10%) na fase I, podendo chegar a NG/H2 15/85% suprido por gasodutos hibridos NG/H2, ja que as turbinas hibridas já são comerciais e aguardam upgrade das distribuidoras de gas

# DeepH2
H2. Esse cara é um elemnto importante do hack energy e transição para NetZero

# DeepChiller
Chiller a absorção, não elétrico, convertem o calor residul proveniente de DeepEnergy em Frio para resfriamento, air cooling ou server liquid cooling

# DeepTiac
Sistema de resfriamento do ar na entrada das turbinas hibridas, assegurando a condição ISO de projeto 15oC/60% 

# DeepFog
Sistema de aspersão de vapor (15 oC na entrada das deepturbines) para assegurar controle de temperatura e umidade relativa.

# DeepFood
DeepFood reduz a conta de energia dos sistemas de refrigeração e gas do nosso proximo fogão wok, https://youtu.be/02QMhK3OAdw, portanto, deepfood vai muito além, pois demanda gasodutos hibridos, gas natural e hidrogênio, inciando a NG/H2 90/10%, para fogões, aquecedodores residenciais, residenciais, comerciais e industriais impactando e reduzindo significativamente as emissões 

# DeepODS 
os 17 ODS e 169 metas e indicadores são atendidos pelo #DeepHack no sistema de energia, antes, durante e depois da trainsição #netZero em 2050, passando por redução de emissões em 20% até o ODS2030, base emissões 2017, aumento do gdp per capita em São Paulo para US$50.000,00 até 2030 alinhado alinhado ao PANCLIMA para zerar ao aquecimento global até 2050, sub produto de power losses (ineficiência energética)
https://lh6.googleusercontent.com/z_UI18ELpfqeMJOWqBVf8Oc8nhAzsvbxHooJAMTCWH8CAXSl5OSFXsevBvy-YIJEZ8VR_E9bIfFMNZuscCBXW5XfTbIrnCTKL-nggJOdJ3Iw2euU8D7aijD0uKTS5cQhqvSD0_8JzEHlufVS_QNka_s

# DeepRendaPercapita
Graças ao Pré Sal, Maricá no Rio de Janeiro teve incremento de renda per capita de US$2000.00 em 2010, para US$45.000 em 2019, maior que o japão, portanto, vale a penao o #hackenergy com expectativa de melhor ganho em renda per capita.
