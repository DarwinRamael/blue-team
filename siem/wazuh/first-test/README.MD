# 🚀 Projeto Wazuh #01: Implementação de Agentes e Visibilidade de Endpoints

## 📖 Visão Geral
Este é o projeto inicial de monitoramento utilizando o **Wazuh**. Após a instalação do servidor, o foco agora é estabelecer a comunicação entre os ativos da rede e o SIEM através da instalação de agentes. Um SIEM sem agentes é apenas um dashboard vazio; com este projeto, habilitamos a telemetria proativa.

### 🎯 Objetivos
1.  Realizar o deploy do primeiro agente (Windows ou Linux).
2.  Estabelecer conexão segura via chave de autenticação.
3.  Validar o recebimento de eventos de segurança (Logon/Logoff).
4.  Realizar um inventário inicial de hardware e software do ativo.

---

## 🛠️ Passo 1: Deploy do Agente (Via Interface Web)

O Wazuh facilita muito o deploy através de um assistente que gera o comando de instalação pronto.

* **Como chegar:** No Dashboard do Wazuh > **Wazuh** > **Agents** > **Deploy new agent**.
* **O que fazer:**
    1.  Selecione o Sistema Operacional (ex: Windows).
    2.  Insira o **IP Estático** do seu servidor Wazuh (que configuramos no projeto anterior).
    3.  Defina um nome para o agente (ex: `PC-ADMIN-DESKTOP`).
* **Comando gerado:** O Wazuh vai te dar um comando em PowerShell (para Windows) ou Bash (para Linux). 
* **Dica de mestre:** Execute o comando como **Administrador/Root**. O agente precisa de altos privilégios para ler logs do sistema e arquivos críticos.

> *(Imagem: Tela do assistente 'Deploy new agent' mostrando as opções preenchidas)*

---

## 🔑 Passo 2: Registro e Ativação

Após rodar o comando, o agente precisa "se apresentar" ao servidor.

* **O que fazer:** Após instalar, inicie o serviço do agente.
    * No Windows: `Start-Service -Name Wazuh`
    * No Linux: `systemctl start wazuh-agent`
* **O que NÃO fazer:** Esquecer de abrir a porta **1514 (UDP/TCP)** no firewall do seu Ubuntu (se o UFW estiver ativo). Essa é a porta que os agentes usam para enviar os logs.
* **Validação:** Volte ao painel do Wazuh. O status do agente deve mudar de `Never connected` para `Active`.

> *(Imagem: Dashboard do Wazuh mostrando o primeiro agente com a bolinha verde 'Active')*

---

## 📊 Passo 3: Exploração de Dados (Inventário e Segurança)

Agora que o agente está enviando dados, vamos ver o que o Wazuh descobriu sobre ele.

* **Inventory Data (SCA):** Clique no agente e vá em **Inventory**. Aqui você verá todas as portas abertas, programas instalados e interfaces de rede.
* **Segurança Baseada em Configuração:** Vá em **Security Configuration Assessment (SCA)**. O Wazuh vai te dar uma nota de 0 a 100 baseada em quão "segura" está a configuração do seu SO. 
    * *Exemplo:* Ele vai te avisar se o firewall do Windows está desligado ou se há usuários sem senha.

> *(Imagem: Tela de SCA mostrando as falhas de configuração encontradas no agente recém-instalado)*

---

## 🛡️ Passo 4: O Primeiro Teste de Alerta (Logon)

Vamos provar que o SIEM está vigiando.

1.  No computador onde o agente está instalado, faça um **Logoff** e depois um **Logon**.
2.  Vá no painel do Wazuh em **Security Events**.
3.  Filtre pelo ID do agente.
4.  **Resultado:** Você verá o evento de "Windows Logon Success" (Event ID 4624) registrado no SIEM.

---

## ✅ Conclusão
Este projeto marca o início da **Observabilidade de Segurança** no laboratório. Agora, qualquer movimentação suspeita no computador monitorado será reportada centralizadamente ao Wazuh.

**Próximos Passos:** Nos próximos projetos, vamos configurar o **FIM (File Integrity Monitoring)** para detectar se alguém alterou um arquivo importante e o **Vulnerability Detection** para saber quais patches de segurança estão faltando nesse agente.

---
