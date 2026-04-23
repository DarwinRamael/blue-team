# 🛡️ SOC Lab – SIEM com Wazuh + OPNsense (Blue Team Project)

Este projeto documenta a implementação de um **Security Operations Center (SOC) Lab**, com foco em **monitoramento contínuo, detecção de ameaças e resposta automatizada a incidentes**.

O ambiente foi projetado para simular cenários reais de defesa cibernética, permitindo a prática de conceitos fundamentais de **Blue Team**, incluindo SIEM, correlação de eventos e automação de respostas.

---

## 🎯 Objetivos do Projeto

* Implementar um ambiente SOC funcional
* Centralizar logs de múltiplas fontes
* Detectar atividades suspeitas em tempo real
* Automatizar respostas a incidentes
* Aplicar conceitos de **defesa em profundidade**

---

## 🧱 Arquitetura do Lab

O ambiente foi estruturado com os seguintes componentes:

* **Wazuh (SIEM/XDR)** → Monitoramento, análise e correlação de eventos
* **OPNsense (Firewall)** → Controle de tráfego e enforcement de regras
* **Endpoints monitorados** → Geração de eventos (logs de sistema)
* **Rede simulada** → Tráfego legítimo e potencialmente malicioso

[INSERIR IMAGEM: diagrama da arquitetura do SOC Lab]

---

## 🔍 Fase 1 – Implementação do SIEM

### 📊 Centralização de Logs

O Wazuh foi configurado para coletar e centralizar eventos provenientes de:

* Endpoints (logs de sistema)
* Firewall (OPNsense)
* Atividades de rede

➡️ **Objetivo:** Criar visibilidade unificada do ambiente

---

### 🔗 Correlação de Eventos

Foram configuradas regras para identificar padrões suspeitos, como:

* Tentativas de acesso repetidas (brute force)
* Conexões anômalas
* Atividades incomuns no sistema

➡️ **Insight:** A correlação permite transformar logs isolados em **alertas acionáveis**

---

## 🔥 Fase 2 – Monitoramento Contínuo

O ambiente foi projetado para operar em tempo real, permitindo:

* Detecção imediata de eventos suspeitos
* Geração automática de alertas
* Visualização centralizada via dashboard

[INSERIR IMAGEM: dashboard do Wazuh mostrando alertas]

---

## ⚡ Fase 3 – Resposta a Incidentes (Automação)

### 🤖 Automação Implementada

Foram criadas respostas automáticas para incidentes, incluindo:

* Bloqueio de IPs maliciosos no firewall
* Contenção de atividades suspeitas
* Redução do tempo de resposta

---

### 🔐 Exemplo de Fluxo Automatizado

1. Detecção de comportamento suspeito
2. Geração de alerta no SIEM
3. Trigger de regra automatizada
4. Bloqueio do IP no OPNsense

[INSERIR IMAGEM: fluxo de resposta automatizada]

➡️ **Resultado:** Mitigação rápida sem intervenção manual

---

## 📂 Fase 4 – Integração Wazuh + OPNsense

A integração permitiu:

* Aplicação de ações defensivas diretamente no firewall
* Resposta coordenada entre detecção e contenção
* Maior eficiência operacional

➡️ **Insight:** Integrações são fundamentais para um SOC moderno

---

## 📈 Resultados Obtidos

* Redução significativa no tempo de resposta a incidentes
* Maior visibilidade sobre o ambiente
* Detecção eficiente de atividades suspeitas
* Implementação prática de automação defensiva

---

## 🧠 Lições Aprendidas

* SIEM sem correlação gera excesso de ruído
* Automação é essencial para escalabilidade em segurança
* Firewalls podem ser usados ativamente na resposta, não apenas na prevenção
* Monitoramento contínuo é a base de qualquer SOC
* Defesa em profundidade aumenta significativamente a resiliência do ambiente

---

## 🛡️ Conceitos Aplicados

* Security Operations Center (SOC)
* SIEM (Security Information and Event Management)
* XDR (Extended Detection and Response)
* Threat Detection
* Incident Response
* Defense in Depth

---

## 📊 Diferenciais Técnicos Demonstrados

Este projeto evidencia:

* Capacidade de construção de ambiente SOC funcional
* Integração entre ferramentas de segurança
* Implementação de automação em resposta a incidentes
* Pensamento defensivo estruturado
* Conhecimento prático de operações de segurança

---

## 📌 Considerações Finais

Este lab representa uma implementação prática de um ambiente de defesa cibernética, com foco em:

✔ Monitoramento contínuo
✔ Detecção inteligente
✔ Resposta automatizada

A experiência adquirida demonstra habilidades aplicáveis a funções como:

* SOC Analyst
* Blue Team Engineer
* Cybersecurity Analyst

---

## 🔗 Referência

Confira o projeto completo:

[INSERIR LINK DO PROJETO AQUI]

---

## 📎 Observação

As imagens devem ser adicionadas nos pontos indicados para complementar a documentação visual e fortalecer a apresentação do projeto.

---

