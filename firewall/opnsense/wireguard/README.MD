# 🛸 Operação "Portal de Sombra": VPN de Alta Performance com WireGuard & OPNsense

## 📖 Por que este projeto existe?

Acessar o Home Lab de fora é essencial, mas abrir portas para RDP ou SSH na internet é como deixar a chave da mansão pendurada na fechadura. VPNs antigas são pesadas e lentas. Eu queria algo que fosse **instantâneo, moderno e invisível**.

Este projeto documenta a implementação do **WireGuard** no OPNsense. Saímos da era das conexões instáveis para um túnel de criptografia de ponta que só responde a quem tem a chave. Se você não é convidado, meu firewall nem sequer admite que existe.

### 🏗️ A "Ponte de Comando" (Hardware & Topologia)

* **O Protocolo:** WireGuard (rodando direto no Kernel para não ter gargalo).
* **O Setup:** Smartphone/Laptop (O Viajante) ➡️ Internet ➡️ **OPNsense (O Portal)** ➡️ Rede Interna/SOC Lab.
* **O Diferencial:** O WireGuard não usa o protocolo de "aperto de mão" barulhento das outras VPNs. Ele é silencioso. Se o pacote não estiver assinado corretamente, ele é descartado sem resposta. Modo fantasma ativado.

---

## 🛠️ Passo 1: O Segredo de Estado (Instância Local)

No WireGuard, não existe "usuário e senha". Tudo é baseado em chaves criptográficas.

* **O que fazer:** Criar a instância local no OPNsense e gerar o par de chaves (Pública/Privada).
* **Por que:** A chave privada nunca sai do seu firewall. É ela que garante que ninguém consiga fingir ser o seu servidor.
* **Dica de mestre:** Escolha uma porta UDP alta e aleatória (ex: `55820`) para fugir dos scripts automáticos que varrem a porta padrão.

> *(Imagem: Configuração da instância local do WireGuard com as chaves geradas)*

---

## 🌐 Passo 2: O Aperto de Mão (Configurando o Peer)

O "Peer" é qualquer dispositivo que terá permissão para atravessar o portal.

* **O que fazer:** Adicionar a chave pública do seu celular ou notebook ao OPNsense.
* **Allowed IPs:** Aqui é onde o Analista define o escopo. Usei `0.0.0.0/0` para o "Full Tunnel" — ou seja, até quando estou no Wi-Fi público, meu tráfego vai para casa, é filtrado pelo firewall e só depois sai para a internet.
* **Endpoint:** O endereço (IP ou DDNS) que o mundo vê da sua casa.

> *(Imagem: Aba de Peers mostrando o celular configurado e pronto para o combate)*

---

## 🔒 Passo 3: O Segurança na Porta (Regras de Firewall)

Ter o túnel não significa que a rede está aberta. O firewall continua sendo o juiz.

1.  **Regra na WAN:** Abrir a porta UDP específica para o WireGuard entrar.
2.  **Regra na Interface WG:** Aqui aplicamos o **Privilégio Mínimo**. Criei regras para o túnel acessar apenas o servidor do Proxmox e o DNS, bloqueando o acesso direto à rede de gerenciamento do modem.
3.  **MSS Clamping:** Ajuste fino para garantir que os pacotes não quebrem no meio do caminho devido ao tamanho do cabeçalho da VPN.

> *(Imagem: Regras de firewall na interface WireGuard limitando o tráfego aos alvos necessários)*

---

## 📱 Passo 4: O Atalho Mágico (QR Code)

A conveniência não precisa sacrificar a segurança. O OPNsense facilita a vida do administrador.

* **Ação:** Gerar o QR Code de configuração.
* **O Teste:** Abrir o app no celular, escanear e clicar em "Ativar".
* **Resultado:** A conexão é tão rápida que parece que você já estava na rede local. O acesso aos dashboards internos agora está na palma da mão, em qualquer lugar.

> *(Imagem: Tela de geração de QR Code para facilitar a vida do Road Warrior)*

---

## ✅ Validação Final (A prova dos 9)

Para garantir que o túnel não é "furado", os seguintes testes foram feitos:

1.  **Handshake Status:** Verificado no dashboard que a troca de chaves ocorre em milissegundos.
2.  **IP Check:** Verificado que, mesmo no 5G, meu IP externo é o da minha casa.
3.  **DNS Seguro:** Confirmado que as consultas de DNS estão sendo feitas pelo meu servidor interno (Unbound), bloqueando anúncios no celular.

> *(Imagem: Dashboard de Status do WireGuard mostrando o túnel ativo e tráfego fluindo)*

---

## 🚀 Conclusão

Este projeto transformou meu acesso remoto de algo "arriscado" para algo "blindado". Agora, gerenciar o SOC Lab de um café ou da rua é tão seguro quanto estar sentado na frente do servidor. Rapidez, simplicidade e segurança de verdade.

---

**Curtiu esse túnel?** Conecte-se comigo no [LinkedIn](https://www.linkedin.com/in/tecdarwin/) para trocarmos uma ideia sobre defesa de rede!
