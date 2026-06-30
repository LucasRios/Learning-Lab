# AWS — Fundamentos de Cloud Computing

## 1. O que é Computação em Nuvem?

Entrega **sob demanda** de computação, banco de dados, armazenamento, aplicativos e outros recursos de TI via Internet com **preços pay-as-you-go**.

### 6 Vantagens da Nuvem

1. Mudar de despesa de capital (CapEx) para despesa variável (OpEx)
2. Economias de escala massivas
3. Parar de adivinhar capacidade
4. Aumentar velocidade e agilidade
5. Parar de gastar dinheiro com datacenters
6. Tornar-se global em minutos

---

## 2. Modelos de Serviço

| Modelo | Você gerencia | Provedor gerencia | Exemplo |
|---|---|---|---|
| **IaaS** | SO, runtime, aplicação | Hardware, rede, virtualização | EC2 |
| **PaaS** | Aplicação e dados | Tudo abaixo da aplicação | Elastic Beanstalk |
| **SaaS** | Uso do software | Tudo | Gmail, Office 365 |

## Modelos de Implantação

| Modelo | Descrição | Exemplos |
|---|---|---|
| **Nuvem pública** | Toda infraestrutura na nuvem | AWS, Azure, GCP |
| **Híbrido** | Mistura nuvem + on-premises | AWS Outposts |
| **Privado (on-premises)** | Você gerencia o datacenter | VMware privado |

---

## 3. Infraestrutura Global AWS

### Regiões
Localização física no globo composta por **3 ou mais Zonas de Disponibilidade**. Cada região é isolada das outras — falhas não se propagam entre regiões.

**Como escolher uma região:**
- Conformidade legal e residência de dados
- Latência para os usuários finais
- Disponibilidade dos serviços necessários
- Preço (varia entre regiões)

### Zonas de Disponibilidade (AZ)
Um ou mais datacenters com:
- Energia redundante e independente
- Rede redundante
- Conectividade de alta velocidade entre AZs da mesma região
- Distância mínima de 100km entre AZs

### Edge Locations
Endpoints para cache de conteúdo via **Amazon CloudFront** (CDN). Mais numerosas que as regiões — permitem baixa latência globalmente.

---

## 4. Rede — Amazon VPC

### Virtual Private Cloud (VPC)
Rede virtual isolada dentro da AWS. Você define: nome, região, range de IPs (CIDR).

```
VPC (ex: 10.0.0.0/16)
├── Sub-rede pública  (10.0.1.0/24) → acesso à internet
└── Sub-rede privada (10.0.2.0/24) → sem acesso direto à internet
```

### Componentes principais

| Componente | Função |
|---|---|
| **Internet Gateway** | Conecta a VPC à internet pública |
| **Virtual Private Gateway** | Conecta a VPC via VPN a redes on-premises |
| **AWS Direct Connect** | Conexão privada dedicada entre datacenter e VPC (menor latência, maior throughput) |
| **Sub-redes** | Segmentos da VPC — públicas ou privadas |
| **Route Tables** | Regras de roteamento do tráfego |
| **Security Groups** | Firewall stateful no nível da instância |
| **Network ACLs** | Firewall stateless no nível da sub-rede |

### AWS Direct Connect vs VPN

| | VPN | Direct Connect |
|---|---|---|
| Conexão | Pública (internet) criptografada | Privada dedicada |
| Latência | Variável | Consistente e baixa |
| Custo | Menor | Maior |
| Setup | Rápido | Semanas |

---

## 5. Computação — Amazon EC2

### Tipos de Instância

| Família | Otimizada para | Exemplos de uso |
|---|---|---|
| **General Purpose** | Balanceado CPU/RAM | Servidores web, ambientes dev |
| **Compute Optimized** | Alta CPU | Processamento de batch, gaming servers |
| **Memory Optimized** | Alto RAM | Bancos de dados in-memory, big data |
| **Storage Optimized** | Alta I/O de disco | Data warehouses, bancos NoSQL |
| **Accelerated Computing** | GPU/FPGA | ML training, rendering, HPC |

### Modelos de Preço EC2

| Modelo | Desconto | Compromisso | Quando usar |
|---|---|---|---|
| **On-Demand** | Nenhum | Nenhum | Workloads imprevisíveis, testes |
| **Reserved** | Até 72% | 1 ou 3 anos | Workloads estáveis e previsíveis |
| **Savings Plans** | Até 66% | 1 ou 3 anos (flexível por serviço) | Flexibilidade entre EC2, Lambda, Fargate |
| **Spot** | Até 90% | Nenhum (pode ser interrompido) | Workloads tolerantes a falhas, batch |
| **Dedicated Hosts** | — | Por hora ou por ano | Licenciamento por servidor, compliance |

### Auto Scaling
Ajusta automaticamente o número de instâncias EC2 conforme a demanda:
- **Scale out** — adiciona instâncias quando a demanda aumenta
- **Scale in** — remove instâncias quando a demanda diminui

---

## 6. Armazenamento

### Amazon S3 — Object Storage

Armazenamento de objetos com durabilidade de **99,999999999% (11 noves)**.

**Classes de armazenamento S3:**

