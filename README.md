# Signed Governance Artifacts (SGA)

## O que é
SGA é um projeto para publicar artefatos governados com integridade criptográfica verificável usando AWS (S3 + CloudFront) e automação via GitHub Actions. Ele define contratos mínimos de paths, versionamento e verificação para que consumidores possam validar a autenticidade e a imutabilidade dos artefatos publicados.

## O que não é
- Não é um backend, API REST, dashboard ou sistema de autenticação.
- Não é um conjunto de microserviços, Kubernetes, blockchain ou ML/IA.
- Não é um produto genérico de armazenamento; é um pipeline específico de publicação de artefatos governados.

## Como funciona (visão alta)
1. Um sistema de governança gera um artefato de snapshot (fora do escopo deste repositório).
2. O SGA assina, publica e distribui o snapshot em paths append-only com hashes e assinatura.
3. Um consumidor baixa o snapshot, verifica o hash e a assinatura, e então usa o conteúdo.

> **Nota:** URLs de distribuição (ex.: CloudFront) e chaves de assinatura são *placeholders* até o MVP ser implementado.

## O que dá para verificar
- Integridade (hash SHA-256).
- Autenticidade (assinatura digital).
- Imutabilidade por `release_id` (paths append-only).

## Navegação da documentação
- [PROJECT.md](PROJECT.md) — charter e princípios do projeto.
- [ROADMAP.md](ROADMAP.md) — sprints 0 a 5.
- [ARCHITECTURE.md](ARCHITECTURE.md) — arquitetura alvo e contratos conceituais.
- [VERIFY.md](VERIFY.md) — processo de verificação via CLI (com placeholders onde necessário).
- [docs/](docs/) — espaço reservado para documentação de apoio.
- [infra/](infra/) — placeholder para infraestrutura futura.

## Requisitos de governança
- Governança antes de performance.
- Simplicidade estrutural.
- Separação epistêmica (geração ≠ publicação ≠ consumo).
- Append-only conceitual.
- Tudo versionado (infra e docs).
- Nenhuma decisão “porque sim”.
