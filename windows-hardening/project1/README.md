# Projeto de Hardening: Implementação de Controles ISO 27001 em Estações de Trabalho

## 🛡️ Sobre o Projeto
Este repositório documenta a aplicação prática de controles de segurança da norma **ISO 27001 (Anexo A)** em um ambiente Windows 10/11, utilizando apenas recursos nativos do sistema operacional. O objetivo é demonstrar a redução da superfície de ataque através do endurecimento (Hardening) das configurações de fábrica.

---

## 📋 Checklist de Implementação

### 1. Políticas de Conta e Senhas (Controle A.9.4.3)
**Objetivo:** Impedir ataques de força bruta e garantir que as senhas sejam robustas.

* **Como chegar:** Iniciar > Digite `secpol.msc` > Configurações de Segurança > Políticas de Conta > Política de Senha.
* **O que fazer:**
    * **Exigir histórico de senhas:** Definir para 5 senhas lembradas.
    * **Tempo de vida máximo da senha:** 90 dias.
    * **Comprimento mínimo da senha:** 12 caracteres.
    * **Criptografia reversível:** Desabilitado.
* **O que NÃO fazer:** Não definir um tempo de vida mínimo muito curto, pois isso irrita o usuário e gera chamados de suporte desnecessários.
* **Como validar:** Tente alterar sua senha para uma senha simples (ex: 123) e verifique se o Windows recusa a alteração.

> *(Imagem: Tela de Configuração de Políticas de Senha no secpol.msc)*

---

### 2. Bloqueio de Conta (Mitigação de Brute Force)
**Objetivo:** Travar a conta caso alguém tente adivinhar a senha repetidamente.

* **Como chegar:** No mesmo `secpol.msc` > Políticas de Conta > Política de Bloqueio de Conta.
* **O que fazer:**
    * **Limiar de bloqueio de conta:** 5 tentativas inválidas.
    * **Duração do bloqueio:** 30 minutos.
* **Como validar:** Tente errar a senha 5 vezes na tela de bloqueio e veja se o sistema impede novas tentativas pelo tempo determinado.

> *(Imagem: Tela de Política de Bloqueio de Conta)*

---

### 3. Redução de Serviços e Protocolos Inseguros (Controle A.12.1.2)
**Objetivo:** Desativar portas e serviços que não são mais necessários e podem ser explorados (ex: SMBv1).

* **Como chegar:** Painel de Controle > Programas > Ativar ou Desativar Recursos do Windows.
* **O que fazer:**
    * Desmarcar **"Suporte para Compartilhamento de Arquivos SMB 1.0/CIFS"**.
    * Desmarcar serviços de impressão se não for utilizar.
* **O que NÃO fazer:** Não desativar recursos sem antes testar se alguma aplicação legada da empresa ainda depende deles.
* **Como validar:** Abra o PowerShell como Administrador e digite `Get-SmbServerConfiguration`. Verifique se `EnableSMB1Protocol` está como `False`.

> *(Imagem: Janela de Recursos do Windows com SMBv1 desmarcado)*

---

### 4. Gerenciamento de Privilégios (Princípio do Menor Privilégio - A.9.2)
**Objetivo:** Garantir que o usuário no dia a dia não use conta de Administrador.

* **Como chegar:** Configurações > Contas > Outros Usuários.
* **O que fazer:** Criar uma conta padrão para o uso diário e manter a conta de Administrador protegida e usada apenas para instalações.
* **Como validar:** Tente instalar um software com a conta padrão; o sistema deve solicitar a senha de administrador (UAC).

> *(Imagem: Painel de Gerenciamento de Usuários mostrando a conta Padrão)*

---

### 5. Configuração de Auditoria de Eventos (Controle A.12.4.1)
**Objetivo:** Gerar rastros (logs) para saber quem fez o quê no sistema.

* **Como chegar:** `secpol.msc` > Configurações Locais > Política de Auditoria.
* **O que fazer:**
    * **Auditar eventos de logon:** Sucesso e Falha.
    * **Auditar acesso a objetos:** Sucesso e Falha.
    * **Auditar gerenciamento de contas:** Sucesso.
* **Como validar:** Abra o **Visualizador de Eventos** (Event Viewer) > Logs do Windows > Segurança. Procure pelo Event ID 4624 (Logon com sucesso).

> *(Imagem: Visualizador de Eventos mostrando logs de auditoria de segurança)*

---

### 6. Criptografia de Dados em Repouso (Controle A.18.1.5)
**Objetivo:** Proteger os arquivos em caso de furto do equipamento.

* **Como chegar:** Iniciar > Digite "Gerenciar BitLocker".
* **O que fazer:** Ativar o BitLocker na unidade C:. Salve a chave de recuperação em um local seguro (não no próprio PC).
* **O que NÃO fazer:** Perder a chave de recuperação. Sem ela, os dados são irrecuperáveis.
* **Como validar:** Verifique o ícone do seu disco rígido no "Este Computador"; ele deve exibir um cadeado.

> *(Imagem: Painel do BitLocker com o status "Ativado")*

---

## 🚀 Conclusão
A aplicação dessas medidas reduz drasticamente a superfície de ataque de uma estação de trabalho. Como profissional de infraestrutura com foco em segurança, entendo que o Hardening é um processo contínuo e deve ser revisado periodicamente conforme novas ameaças surgem.

---
**Contato:**
[Darwin Ramael]
[www.linkedin.com/in/tecdarwin]
