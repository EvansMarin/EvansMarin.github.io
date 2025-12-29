# Olá, sou Victor Marinho!

Sou estudante de Engenharia de Software e um entusiasta focado em Cibersegurança e Infraestrutura de Redes. Meu objetivo é aplicar conhecimentos teóricos em soluções práticas, sempre buscando entender o 'como' e o 'porquê' por trás de cada protocolo e camada de segurança.

Atualmente, dedico meu tempo ao desenvolvimento de laboratórios práticos (como este que você vê no meu portfólio), simulando cenários reais de infraestrutura para consolidar meus estudos para as certificações CompTIA Network+ e Security+.
---
## 🎓 Certificações e Conquistas

### 🛡️ Cibersegurança
* [**Fortinet Certified Fundamentals (FCF) - Cybersecurity**](https://www.credly.com/earner/earned/badge/05439bda-6a5d-40e8-bdff-1ff4daf17a23)
* [NSE 1: Getting Started in Cybersecurity 3.0](https://www.credly.com/earner/earned/badge/358bfae1-0e88-4dc3-aea3-0992a4f70bcf) (Fortinet)
* [NSE 2: Technical Introduction to Cybersecurity 3.0](https://www.credly.com/earner/earned/badge/dba43948-44f0-44ac-8175-229978883dc3) (Fortinet)
* [Cisco Network Defense](https://www.credly.com/earner/earned/badge/739b47ae-a961-44a6-b204-9739bcac93b6) 

### 🌐 Infraestrutura e Redes
* [Cisco Network Technician Career Path](https://www.credly.com/earner/earned/badge/51b47656-ba64-4c66-a309-938e52e4f2bd) 
* [Cisco Networking Academy Learn-A-Thon 2025](https://www.credly.com/earner/earned/badge/626cec39-cfbe-4676-bb8b-e0bbc326f1e1)





---
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



---

## Laboratório: Hardening e Segurança de Acesso Físico (Port Security)

Este laboratório focou na implementação de controles de segurança em Layer 2 para mitigar riscos de intrusão física e movimentação lateral em uma rede local (LAN).

### 1. Validação de Conectividade e Mapeamento (L2/L3)
Antes da aplicação de políticas de hardening, estabeleci a conectividade base e realizei a análise de identidade dos dispositivos através de protocolos ICMP e inspeção de tabelas.

* **Teste ICMP:** Validação de conectividade entre os hosts da topologia.
* **Análise de Identidade (ARP):** Mapeamento de IPs para endereços MAC.
* **Tabela CAM:** Verificação do aprendizado dinâmico do Switch.

![Teste de Ping](print/06-teste-conectividade-icmp.png)
![Tabela ARP](print/07-verificacao-tabela-arp.png)
![Tabela MAC Switch](print/08-inspecao-tabela-cam-switch.png)

### 2. Implementação de Port Security (Hardening)
Apliquei políticas restritivas na interface Fa0/1 para garantir que apenas o dispositivo autorizado tivesse acesso à rede.

* **Sticky MAC:** Configuração para persistência do endereço MAC legítimo.
* **Security Violation (Shutdown):** Definição de bloqueio total da porta e geração de logs em caso de tentativa de intrusão.

![Configuração Hardening](print/09-configuracao-port-security-hardening.png)
![Log de Erro de Violação](print/10-log-violacao-err-disabled.png)

### 3. Simulação de Incidente e Resposta a Incidentes
A etapa final validou a eficácia da política através da conexão de um dispositivo não autorizado.

* **Detecção de Intruso:** O Switch identificou a divergência e bloqueou a interface instantaneamente (cabos em estado de erro).
* **Intervenção Manual:** Demonstração da necessidade de auditoria e comandos `shutdown` / `no shutdown` para restaurar o serviço.
* **Recuperação:** Restabelecimento da conexão para o host legítimo após a limpeza do incidente.

![Intruso Bloqueado (Cabos Vermelhos)](print/11-incidente-intruso-bloqueado.png)
![Comandos de Recuperação CLI](print/12-recuperacao-servico-manual.png)
![Serviço Restaurado (Conexão Verde)](print/13-recuperacao-servico-manual.png)

---


# Infraestrutura de rede local segura

1. **Simulei uma rede do zero:** Montei uma topologia com roteador e switches para entender como o tráfego de uma empresa se comporta na prática.

![Topologia da Rede](print/14-topologia-infra-rede-segura.png)

2. **Configurei a segmentação da rede:** Criei as VLANs para o Financeiro e para o Suporte. Usei o protocolo VTP para não ter o trabalho manual de criar cada rede em cada switch, garantindo que todos ficassem sincronizados automaticamente.

![Segmentação VLAN e VTP](print/15-segmentacao-vlan-e-vtp.png)

3. **Aprendi a controlar o fluxo de dados:** Defini manualmente o Switch 1 como o "chefão" da rede (Root Bridge). Com isso, eu determinei o caminho principal que os dados devem seguir, evitando que a rede perdesse tempo em rotas ineficientes.

![Configuração Root Bridge STP](print/16-configuracao-root-bridge-stp.png)

4. **Configurei as "estradas" da rede:** Ativei os links como Trunk entre os switches. Aprendi que isso é fundamental para que todas as VLANs consigam conversar através de um único cabo físico.

![Verificação Trunking 802.1Q](print/17-verificacao-trunking-8021q.png)

5. **Testei a proteção contra intrusos:** Ativei o BPDU Guard para proteger a hierarquia que eu criei. Validei que, se alguém tentar plugar um switch não autorizado, a porta é desativada na hora para proteger a rede.

![Proteção BPDU Guard](print/18-protecao-hierarquia-bpdu-guard.png)

6. **Validei a comunicação entre setores:** Configurei o roteador para servir de ponte entre as VLANs. Testei e comprovei que um PC do Financeiro consegue falar com um PC do Suporte de forma segura, usando o comando ping para confirmar o sucesso.

![Validação Inter-VLAN Ping](print/19-validacao-intervlan-ping.png)

7. **Juntei forças com o EtherChannel:** Configurei o protocolo LACP para unir dois cabos físicos em um só canal lógico. Aprendi que isso dobra a velocidade e, se um cabo quebrar, o outro segura a bronca sem a rede cair.

![Verificação EtherChannel LACP](print/20-verificacao-etherchannel-lacp.png)

8. **Configurei a segurança das portas:** Ativei o Port-Security para que a porta do switch aprenda quem deve estar ali. Testei a função de "shutdown" e vi que ela bloqueia o acesso instantaneamente se um dispositivo estranho tentar se conectar.

![Verificação Port-Security](print/21-verificacao-port-security-infra.png)
