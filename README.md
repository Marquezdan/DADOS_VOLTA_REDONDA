# Dados de Telemetria de VCI e VPA

Repositório com os dados de medição veicular utilizados no projeto **Descarbonize.ai**, no contexto da comparação entre **veículos a combustão interna (VCI)** e **veículos de propulsão alternativa (VPA)**, com foco em telemetria, análise exploratória de dados e apoio a atividades de modelagem e engenharia reversa de sinais automotivos.

## Visão geral

Este repositório reúne arquivos de telemetria obtidos em campanhas de coleta realizadas com veículos instrumentados, incluindo:

- registros de variáveis disponibilizadas via interface de diagnóstico **OBD-II**;
- arquivos de captura bruta do barramento **CAN**;
- arquivos intermediários e resultados de tratamento básico das bases;
- insumos para análise comparativa entre veículos elétricos e veículos a combustão.

Parte relevante destes dados foi utilizada na campanha de coleta descrita no relatório técnico do projeto, com medições realizadas em Volta Redonda, nas quais foram instrumentados veículos de diferentes arquiteturas de propulsão.

## Contexto da coleta

Na campanha descrita no relatório, os veículos instrumentados incluíram:

- Volkswagen Fox;
- Volkswagen Nivus;
- BYD Dolphin Mini;
- Peugeot e-2008 GT.

Nos veículos elétricos, a estratégia de medição combinou duas fontes principais:

1. **Leituras diagnósticas via OBD-II**, obtidas com o aplicativo **Car Scanner** conectado ao veículo por meio de um **scanner OBD-II VGate iCar Pro com interface Bluetooth**;
2. **Captura bruta do barramento CAN**, realizada com um **Raspberry Pi 5** equipado com módulo **PiCAN3 HAT**.

Essa arquitetura permitiu usar as leituras diagnósticas como **referência observável para correlação e validação**, enquanto os arquivos de tráfego bruto do CAN foram empregados no processo de engenharia reversa e identificação de sinais veiculares.

## Objetivo do repositório

Este repositório tem como objetivos principais:

- centralizar os dados de telemetria coletados nas campanhas experimentais;
- apoiar análises exploratórias e comparativas entre VCI e VPA;
- disponibilizar bases para experimentos de pré-processamento, sincronização e modelagem;
- apoiar atividades de engenharia reversa de sinais veiculares, especialmente em contextos com documentação pública limitada;
- preservar os dados utilizados nos relatórios técnicos e nas etapas analíticas do projeto.

## Tipos de dados disponíveis

Os conjuntos de dados deste repositório podem incluir, conforme a campanha de coleta:

- arquivos `.csv` com variáveis diagnósticas e telemetria derivada;
- arquivos de texto com quadros brutos do barramento CAN;
- arquivos tratados ou padronizados para análise posterior;
- tabelas auxiliares e metadados de apoio à interpretação das medições.

Em termos gerais, os dados podem conter informações como:

- tempo de amostragem;
- velocidade;
- aceleração;
- altitude;
- latitude e longitude;
- distância percorrida;
- consumo instantâneo;
- potência;
- tensão e corrente de bateria;
- estado de carga da bateria (*State of Charge*), para veículos elétricos;
- variáveis associadas a pedal de aceleração, pedal de freio, torque e outros parâmetros veiculares.

## Estratégia de aquisição dos dados

A obtenção dos dados seguiu uma abordagem multicanal:

### 1. Interface diagnóstica OBD-II
As leituras disponibilizadas pela interface de diagnóstico foram registradas pelo aplicativo Car Scanner em arquivos `.csv`. Esses dados foram utilizados como base de referência para correlação com os sinais identificados em outras fontes.

### 2. Sniffing direto do barramento CAN
Em paralelo, o Raspberry Pi com PiCAN realizou a captura do tráfego bruto da rede CAN do veículo. Os registros incluem informações como:

- timestamp;
- identificador da ECU;
- tamanho da carga útil;
- bytes brutos em formato hexadecimal.

### 3. Apoio à engenharia reversa
Os dados deste repositório também dão suporte ao processo de engenharia reversa descrito no relatório técnico, no qual:

- foram analisados logs de comunicação entre aplicativo e scanner OBD-II;
- foi identificado o uso de serviços de diagnóstico baseados em **UDS**;
- quadros CAN foram agrupados e correlacionados com leituras observáveis;
- sinais relevantes foram alinhados temporalmente para identificação de parâmetros veiculares.

## Organização esperada do repositório

A estrutura pode evoluir ao longo do projeto, mas recomenda-se organizar os conteúdos em grupos como:

```text
.
├── raw/
│   ├── vci/
│   └── vpa/
├── processed/
│   ├── vci/
│   └── vpa/
├── metadata/
├── notebooks/
├── scripts/
└── docs/
