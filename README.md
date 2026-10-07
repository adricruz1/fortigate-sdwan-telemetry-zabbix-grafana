# 🛡️ Enterprise SD-WAN Telemetry & SLA Monitoring (FortiGate + Zabbix + Grafana)

![Fortinet](https://img.shields.io/badge/Fortinet-FortiGate_200E-red)
![Zabbix](https://img.shields.io/badge/Zabbix-Proxy_LLD-red)
![Grafana](https://img.shields.io/badge/Grafana-Dashboard-orange)
![SecOps](https://img.shields.io/badge/Category-SecOps_%26_Telemetria-blue)

## 📌 Visão Geral do Projeto
Este projeto entrega uma solução de **telemetria de rede e monitorização de SLA por aplicação** num firewall FortiGate 200E, integrada via Zabbix Proxy e visualizada no Grafana.

A solução atende à necessidade da gestão de infraestrutura/segurança para mensuração contínua de **latência em milissegundos (ms)** e **perda de pacotes (%)** para serviços críticos e rotas SD-WAN, **sem a necessidade de Deep SSL Inspection** (evitando a exigência de distribuição de certificados CA nas estações de trabalho e eliminando riscos de bloqueio HTTPS).

---

## 🏗️ Arquitetura da Solução

text
[ FortiGate 200E ]
│ (Performance SLA Probes - OID .1.3.6.1.4.1.12356.101.4.9)
▼
[ Zabbix Proxy (SNMPv2c LLD) ]
│ (Coleta e Descoberta Automática de Probes/Membros)
▼
[ Zabbix Server (Cloud) ]
│ (Armazenamento de Histórico)
▼
[ Grafana Dashboard ] (Métricas e Transformações Regex em Tempo Real)

---

## 🚀 Funcionalidades & Destaques Técnicos

- **Monitorização Passiva de SLA de Aplicações:** Coleta direta via OID de SD-WAN Probes (`.1.3.6.1.4.1.12356.101.4.9`), ignorando a necessidade de interceptação TLS/SSL L7.
- **Descoberta Automática (LLD):** Descoberta dinâmica de túneis VPN e links de Internet (Algar, Embratel, Probes de Serviços) via Zabbix.
- **Tratamento Dinâmico de Mídia no Grafana:** Uso de expressões regulares (`Rename fields by regex`) para higienização dos nomes de membros e apresentação limpa em gráficos temporais.
- **Resiliência e Escala:** Arquitetura via Zabbix Proxy em ambiente distribuído (Local -> Cloud).

---

## 📊 Estrutura dos Painéis no Grafana

1. **Latência Real por Probe (ms):** Monitorização contínua de RTT por aplicação e destino SD-WAN.
2. **Perda de Pacotes (%):** Métrica de estabilidade e qualidade dos links WAN e VPNs.

---

## 🛠️ Como Utilizar este Repositório

1. **Grafana:** Importe o ficheiro JSON localizado em `dash/fortigate-sdwan-sla.json` no seu servidor Grafana.
2. **Zabbix:** Garanta que a regra de LLD para SD-WAN esteja ativa no host do FortiGate coletando as chaves de Latência e Packet Loss.
3. Ajuste o datasource do Grafana para apontar para o seu ambiente Zabbix.

---
**Autor:** Adriano Rodrigues Cruz  
**LinkedIn:** [linkedin.com/in/adriano-cruz-76a9a0236](https://linkedin.com/in/adriano-cruz-76a9a0236)
