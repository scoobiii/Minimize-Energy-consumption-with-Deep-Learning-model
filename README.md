# Minimize Energy Consumption with Deep Learing Model
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


# DeepCool 
Dois métodos diferentes são usados para melhorar a eficiência energética dos data clouds. O primeiro é o **controle de autoajustamento, que é um tipo de IA** que pode ser usado para otimizar o desempenho do sistema de resfriamento de um data cloud. O segundo é o **deep learning, aprendizado profundo**, para otimizar o uso de energia dos servidores em um data cloud.
O projeto faz parte do módulo de **Inteligência Artificial DeepEnergy para Negócios da Udemy.**

Ambos os métodos têm o potencial de reduzir significativamente o consumo de energia dos data clouds. O controle de autoajustamento pode melhorar a eficiência do sistema de resfriamento ajustando automaticamente os parâmetros de resfriamento de acordo com as condições atuais. O aprendizado profundo pode melhorar a eficiência do uso de energia dos servidores otimizando o uso da CPU, memória e armazenamento.

Embora ambos os métodos tenham o potencial de reduzir significativamente o consumo de energia, o aprendizado profundo tem o potencial de ser mais eficaz do que o controle de autoajustamento. O aprendizado profundo pode aprender com os dados históricos para prever as condições futuras e ajustar os parâmetros do sistema de acordo. O controle de autoajustamento, por outro lado, só pode ajustar os parâmetros do sistema de acordo com as condições atuais.

Ambos os métodos são promissores e vamos aplica-los simultaneamente. O controle de autoajustamento pode ser usado para melhorar a eficiência geral do sistema de resfriamento, enquanto o aprendizado profundo pode ser usado para otimizar o uso de energia dos servidores. Essa combinação de métodos pode levar a uma redução significativa no consumo de energia dos data clouds.

Aqui estão alguns detalhes adicionais sobre os dois métodos:

* **Controle de autoajustamento:** O controle de autoajustamento é um tipo de IA, estado da arte empregado pelo mercado, que pode ser usado para otimizar o desempenho do sistema de resfriamento de um data cloud. Ele faz isso monitorando constantemente as condições do ambiente e ajustando os parâmetros de resfriamento de acordo. Por exemplo, se a temperatura do ar aumentar, o controle de autoajustamento pode ligar os chillers ou aumentar a velocidade dos ventiladores. Se a temperatura do ar cair, o controle de autoajustamento pode desligar os chillers ou diminuir a velocidade dos ventiladores.
* **Aprendizado profundo:** O aprendizado profundo é um tipo de IA que pode ser usado para aprender com os dados históricos e prever as condições futuras. Isso pode ser usado para otimizar o uso de energia dos servidores em um data cloud. Por exemplo, o aprendizado profundo pode ser usado para prever a carga de trabalho de um servidor e ajustar o uso da CPU, memória, trafego de dados, temperatura dos nucleos, uso de memoria, consumo de energia por prompt e armazenamento de acordo. Isso pode levar a uma redução no consumo de energia dos servidores impactando o PUE.
 
# DeeDeep

| Atividade | Consumo de energia (watts) | Tempo (minutos) | Consumo de energia (kWh) | Custo (R$) |
|---|---|---|---|---|
| Banho 😱 | 5500 | 10 | 5,5 | 0,34 |
| Mineração de *PLIMM 😱😱 | 4466,8 | 10 | 4,47 | 0,28 |
| Gerando Prompt GPT 😱😱😱 | 2600,84 | 10 | 2,6 | 0,16 |

