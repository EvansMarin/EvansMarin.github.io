# Olá. Eu sou o Victor

# Laboratório: Segmentação de Rede e Roteamento Inter-VLAN

Neste projeto, implementei a segmentação lógica de uma rede local (LAN) para isolar os departamentos de Financeiro e Suporte, garantindo segurança e controle de tráfego através de roteamento eficiente.

---

## Passo 1: Configuração de VLANs
Criei as VLANs 10 (FINANCEIRO) e 20 (SUPORTE) e associei as portas físicas do switch aos seus respectivos departamentos. 
* **Porta Fa0/1:** VLAN 10
* **Porta Fa0/11:** VLAN 20

![Criação das VLANs](print/01-configuracao-vlans.png)

---

## Passo 2: Teste de Isolamento (Segurança Layer 2)
Após a criação das VLANs, realizei um teste de ping entre as sub-redes. O teste falhou conforme o esperado, provando que os setores estavam logicamente isolados, mesmo compartilhando o mesmo hardware físico.

![Teste de Isolamento](print/02-teste-isolamento-vlan.png)

---

## Passo 3: Configuração de Trunking (802.1Q)
Para permitir que o tráfego de múltiplas VLANs trafegue por um único link físico em direção ao roteador, configurei as interfaces Gigabit como portas de Tronco (Trunk), utilizando o encapsulamento IEEE 802.1Q.

![Verificação de Trunking](print/03-verificao-trunking.png)

---

## Passo 4: Roteamento Inter-VLAN (Router-on-a-Stick)
Implementei sub-interfaces lógicas na interface GigabitEthernet0/0 do roteador. Cada sub-interface foi configurada com seu respectivo gateway e encapsulamento dot1Q para permitir a comunicação controlada entre as VLANs.

![Configuração Router-on-a-Stick](print/04-configuracao-router-on-a-stick.png)

---

## Passo 5: Validação Final de Conectividade
Com o roteamento configurado, realizei o teste final de conectividade. O ping entre os departamentos foi estabelecido com sucesso, validando que a rede possui segmentação de segurança e comunicação inteligente.

![Validação Final de Ping](print/05-validacao-final-ping.png)
