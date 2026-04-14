# 🏗️ Projeto Proxmox VE: A Fundação do meu Lab de Segurança

## 📖 O que é isso e por que não usar o VirtualBox?
Instalar o Proxmox VE (Virtual Environment) em uma máquina dedicada significa sair da "camada de aplicação" e ir direto para o **Tipo 1 Hypervisor**. Aqui não tem sistema operacional de hospedeiro roubando recursos; o Proxmox roda direto no hardware (**Bare Metal**). 

Este é o primeiro passo para criar um ecossistema de servidores isolados, permitindo que eu suba um SOC (Security Operations Center) completo, incluindo o **Wazuh**, sem fritar meu computador de uso pessoal.

### 💻 Hardware do Lab
* **Máquina:** [Insira aqui o modelo ou specs simples, ex: Mini PC / Desktop Dedicado].
* **Objetivo:** Virtualizar instâncias Linux/Windows, containers LXC e, futuramente, meu nó de monitoramento SIEM.

---

## 🛠️ Passo 1: O "Flash" no Metal (Instalação)

A instalação do Proxmox é direta, mas exige atenção aos detalhes de disco.

* **O que fazer:** Gravei a ISO em um pendrive (Ventoy/Rufus) e dei boot. Durante a instalação, selecionei o disco principal e o sistema de arquivos (usei **ext4** ou **ZFS**, dependendo da sua escolha - *ZFS é ótimo para snapshots!*).
* **Configuração de Rede:** Defini um IP Estático para o Proxmox. 
    * *Dica de Ouro:* Nunca deixe um servidor de infraestrutura em DHCP. Se o IP mudar, você perde o acesso a tudo.
* **O que NÃO fazer:** Escolher uma senha de root fraca. Lembre-se: quem manda no Proxmox, manda em todas as máquinas virtuais dentro dele.

> *(Imagem: Tela de sumário da instalação do Proxmox confirmando o IP e o Disco)*

---

## 🌐 Passo 2: Acesso à WebGUI (Onde a mágica acontece)

Depois do reboot, o "General" Proxmox nos dá as boas-vindas com uma tela preta e uma URL.

* **Como chegar:** Acessei via navegador em `https://[IP-DO-PROXMOX]:8006`.
* **O erro comum:** O navegador vai reclamar do certificado SSL (é um certificado auto-assinado). Clique em "Avançado" e "Prosseguir". Não entre em pânico, isso é normal em labs locais.
* **Login:** Usuário `root` e a senha forte que definimos no passo anterior.

> *(Imagem: Tela de login do Proxmox - O portal para o seu novo império digital)*

---

## 🛡️ Passo 3: Configurações Iniciais e "Hardening" Básico

Mesmo sendo um laboratório, tratamos como produção. 

### 1. Repositórios "No-Subscription"
Como estamos usando a versão gratuita, precisamos ajustar os repositórios para receber atualizações sem a licença paga.
* **O que fazer:** Vá em `Updates > Repositories`, desative o "Enterprise" e adicione o "No-Subscription".
* **Por que:** Manter o sistema atualizado é a regra nº 1 da segurança.

### 2. A Ponte de Rede (Linux Bridge)
Configurei o `vmbr0`. É através dessa ponte que minhas futuras VMs (como o Wazuh) vão conversar com o pfSense e com a internet.
* **Conceito Técnico:** Entender o mapeamento de portas físicas para bridges virtuais é essencial para não criar "buracos" na rede.

> *(Imagem: Painel de Network do Proxmox mostrando a Linux Bridge ativa)*

### 3. Upload de ISOs (O estoque de armas)
Ninguém cria servidor sem imagem. Já fiz o upload das ISOs do **Ubuntu Server** (para o Wazuh) e **Windows Server**.
* **Como chegar:** `local (pve) > ISO Images > Upload`.

---

## 🚀 O Próximo Passo: Rumo ao Wazuh
O Proxmox já está "em pé", estável e configurado. Agora tenho o ambiente perfeito para subir meu **Wazuh**. 
A ideia é ter um container ou VM dedicada para coletar logs, analisar eventos e me dar aquela visão de "Matrix" sobre tudo o que acontece na minha rede.

---

## ✅ Validação de Sucesso
1.  **Acesso Remoto:** Consigo gerenciar o hardware de qualquer lugar da minha rede local via HTTPS.
2.  **Snapshot Test:** Criei uma VM de teste e tirei um Snapshot. Se eu quebrar algo no futuro (e eu vou), volto no tempo em segundos. **Isso é o paraíso da administração de sistemas.**
