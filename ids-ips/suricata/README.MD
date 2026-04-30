
# 👁️ Projeto Suricata: Deixando a Rede Inteligente

## 📖 O que é este projeto?
O objetivo aqui não é apenas "instalar o Suricata", mas sim **doutriná-lo**. Vamos configurar regras personalizadas, testar assinaturas de ataques comuns e entender como ele transita de um simples observador (IDS) para um executor impiedoso (IPS).

### 🛠️ O que vamos testar:
1.  **Detecção de ICMP (O famoso "Ping da Morte").**
2.  **Mapeamento de Nmap (O "Xeretando a Porta").**
3.  **Bloqueio de User-Agent (Barreando ferramentas específicas).**

---

## 🛠️ Passo 1: O Cérebro do Suricata (Regras e Assinaturas)

O Suricata funciona à base de regras. Elas seguem uma lógica: `Ação | Protocolo | Origem | Porta -> Destino | Porta | (Opções)`.

* **Configuração Inicial:** No pfSense, vá em **Services > Suricata > Global Settings**.
* **O que fazer:** Ative o **Emerging Threats Open**. É a lista "pão com manteiga" da segurança, atualizada diariamente com novos malwares.
* **A "Pitada" Técnica:** No Proxmox, certifique-se de que a placa de rede da VM do pfSense está em modo promíscuo ou que o Suricata está monitorando a interface correta (`WAN` ou `LAN`).

> *(Imagem: Tela de Global Settings com os Rulesets ativos e atualizados)*

---

## 🔬 Passo 2: Laboratório de Testes (Mãos na Massa)

Para testar, criei regras customizadas em **Suricata > Interfaces > [Sua Interface] > Rules**. No dropdown, selecione **Custom Rules**.

### Teste 1: O Alerta de ICMP (O "Oi, você tá aí?")
**Regra:** `alert icmp any any -> $HOME_NET any (msg:"ALERTA: Ping Detectado - Possível Reconhecimento"; sid:1000001; rev:1;)`

* **O que faz:** Toda vez que alguém pingar minha rede, o Suricata grita.
* **Como testar:** De uma máquina externa (ou do seu terminal), dê um `ping [IP-DO-FIREWALL]`.
* **O que validar:** Vá na aba **Alerts**. Você verá o evento registrado com a mensagem que criamos.

> *(Imagem: Aba de Alerts mostrando a regra 1000001 disparando loucamente)*

---

### Teste 2: Detectando Nmap (O "Xereta")
Atacantes usam o Nmap para ver quais portas você tem abertas. O Suricata já tem regras para isso, mas vamos garantir que elas estão funcionando.

* **O que fazer:** Ative as regras de `scanners.rules`. 
* **Como testar:** Use o comando `nmap -sS -A [IP-DO-FIREWALL]`.
* **A análise:** O Suricata vai detectar o "TCP Stealth Scan". Para ele, isso é comportamento de quem está forçando a maçaneta da porta.

> *(Imagem: Alertas de "ET SCAN Nmap" aparecendo no log)*

---

### Teste 3: Bloqueio de User-Agent (O "Aqui você não entra")
Vamos supor que você não quer que ninguém use o navegador "Curl" ou uma ferramenta de automação para acessar seu servidor.

**Regra:** `drop tcp any any -> $HOME_NET 80 (msg:"Bloqueio: Tentativa de acesso via CURL detectada"; content:"User-Agent|3a| curl"; http_header; sid:1000002; rev:1;)`

* **A sacada:** Note que usamos a ação **DROP**. Para isso funcionar, o Suricata deve estar em modo **IPS**.
* **Como validar:** Tente acessar seu servidor via terminal com `curl http://[IP]`. A conexão deve simplesmente "morrer" no meio do caminho.

---

## 🚫 Passo 3: O Modo IPS (O Bouncer Ativo)

Aqui é onde o filho chora e a mãe não vê. No modo **IDS**, o Suricata apenas anota a placa do carro. No modo **IPS**, ele joga o tapete de pregos.

* **Configuração:** Em **Suricata > Interface Settings**, mude o **IPS Mode** para `Legacy Mode` (mais compatível) ou `Inline Mode` (mais rápido, mas exige placas que suportem Netmap).
* **O que NÃO fazer:** Não ative todas as regras do mundo em modo DROP de uma vez. Você vai bloquear até a atualização do Windows e seu próprio acesso. **Vá com calma.**
* **Como testar o bloqueio:** Vá na aba **Blocks**. Se o IP da sua máquina de teste estiver lá, parabéns: você foi banido da sua própria rede (sucesso técnico!).

> *(Imagem: Aba de 'Blocks' com IPs listados e o motivo do banimento)*

---

## 📊 Passo 4: Visibilidade e Logs

Recrutador adora ver que você sabe ler logs, não apenas apertar botões.

* **Onde olhar:** `/var/log/suricata/` (via SSH) ou a aba **Alerts** na WebGUI.
* **Dica técnica:** Explique no seu GitHub que o Suricata gera arquivos `eve.json`. Esse arquivo é o "ouro" que o **Wazuh** (nosso próximo projeto) vai ler para criar gráficos bonitões e alertas por e-mail.

---

## ✅ Conclusão do Lab
O Suricata não é uma ferramenta de "instalar e esquecer". É um organismo vivo. Neste projeto, provei que consigo:
1.  Escrever assinaturas de detecção manuais.
2.  Diferenciar tráfego legítimo de escaneamento malicioso.
3.  Configurar uma barreira ativa que corta a conexão antes mesmo do atacante ver o que tem dentro da rede.

**Próxima parada:** Integrar tudo isso no **Wazuh** para centralizar esses alertas e ter um verdadeiro **SOC (Security Operations Center)** em casa!

---
