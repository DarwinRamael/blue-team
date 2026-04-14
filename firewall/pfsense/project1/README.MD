Com certeza\! Vamos dar uma "vitaminada" nesse texto. O objetivo é mostrar que você domina o assunto a ponto de conseguir explicar com leveza, sem perder a autoridade técnica. Recrutadores adoram ver alguém que tem **"paranóia saudável"** (essencial em segurança) e paixão pelo que faz.

Aqui está a versão dinâmica e técnica para o seu GitHub:

-----

# 🛡️ Operação "Bye-Bye ISP": Firewall de Borda com pfSense & Suricata

## 📖 Por que este projeto existe?

Sabe aquele roteador padrão que a operadora instala e que você mal consegue mudar a senha sem ele travar? Pois é. Decidi que era hora de tirar as chaves do meu castelo das mãos de terceiros.

Este projeto documenta a transformação de um hardware de baixo consumo em um **firewall de nível empresarial**. Aqui, não aceitamos "configuração padrão". Aplicamos o conceito de **Defesa em Profundidade**, transformando uma rede comum em uma fortaleza digital monitorada em tempo real.

### 🏗️ A "Battle Station" (Hardware & Topologia)

  * **O Cérebro:** PC Low Power com 2 interfaces Gigabit (porque latência é o inimigo).
  * **O Setup:** Modem da Operadora (no "cantinho do castigo" em modo Bridge) ➡️ **pfSense (O General)** ➡️ Switch ➡️ Minha Rede.
  * **O Diferencial:** Com o modem em Bridge, o pfSense assume o IP público. Ou seja: eu mando na borda, eu filtro os pacotes e eu decido quem entra na festa.

-----

## 🛠️ Passo 1: O Batismo (Console)

A primeira etapa é dizer ao pfSense quem é quem na fila do pão.

  * **O que fazer:** Atribuir as interfaces. `WAN` olha para a internet (o caos), `LAN` olha para a minha casa (o porto seguro).
  * **Por que:** Errar aqui é como colocar a porta da frente da sua casa nos fundos.
  * **Dica de mestre:** Identifique fisicamente os cabos antes de começar, ou você vai passar 20 minutos trocando cabos e se perguntando por que o DHCP não sobe.

> *(Imagem: Tela do console do pfSense com as interfaces devidamente batizadas)*

-----

## 🌐 Passo 2: O Wizard (Configuração Inicial)

Aqui é onde a mágica (e a segurança) começa.

### Tela: General Information

  * **Configuração:** DNS da Cloudflare (`1.1.1.1`) ou Quad9 (`9.9.9.9`).
  * **Por que:** Porque privacidade importa. Não precisamos que o ISP saiba cada site que visitamos.

### Tela: Configure WAN Interface

  * **Configuração:** Marcar **"Block RFC1918"** e **"Block Bogon Networks"**.
  * **O que isso faz:** Bloqueia tráfego que não deveria existir na internet pública. Se um IP privado tentar bater na minha WAN, o pfSense nem abre a porta para perguntar quem é. É o famoso "nem vem que não tem".

> *(Imagem: O pfSense colocando os IPs maliciosos para correr na configuração de WAN)*

-----

## 🔒 Passo 3: Hardening (Deixando o General "Cascudo")

Segurança por obscuridade não é tudo, mas ajuda a dormir melhor.

  * **Ação:** Mudei a porta da WebGUI de 443 para algo aleatório (ex: `8443`) e forcei o HTTPS.
  * **O que NÃO fazer:** Deixar o usuário `admin` com a senha `pfsense`. Se você fizer isso, um hacker estagiário ganha acesso ao seu roteador em 30 segundos.
  * **Como validar:** Tente acessar o IP do firewall pela porta 80. Se ele te der um "gelo" (timeout), parabéns\! Você não está mais gritando para a rede quem você é.

> *(Imagem: Configurações de System Advanced: HTTPS é obrigatório aqui\!)*

-----

## 🕵️ Passo 4: Suricata - O Cão de Guarda (IDS/IPS)

O firewall barra a entrada, mas o **Suricata** analisa as intenções. Ele faz a inspeção profunda de pacotes (DPI).

1.  **Instalação:** Via Package Manager. É como instalar um módulo de inteligência no seu General.
2.  **Regras:** Ativei as listas **Emerging Threats** e **Snort VRT**.
3.  **IDS vs IPS:** Começamos no modo **IDS** (Detecção).
      * *Por que?* Porque não queremos que o firewall bloqueie o Netflix da família achando que é um ataque hacker (falso positivo = dor de cabeça). Depois de calibrado, passamos para o modo **IPS** (Bloqueio Ativo).
4.  **Teste de Fogo:** Usei o `testmyids.com` para simular uma atividade suspeita.
      * **Resultado:** O Suricata detectou a assinatura e gerou um alerta instantâneo. "Não no meu turno\!"

> *(Imagem: Aba de Alerts do Suricata mostrando o bloqueio de uma assinatura de ataque)*

-----

## ✅ Validação Final (A prova dos 9)

Para garantir que não é só "perfumaria", fiz os seguintes testes:

1.  **Leak Test:** Verificado que meu DNS não está vazando dados.
2.  **Port Scan Externo:** Fiz um scan de portas de fora para dentro. Resultado? "Stealth". O firewall simplesmente ignora as tentativas de conexão.
3.  **Logs de Guerra:** Mostro abaixo os IPs da Rússia, China e outros lugares tentando "forçar a maçaneta" da minha rede e sendo bloqueados silenciosamente pelo pfSense.

> *(Imagem: Dashboard final - Tudo verde, tráfego fluindo e ataques sendo bloqueados)*

-----

## 🚀 Conclusão

Este projeto prova que com hardware reciclado e software certo, você pode ter segurança de nível bancário em casa. Saí do "espero que ninguém me ataque" para o "eu sei exatamente quem tentou e por que falhou".

-----

**Curtiu o projeto?** Conecte-se comigo no [LinkedIn](https://www.google.com/search?q=SEU_LINK_AQUI) para trocarmos uma ideia sobre Cyber e Infra\!
