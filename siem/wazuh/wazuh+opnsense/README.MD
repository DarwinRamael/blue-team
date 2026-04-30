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

<div align="center">

<svg width="700" height="400" viewBox="0 0 700 400" xmlns="http://www.w3.org/2000/svg">

  <!-- Endpoints -->
  <rect x="50" y="150" width="120" height="60" rx="10" fill="#2d3748"/>
  <text x="110" y="185" text-anchor="middle" fill="white" font-size="12">
    Endpoints
  </text>
  <text x="110" y="200" text-anchor="middle" fill="white" font-size="10">
    Logs / Eventos
  </text>

  <!-- Network -->
  <rect x="220" y="150" width="120" height="60" rx="10" fill="#4a5568"/>
  <text x="280" y="185" text-anchor="middle" fill="white" font-size="12">
    Rede Simulada
  </text>
  <text x="280" y="200" text-anchor="middle" fill="white" font-size="10">
    Tráfego
  </text>

  <!-- OPNsense -->
  <rect x="390" y="150" width="120" height="60" rx="10" fill="#dd6b20"/>
  <text x="450" y="180" text-anchor="middle" fill="white" font-size="12">
    OPNsense
  </text>
  <text x="450" y="200" text-anchor="middle" fill="white" font-size="10">
    Firewall
  </text>

  <!-- Wazuh -->
  <rect x="550" y="100" width="120" height="80" rx="10" fill="#2b6cb0"/>
  <text x="610" y="140" text-anchor="middle" fill="white" font-size="12">
    Wazuh
  </text>
  <text x="610" y="160" text-anchor="middle" fill="white" font-size="10">
    SIEM / XDR
  </text>

  <!-- Arrows -->
  <line x1="170" y1="180" x2="220" y2="180" stroke="black" stroke-width="2" marker-end="url(#arrow)" />
  <line x1="340" y1="180" x2="390" y2="180" stroke="black" stroke-width="2" marker-end="url(#arrow)" />
  <line x1="510" y1="180" x2="550" y2="140" stroke="black" stroke-width="2" marker-end="url(#arrow)" />

  <!-- Arrow definition -->
  <defs>
    <marker id="arrow" markerWidth="10" markerHeight="10" refX="6" refY="3" orient="auto">
      <path d="M0,0 L0,6 L9,3 z" fill="black" />
    </marker>
  </defs>

  <!-- Labels -->
  <text x="195" y="170" font-size="10">Eventos</text>
  <text x="365" y="170" font-size="10">Tráfego</text>
  <text x="520" y="150" font-size="10">Logs / Alertas</text>

</svg>

</div>

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

## 📎 Observação

As imagens serão adicionadas com o passar do tempo.

---