| Classe | Uso | Disponibilidade | Custo |
|---|---|---|---|
| **Standard** | Dados frequentemente acessados | 99.99% | Alto |
| **Standard-IA** | Dados pouco acessados | 99.9% | Médio |
| **One Zone-IA** | Dados pouco acessados, 1 AZ | 99.5% | Menor |
| **Glacier Instant** | Arquivamento com acesso em ms | — | Baixo |
| **Glacier Flexible** | Arquivamento, acesso em minutos-horas | — | Muito baixo |
| **Glacier Deep Archive** | Retenção de longo prazo | — | Mínimo |
| **Intelligent-Tiering** | Acesso imprevisível | 99.9% | Automático |

### Outros serviços de armazenamento

| Serviço | Tipo | Uso |
|---|---|---|
| **EBS** | Block storage | Volume de disco para EC2 |
| **EFS** | File system | Compartilhamento de arquivos entre instâncias |
| **FSx** | File system gerenciado | Windows File Server, Lustre HPC |
| **Storage Gateway** | Híbrido | Integração on-premises com nuvem |
| **Snow Family** | Transferência física | Migração de grandes volumes offline |

---

## 7. Banco de Dados

### Serviços relacionais (SQL)

| Serviço | Engine | Destaque |
|---|---|---|
| **Amazon RDS** | MySQL, PostgreSQL, SQL Server, Oracle, MariaDB | Gerenciado com backups automáticos |
| **Amazon Aurora** | MySQL/PostgreSQL compatível | 5x mais rápido que MySQL, serverless option |

### Serviços não relacionais (NoSQL)

| Serviço | Tipo | Uso |
|---|---|---|
| **DynamoDB** | Key-value / Document | Alta performance, serverless, escala automática |
| **ElastiCache** | In-memory (Redis/Memcached) | Cache de sessão, resultados de queries |
| **DocumentDB** | Document (MongoDB-compatible) | Dados JSON semi-estruturados |
| **Neptune** | Graph | Grafos de relacionamentos |
| **Timestream** | Time-series | IoT, monitoramento, métricas |
| **QLDB** | Ledger | Histórico imutável e auditável |

---

## 8. Serviços Serverless

| Serviço | Função |
|---|---|
| **AWS Lambda** | Execução de código sem gerenciar servidores — cobrado por execução |
| **AWS Fargate** | Containers sem gerenciar clusters EC2 |
| **API Gateway** | Criação e gerenciamento de APIs REST e WebSocket |
| **EventBridge** | Barramento de eventos para integração entre serviços |
| **Step Functions** | Orquestração de workflows com máquinas de estado |

---

## 9. Segurança e Identidade

### Modelo de Responsabilidade Compartilhada

| AWS é responsável por | Cliente é responsável por |
|---|---|
| Infraestrutura física | Dados dos clientes |
| Hardware, rede global | Configuração de SO e apps |
| Hypervisor | IAM e controle de acesso |
| Serviços gerenciados | Criptografia de dados |

### Principais serviços de segurança

| Serviço | Função |
|---|---|
| **IAM** | Identidade e controle de acesso (usuários, grupos, roles, políticas) |
| **AWS Organizations** | Gerenciamento centralizado de múltiplas contas |
| **AWS KMS** | Gerenciamento de chaves de criptografia |
| **AWS Secrets Manager** | Armazenamento seguro de credenciais e segredos |
| **AWS Shield** | Proteção contra DDoS (Standard gratuito, Advanced pago) |
| **AWS WAF** | Web Application Firewall — filtra tráfego HTTP malicioso |
| **Amazon GuardDuty** | Detecção de ameaças com ML |
| **AWS CloudTrail** | Log de auditoria de todas as chamadas de API |
| **AWS Config** | Rastreamento de conformidade de configurações de recursos |

### IAM — Conceitos principais

- **Usuários** — identidades individuais
- **Grupos** — coleção de usuários com mesmas permissões
- **Roles** — permissões assumidas temporariamente por serviços ou usuários
- **Políticas** — documentos JSON que definem permissões
- **MFA** — autenticação multifator (obrigatório para conta root)

> **Princípio do menor privilégio:** conceda apenas as permissões mínimas necessárias.

---

## 10. Monitoramento e Gestão

| Serviço | Função |
|---|---|
| **Amazon CloudWatch** | Métricas, logs e alarmes de recursos AWS |
| **AWS CloudTrail** | Histórico de chamadas de API e atividades da conta |
| **AWS Trusted Advisor** | Recomendações de custo, segurança, performance e disponibilidade |
| **AWS Cost Explorer** | Análise e previsão de gastos |
| **AWS Budgets** | Alertas de orçamento |
| **AWS Health Dashboard** | Status dos serviços AWS em tempo real |

---

## 11. Suporte AWS

| Plano | Destaque |
|---|---|
| **Basic** | Gratuito, documentação e fóruns |
| **Developer** | Suporte técnico por e-mail em horário comercial |
| **Business** | Suporte 24/7, Trusted Advisor completo, SLA de 1h |
| **Enterprise On-Ramp** | TAM pool, SLA de 30 min para crítico |
| **Enterprise** | TAM dedicado, SLA de 15 min para crítico |
