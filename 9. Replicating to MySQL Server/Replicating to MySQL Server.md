# 🔁 Read Replicas no HeatWave MySQL

> Aumente a escalabilidade e performance da sua aplicação MySQL com as réplicas de leitura do HeatWave.

## 📘 O que são Read Replicas?

Read Replicas (réplicas de leitura) são cópias de uma instância primária MySQL que podem ser usadas exclusivamente para **operações de leitura** (queries `SELECT`).  
No **HeatWave MySQL**, essas réplicas são otimizadas para **desempenho analítico** e **escalabilidade horizontal**.

---

## ✅ Benefícios

- ⚡ **Aumento de performance**: distribui a carga de leitura entre múltiplas instâncias.
- 🔄 **Alta disponibilidade**: permite failover e recuperação mais rápida.
- 🔍 **Separação de cargas**: leitura e escrita podem ser feitas por instâncias distintas.
- 📊 **Integração com HeatWave**: aceleração para análises em tempo real com colunas in-memory.

---

## 🧱 Arquitetura

```text
                        +-------------------+
                        | Aplicação Cliente |
                        +--------+----------+
                                 |
                 +---------------+---------------+
                 |                               |
        +--------v--------+             +--------v--------+
        | Instância Primária| --------> |  Read Replica #1 |
        +--------+--------+             +--------+--------+
                 |                               |
                 |                       +--------v--------+
                 |                       |  Read Replica #2 |
                 |                       +------------------+
