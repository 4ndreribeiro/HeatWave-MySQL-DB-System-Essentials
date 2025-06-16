
# 🔁 Read Replicas no HeatWave MySQL

Este documento explica como configurar e utilizar **Read Replicas** no **MySQL Database Service com HeatWave** na Oracle Cloud Infrastructure (OCI).

---

## 📘 O que são Read Replicas?

As Read Replicas são instâncias de banco de dados MySQL que funcionam como cópias somente leitura de uma instância primária. São usadas para:

- Escalar a leitura de aplicações.
- Melhorar desempenho de consultas.
- Separar cargas de leitura e escrita.
- Acelerar análises com HeatWave.

---

## ✅ Benefícios

- 🔄 Separação de cargas de leitura e escrita
- ⚡ Escalabilidade horizontal
- 📈 Redução de latência de leitura
- 🔥 Suporte a consultas analíticas com HeatWave
- 🛡️ Failover planejado e alta disponibilidade

---

## 🧱 Arquitetura

```
+-------------------+
| Aplicação Cliente |
+--------+----------+
         |
+--------v--------+         +--------------------+
| Instância Primária| ----> | Read Replica #1    |
+--------+--------+         +--------------------+
         |
         |                  +--------------------+
         +----------------> | Read Replica #2    |
                            +--------------------+
```

---

## 🚀 Como Criar uma Read Replica (OCI CLI)

### Pré-requisitos

- OCI CLI configurado (`oci setup config`)
- Instância MySQL existente

### Comando

```bash
oci mysql replica create \
  --source-db-system-id ocid1.mysqldbsystem.oc1..xxxxx \
  --display-name replica-heatwave-01 \
  --compartment-id ocid1.compartment.oc1..xxxxx \
  --admin-password 'SenhaForte123!' \
  --shape-name "MySQL.VM.Standard.E3.1" \
  --availability-domain "AD-1"
```

---

## 🔥 Acelerando com HeatWave

```bash
oci mysql heat-wave-cluster create \
  --db-system-id ocid1.mysqlreplica.oc1..xxxxx \
  --shape-name "MySQL.HeatWave.VM.Standard.E3" \
  --cluster-size 2
```

---

## 🔎 Testando a Read Replica

```bash
mysql -h replica-heatwave-01.mysql.sa-saopaulo-1.oraclecloud.com -u admin -p
```

```sql
-- Leitura liberada
SELECT COUNT(*) FROM vendas WHERE status = 'completo';

-- Escrita bloqueada
INSERT INTO vendas (produto) VALUES ('Novo');
-- ERRO: servidor está em modo read-only
```
![Arquitetura das Read Replicas](./heatwave_read_replicas.svg)

---

## 📌 Boas Práticas

- Nunca escreva diretamente em réplicas.
- Monitore a latência da replicação.
- Use balanceadores para distribuir carga.
- Promova réplicas em caso de falha da primária.

---

## 📄 Licença

Distribuído sob a licença MIT.
