# Projeto: Signed Governance Artifacts (SGA)

## Charter
O SGA publica artefatos governados com integridade criptográfica verificável usando AWS. O objetivo é permitir que consumidores verifiquem autenticidade e imutabilidade de snapshots de governança sem depender de sistemas proprietários.

### Princípios obrigatórios
- Governança antes de performance.
- Simplicidade estrutural.
- Separação epistêmica (geração ≠ publicação ≠ consumo).
- Append-only conceitual (nunca sobrescrever artefatos publicados).
- Tudo versionado (infra e docs).
- Nenhuma decisão “porque sim”.

### Escopo
- **Inclui:** documentação, contratos conceituais, estrutura de repositório e planejamento do MVP.
- **Exclui:** implementação de infraestrutura, pipelines, backend, APIs, dashboards, autenticação, microserviços, Kubernetes, blockchain, ML/IA.

### Definição de sucesso (MVP)
- Publicação de snapshots governados em paths append-only.
- Assinatura e distribuição via S3 + CloudFront.
- Verificação via CLI por consumidores.

### Sistemas do ecossistema
- **governanca-system:** gera o artefato de snapshot.
- **SGA:** publica, assina e distribui.
- **ConexaoSolar:** consome e verifica.

### Não objetivos
- Gerar ou decidir políticas de governança.
- Fornecer integrações customizadas fora do MVP.
- Otimizações prematuras de performance.
