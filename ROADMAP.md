# Roadmap

## Sprint 0 — Fundação (atual)
- Estrutura de diretórios do repositório.
- Documentação base e contratos conceituais mínimos.
- Definição de paths append-only e responsabilidades.

## Sprint 1 — Infra básica
- S3 com versionamento habilitado.
- CloudFront com OAC.
- IaC versionado para provisionamento inicial.

## Sprint 2 — Pipeline automatizado
- Geração de hash SHA-256 do snapshot.
- Upload do snapshot e `.sha256`.
- Registro mínimo do release.

## Sprint 3 — Assinatura
- Geração de `.sig`.
- Documentação de verificação via CLI.
- Publicação dos contratos de assinatura.

## Sprint 4 — Integração com consumidores
- Integração com ConexaoSolar via CloudFront.
- Fluxo de consumo e validação fim a fim.

## Sprint 5 — Hardening
- KMS/rotação de chaves.
- Cache controlado.
- Observabilidade mínima.
