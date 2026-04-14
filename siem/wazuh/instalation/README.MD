# 🛡️ Projeto Wazuh SIEM: O Coração do meu SOC (Instalação e Setup)

## 📖 O que é o Wazuh?
O Wazuh é uma plataforma de segurança que unifica capacidades de **XDR** (Extended Detection and Response) e **SIEM** (Security Information and Event Management). 

Ele é o "Analista de Inteligência" do meu laboratório. Ele coleta logs de tudo, analisa ameaças e me dá um dashboard centralizado para saber quem está tentando "forçar a fechadura" dos meus servidores.

### 🏗️ Ambiente do Projeto
* **Hypervisor:** Proxmox VE.
* **Sistema Operacional:** Ubuntu Server 24.04 LTS (ou mais recente).
* **Objetivo:** Instalação limpa, rede estática "na veia" e prontidão para monitoramento.

---

## 🛠️ Passo 1: O "Setup Perfeito" (Instalação do Ubuntu)

Para evitar dores de cabeça com configurações manuais de rede depois, a estratégia foi definir tudo no instalador do Ubuntu (**Subiquity**).

* **Configuração de IP Estático:** * Na tela de rede, não aceite o DHCP (que é o "endereço nômade"). 
    * Entre nas configurações da interface, mude para **Manual (IPv4)** e defina seu IP fixo (ex: `192.168.1.50/24`), Gateway e DNS.
    * **Por que?** Porque se o SIEM mudar de IP, os agentes ficam perdidos e você perde a visibilidade da rede. Definir na instalação garante que o sistema já nasce com "domicílio fixo".
* **Ativação do SSH (Obrigatório!):** * Marque a opção **"Install OpenSSH Server"**. 
    * **Por que?** Porque ninguém merece digitar comandos quilométricos diretamente no console do Proxmox. Com o SSH, fazemos tudo via terminal (ou PuTTY/Termius), com o poder do famoso `Ctrl+C / Ctrl+V`.

> *(Imagem: Tela do instalador do Ubuntu com o IP Manual configurado e o checkbox do OpenSSH marcado)*

---

## 📥 Passo 2: O Ritual de Instalação do Wazuh

Com o sistema instalado e o SSH ativo, acessei a máquina remotamente. Agora, o comando de instalação automática faz o trabalho pesado de subir o Indexer, o Server e o Dashboard.

* **O Comando de Instalação:**
  ```bash
  curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash wazuh-install.sh -a
  ```
* **Dica de sobrevivência:** Esse processo demora uns 5 a 10 minutos. É o tempo de pegar um café e torcer para a luz não cair.
* **Gestão de Credenciais:** Ao final, o instalador gera uma senha para o usuário `admin`. **Anote isso como se fosse sua senha do banco.** Se perder, você vai descobrir que recuperar o acesso ao Wazuh é um excelente exercício de paciência (que ninguém quer fazer).

> *(Imagem: Terminal via SSH mostrando a barra de progresso da instalação e as credenciais finais sendo exibidas)*

---

## 🚀 Passo 3: Inicialização e Verificação

O script geralmente já sobe os serviços, mas como profissionais de segurança, nós **sempre** conferimos.

* **Comandos de Verificação:**
  ```bash
  sudo systemctl status wazuh-manager
  sudo systemctl status wazuh-indexer
  sudo systemctl status wazuh-dashboard
  ```
* **O que não fazer:** Tentar logar na WebGUI 1 segundo depois do comando acabar. O Dashboard é pesado e leva um tempinho para "acordar". Respire fundo.

---

## 🌐 Passo 4: O Painel de Controle (Web Login)

Agora a recompensa!

* **Acesso:** No navegador, digite `https://[SEU-IP-ESTATICO]`.
* **Segurança:** O certificado é auto-assinado (o navegador vai reclamar). Clique em "Avançado" e "Aceitar o risco". Afinal, o laboratório é seu e você confia em você mesmo (eu espero).
* **Login:** Use as credenciais que você salvou no Passo 2.

> *(Imagem: Tela de Login do Wazuh Dashboard e a imagem do painel carregado com as estatísticas em zero - por enquanto!)*

---

## ✅ Conclusão
O **Wazuh Server** está operacional! Temos agora uma base sólida e, o melhor de tudo, uma máquina com IP fixo que não vai se perder na rede e acesso SSH para futuras manutenções sem estresse.

**Próximos Passos:** Nos próximos capítulos desta saga, vamos espalhar os **Agentes** do Wazuh pelo Windows, Linux e pfSense para que o Dashboard comece a mostrar a movimentação real da rede!

---
**Curtiu a documentação?** Me siga para ver o próximo passo: **Integração de Agentes e Dashboards Personalizados.**
