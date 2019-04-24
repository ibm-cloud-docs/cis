---
copyright:
  years: 2018
lastupdated: "2018-03-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Conceitos de ataque distribuído por negação de serviço (DDoS)

Os ataques DDoS estão entre os tipos mais comuns de ataques na Internet que seu website ou host poderá encontrar.

## O que é um ataque DDoS?
Um ataque distribuído por negação de serviço (DDoS) é uma tentativa maliciosa de interromper o tráfego normal de um servidor, serviço ou rede sobrecarregando o destino ou sua infraestrutura circundante com uma enxurrada de tráfego de Internet. Os ataques DDoS atingem a eficácia utilizando muitos sistemas de computador comprometidos como fontes de tráfego de ataque. As máquinas exploradas podem incluir computadores e outros recursos de rede, como dispositivos IoT. Em um alto nível, um ataque DDoS é como um engarrafamento em uma rodovia, impedindo que o tráfego normal chegue ao seu destino desejado.

## Como um ataque DDoS funciona?
Um invasor obtém o controle de uma rede de máquinas on-line para realizar um ataque DDoS. Computadores e outras máquinas (como dispositivos IoT) são infectados com malware, transformando cada um em um robô (ou zumbi). O invasor controla o grupo de robôs, que é chamado de _botnet_. 

Após estabelecer um botnet, o invasor direciona as máquinas enviando instruções atualizadas para cada robô usando o controle remoto. Um endereço IP de destino pode receber solicitações de uma multidão de robôs, causando um estouro de capacidade do servidor ou rede de destino. Isso cria uma negação de serviço para o tráfego normal. Como cada robô é um dispositivo de Internet legítimo, separar o tráfego de ataque do tráfego normal pode ser difícil. 

## Quais são os tipos comuns de ataques DDoS?
Os vetores de ataque DDoS visam componentes variados de uma conexão de rede. Embora quase todos os ataques DDoS envolvam sobrecarregar um dispositivo ou rede de destino com tráfego, os ataques podem ser divididos em três categorias. Um invasor pode usar um ou diversos vetores de ataque e pode até mesmo percorrer esses vetores de ataque com base nas contramedidas tomadas pelo destino.

Os tipos comuns são:

 * Ataques da camada de aplicativo (camada 7)
 * Ataques de protocolo (camadas 3 e 4)
 * Ataques volumétricos (ataques de amplificação)

###	Ataques da camada de aplicativo
Um ataque de camada de aplicativo às vezes é referido como um _ataque DDoS de camada 7_ (em referência à sétima camada do modelo OSI). O objetivo desses ataques é esgotar os recursos da vítima, atacando a camada onde as páginas da web são geradas no servidor e entregues aos visitantes em resposta a solicitações de HTTP (ou seja, a camada de aplicativo). Os ataques da camada 7 são difíceis, porque pode ser difícil identificar o tráfego como malicioso.

###	Ataques de protocolo
Os ataques de protocolo utilizam fragilidades na camada 3 e camada 4 da pilha de protocolo ISO para tornar o destino inacessível. Esses ataques, também conhecidos como ataques de estado de exaustão, causam uma interrupção do serviço consumindo toda a capacidade da _tabela de estado_ disponível de servidores de aplicativos da web ou de recursos intermediários como firewalls e balanceadores de carga. 
  
###	Ataques volumétricos
Essa categoria de ataques tenta criar congestionamento consumindo toda a largura da banda disponível entre o alvo e a Internet mais ampla. Grandes quantidades de dados são enviadas para um destino utilizando um formulário de amplificação ou por outros meios de criar o tráfego em massa, como solicitações de um botnet. 


## O que eu faço se estiver sob um ataque DDoS?

**Etapa 1:** ative o “Modo de defesa" na tela **Visão geral**. 

![Modo de defesa](images/defense-mode.png)

**Etapa 2:** configure seus registros DNS para o máximo de segurança.

**Etapa 3:** não defina um limite de taxa nem regule solicitações do IBM CIS. Precisamos da largura da banda para ajudá-lo com sua situação.

**Etapa 4:** bloqueie países específicos e visitantes se necessário.