*[PLIMM Initiative](https://opensea.io/collection/plimm)
 [USA&CCNFT Initiative](https://opensea.io/collection/usa-ccnfts)
 [PopLixo Initiative](https://opensea.io/collection/poplixo)
 [PopCity Initiative](https://opensea.io/collection/poplixocity)

# Gerar um prompt chatgpt, consome absurdos de energia, portanto, para viabilizar AI e veiculos elétricos.....

Como você pode ver, a mineração de PLIMM consome mais energia do que um banho ou gerar prompt. No entanto, o custo da mineração de PLIMM é menor do que o custo de um banho ou gerar prompt, porque o PLIMM é uma moeda digital que pode ser minerada com um computador.

É importante notar que esses são apenas exemplos e o consumo real de energia pode variar dependendo do modelo específico do chuveiro, da temperatura da água e da duração do banho.

**Project News** ⚡ 

- \[2023/07\] [`ZeusMonitor`](https://ml.energy/zeus/reference/monitor/#zeus.monitor.ZeusMonitor) was used to profile GPU time and energy consumption for the [ML.ENERGY leaderboard](https://ml.energy/leaderboard).
- \[2023/03\] [Chase](https://symbioticlab.org/publications/files/chase:ccai23/chase-ccai23.pdf), an automatic carbon optimization framework for DNN training, will appear at ICLR'23 workshop.
- \[2022/11\] [Carbon-Aware Zeus](https://taikai.network/gsf/hackathons/carbonhack22/projects/cl95qxjpa70555701uhg96r0ek6/idea) won the **second overall best solution award** at Carbon Hack 22.
---

Zeus is a framework for (1) measuring GPU energy consumption and (2) optimizing energy and time for DNN training.

### Measuring GPU energy

```python
from zeus.monitor import ZeusMonitor

monitor = ZeusMonitor(gpu_indices=[0,1,2,3])

monitor.begin_window("heavy computation")
# Four GPUs consuming energy like crazy!
measurement = monitor.end_window("heavy computation")

print(f"Energy: {measurement.total_energy} J")
print(f"Time  : {measurement.time} s")
```

### Finding the optimal GPU power limit

Zeus silently profiles different power limits during training and converges to the optimal one.

```python
from zeus.monitor import ZeusMonitor
from zeus.optimizer import GlobalPowerLimitOptimizer

monitor = ZeusMonitor(gpu_indices=[0,1,2,3])
plo = GlobalPowerLimitOptimizer(monitor)

plo.on_epoch_begin()

for x, y in train_dataloader:
    plo.on_step_begin()
    # Learn from x and y!
    plo.on_step_end()

plo.on_epoch_end()
```

Please refer to our NSDI’23 [paper](https://www.usenix.org/conference/nsdi23/presentation/you) and [slides](https://www.usenix.org/system/files/nsdi23_slides_chung.pdf) for details.
Checkout [Overview](https://ml.energy/zeus/overview/) for a summary.

Zeus is part of [The ML.ENERGY Initiative](https://ml.energy).

## Repository Organization

```
.
├── zeus/                # ⚡ Zeus Python package
│   ├── optimizer/       #    - GPU energy and time optimizers
│   ├── run/             #    - Tools for running Zeus on real training jobs
│   ├── policy/          #    - Optimization policies and extension interfaces
│   ├── util/            #    - Utility functions and classes
│   ├── monitor.py       #    - `ZeusMonitor`: Measure GPU time and energy of any code block
│   ├── controller.py    #    - Tools for controlling the flow of training
│   ├── callback.py      #    - Base class for Hugging Face-like training callbacks.
│   ├── simulate.py      #    - Tools for trace-driven simulation
│   ├── analyze.py       #    - Analysis functions for power logs
│   └── job.py           #    - Class for job specification
│
├── zeus_monitor/        # 🔌 GPU power monitor
│   ├── zemo/            #    -  A header-only library for querying NVML
│   └── main.cpp         #    -  Source code of the power monitor
│
├── examples/            # 🛠️ Examples of integrating Zeus
│
├── capriccio/           # 🌊 A drifting sentiment analysis dataset
│
└── trace/               # 🗃️ Train and power traces for various GPUs and DNNs
```


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
Ambos os métodos são promissores e provavelmente serão usados em conjunto no futuro, o objetivo presente, do DeepCool ao ampliar o alcance do MECDLM. A combinação de métodos pode levar a uma redução significativa no consumo de energia dos data clouds validada, mensurada, qualificada e certificada na conta de luz, a ser neutralizada com o uso de geradores de energia ativos, full time, turbinas hibridas com eficiência energética de 85%, a gas natural (90%) e hidrogênio (10%) na fase I, podendo chegar a NG/H2 15/85% suprido por gasodutos hibridos NG/H2, ja que as turbinas hibridas já são comerciais e aguardam upgrade das distribuidoras de gas.
Lição de casa para a **Arsesp **é responsável​ por regular, controlar e fiscalizar os serviços de distribuição de gás natural canalizado prestado pelas três concessionárias que atuam no mercado paulista: ​a Companhia de Gás de São Paulo (Comgás);

Componentes do Data Center:

Processamento:
Servidores: Responsáveis pelo processamento de dados.
Unidades de processamento gráfico (GPUs): Usadas para acelerar cálculos intensivos em paralelo.
Processadores (CPUs): Realizam as operações de processamento principal.
Número de núcleos: Determina a capacidade de processamento paralelo do servidor.
Variáveis relacionadas ao servidor:

Variáveis gerais do servidor:
cooling_type: Tipo de resfriamento do servidor (air cooling, liquid cooling).
number_cores: Número de núcleos do servidor.
intrinsic_temperature_nucleo: Temperatura intrínseca do servidor por núcleo.
total_memory: Quantidade total de memória do servidor.
total_storage: Capacidade total de armazenamento do servidor.
memory_usage: Uso atual de memória.
storage_usage: Uso atual de armazenamento.
server_voltage: Tensão de entrada do servidor.
server_current: Corrente consumida pelo servidor.
server_power_consumption: Consumo de energia do servidor em kWh.
hack_voltage: Tensão de entrada do servidor.
hack_current: Corrente consumida pelo servidor.
hack_power_consumption: Consumo de energia do servidor em kWh.
Variáveis do sistema de resfriamento a ar:
fan_speed: Velocidade das ventoinhas do sistema de resfriamento (air cooling).
min_fan_speed: Velocidade mínima permitida para as ventoinhas.
max_fan_speed: Velocidade máxima permitida para as ventoinhas.
air_flow: Fluxo de ar do sistema de resfriamento a ar.
min_air_flow: Fluxo de ar mínimo permitido para o sistema de resfriamento a ar.
max_air_flow: Fluxo de ar máximo permitido para o sistema de resfriamento a ar.
fan_pwm_min: Valor mínimo de modulação por largura de pulso (PWM) para controlar as ventoinhas.
fan_pwm_max: Valor máximo de modulação por largura de pulso (PWM) para controlar as ventoinhas.
Variáveis relacionadas ao sistema de resfriamento líquido (server liquid cooling):

Variáveis do sistema de resfriamento líquido:
pump_speed: Velocidade da bomba do sistema de resfriamento líquido.
min_pump_speed: Velocidade mínima permitida para a bomba.
max_pump_speed: Velocidade máxima permitida para a bomba.
pump_pwm_min: Valor mínimo de modulação por largura de pulso (PWM) para controlar a bomba.
pump_pwm_max: Valor máximo de modulação por largura de pulso (PWM) para controlar a bomba.
pump_voltage: Tensão de entrada do servidor.
pump_current: Corrente consumida pelo servidor.
pump_power_consumption: Consumo de energia do servidor em kWh.
coolant_temperature_in: Temperatura do fluido de resfriamento na entrada do servidor (arrefecimento líquido).
coolant_temperature_out: Temperatura do fluido de resfriamento na saída do servidor (arrefecimento líquido).
fluid_flow: Fluxo de fluido no servidor.
min_fluid_flow: Fluxo mínimo de fluido permitido no servidor.
max_fluid_flow: Fluxo máximo de fluido permitido no servidor.
Armazenamento:

Discos rígidos (HDDs): Fornecem armazenamento de dados em dispositivos magnéticos.
Unidades de estado sólido (SSDs): Fornecem armazenamento de dados em chips de memória flash.
Capacidade total de armazenamento: Quantidade máxima de dados que o Data Center pode armazenar.
Uso atual de armazenamento: Quantidade de dados atualmente armazenados no Data Center.
Transferência de Dados:

Switches de rede: Permitem a conectividade entre servidores e dispositivos de rede.
Roteadores: Encaminham pacotes de dados entre redes.
Firewalls: Protegem o Data Center contra ameaças de segurança de rede.
Taxa de transferência de rede: Velocidade de transferência de dados dentro do Data Center.
Demanda de Sistemas de Energia:

Tensão de entrada do servidor: Tensão elétrica fornecida ao servidor.
Corrente consumida pelo servidor: Quantidade de corrente elétrica consumida pelo servidor.
Consumo de energia do servidor: Quantidade de energia consumida pelo servidor em kWh.
Resfriamento por Sistema Operacional:

Tipo de resfriamento do servidor: Air Cooling (resfriamento a ar) ou Liquid Cooling (resfriamento líquido).
Temperatura intrínseca do servidor por núcleo: Temperatura de operação normal do servidor.
Temperatura do fluido de resfriamento na entrada/saída do servidor: Temperatura do fluido de resfriamento usado para resfriar o servidor.
*Variáveis relacionadas ao sistema de resfriamento a ar (fan coil server air cooling):

Variáveis do sistema de resfriamento a ar:
fan_speed: Velocidade das ventoinhas do sistema de resfriamento (air cooling).
min_fan_speed: Velocidade mínima permitida para as ventoinhas.
max_fan_speed: Velocidade máxima permitida para as ventoinhas.
air_flow: Fluxo de ar do sistema de resfriamento a ar.
min_air_flow: Fluxo de ar mínimo permitido para o sistema de resfriamento a ar.
max_air_flow: Fluxo de ar máximo permitido para o sistema de resfriamento a ar.
fan_pwm_min: Valor mínimo de modulação por largura de pulso (PWM) para controlar as ventoinhas.
fan_pwm_max: Valor máximo de modulação por largura de pulso (PWM) para controlar as ventoinhas.
coolant_temperature_in: Temperatura do fluido de resfriamento na entrada do servidor (arrefecimento a ar).
coolant_temperature_out: Temperatura do fluido de resfriamento na saída do servidor (arrefecimento a ar).
voltage: Tensão
current: Corrente consumida
power_consumption: Consumo de energia kWh.
Variáveis relacionadas ao sistema de resfriamento centralizado (central chiller system):

Variáveis do sistema de resfriamento

centralizado:

chiller_temperature_in: Temperatura do fluido de resfriamento na entrada da central de água gelada.
chiller_temperature_out: Temperatura do fluido de resfriamento na saída da central de água gelada.
chiller_voltage: Tensão de alimentação do sistema de resfriamento centralizado.
chiller_current: Corrente elétrica consumida pelo sistema de resfriamento centralizado.
chiller_power: Consumo de energia do sistema de resfriamento centralizado em kWh.
chiller_pump_speed: Velocidade da bomba de circulação do sistema de resfriamento centralizado.
chiller_fan_speed: Velocidade dos ventiladores do sistema de resfriamento centralizado.
pump_voltage_cooling: Tensão de entrada do bomba
pump_current_cooling: Corrente consumida pela bomba
pump_power_consumption_cooling: Consumo de energia do servidor em kWh.
pump_voltage_hot: Tensão da bomba de condensação.
pump_current_hot: Corrente da bomba de condensação.
`pump_power_consumption_hot: Consumo da bomba de condensação.
cooling_tower_voltage: Tensão do motor da Torre de Resfriamento
cooling_tower_current: Corrente do motor da Torre de Resfriamento
`cooling_tower_consumption: Consumo do motor da Torre de Resfriamento
Demanda de Energia e Resfriamento para os Sistemas de Energia:

Consumo de energia do sistema de resfriamento centralizado: Quantidade de energia consumida pelo sistema de resfriamento centralizado em kWh.
Velocidade da bomba de circulação do sistema de resfriamento centralizado: Velocidade da bomba do sistema de resfriamento centralizado.
Velocidade dos ventiladores do sistema de resfriamento centralizado: Velocidade dos ventiladores do sistema de resfriamento centralizado.
Potência do sistema de resfriamento centralizado: Consumo total de energia do sistema de resfriamento centralizado.
Temperatura do fluido de resfriamento na entrada/saída da central de água gelada: Temperatura do fluido de resfriamento usado no sistema de resfriamento centralizado.
Parâmetros PUE (Power Usage Effectiveness) para Sistemas de Resfriamento:

Energia total consumida pelo Data Center.
Energia consumida exclusivamente pelos servidores.
Energia consumida pelo sistema de resfriamento líquido (chiller).
Esses são alguns dos principais componentes e parâmetros relacionados ao processamento, armazenamento, transferência de dados, demandas de sistemas de energia, resfriamento por sistema operacional e demandas de energia e resfriamento para os sistemas de energia em um Data Center.

Parâmetros PUE para sistemas de resfriamento:

O PUE (Power Usage Effectiveness) é uma métrica usada para avaliar a eficiência energética de um data center. Ele é calculado como a razão entre a energia total consumida pelo data center (incluindo servidores, sistemas de resfriamento, iluminação, etc.) e a energia consumida exclusivamente pelos servidores.

Para o cálculo do PUE, os seguintes parâmetros são utilizados:

Para sistemas de resfriamento a ar (air cooling):

power_total: Energia total consumida pelo data center.

power_servers: Energia consumida exclusivamente pelos servidores.

PUE = power_total / power_servers

Para sistemas de resfriamento líquido (liquid cooling):

power_total: Energia total consumida pelo data center.

power_servers: Energia consumida exclusivamente pelos servidores.

power_chiller: Energia consumida pelo sistema de resfriamento líquido (chiller).

PUE = (power_total - power_chiller) / power_servers

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

# DeepHackEnergy

os 17 ODS e 169 metas e indicadores são atendidos pelo #DeepHack no sistema de energia, antes, durante e depois da trainsição #netZero em 2050, passando por redução de emissões em 20% até o ODS2030, base emissões 2017, aumento do gdp per capita em São Paulo para US$50.000,00 até 2030 alinhado alinhado ao PANCLIMA para zerar ao aquecimento global até 2050, sub produto de power losses (ineficiência energética)

<img src="https://lh4.googleusercontent.com/N-jysswi3F09FriSlYmm9eVVTNQlmixAwZ_qPVPkfYWgPI0SByr1dyFM8JreMtxQ07tFUMceq79SzKyz21OY86-n3QDIudZfcwKNBTMU60raco1n29XJTVJqNh7toeCVo8z3C-rEwT8qKNO-gcC-9sU" width="80%" height="80%" />


<img src="https://lh6.googleusercontent.com/z_UI18ELpfqeMJOWqBVf8Oc8nhAzsvbxHooJAMTCWH8CAXSl5OSFXsevBvy-YIJEZ8VR_E9bIfFMNZuscCBXW5XfTbIrnCTKL-nggJOdJ3Iw2euU8D7aijD0uKTS5cQhqvSD0_8JzEHlufVS_QNka_s" width="80%" height="80%" />

# DeepRendaPercapita
Graças ao Pré Sal, Maricá no Rio de Janeiro teve incremento de renda per capita de US$2000.00 em 2010, para US$45.000 em 2019, maior que o japão, portanto, vale a penao o #hackenergy com expectativa de melhor ganho em renda per capita.

# DeepPi3B

Rodar a porra toda num rasp
