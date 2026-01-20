# Roadmap

## Sprint 0 — Fundação (atual)
- Estrutura de diretórios do repositório.
- Documentação base e contratos conceituais mínimos.
- Definição de paths append-only e responsabilidades.

## Sprint 1 — Especificação do pipeline MVP
- Descrever fluxo de publicação (S3 + CloudFront + GitHub Actions) em nível conceitual.
- Definir formato exato do snapshot e metadata mínima.
- Especificar artefatos de assinatura e hashing.

## Sprint 2 — Infraestrutura mínima (planejada)
- IaC para S3, CloudFront e versionamento (quando aprovado).
- Políticas de acesso e distribuição.
- Documentação de operação e bootstrap.

## Sprint 3 — Pipeline de publicação (planejado)
- GitHub Actions para assinatura e upload.
- Geração de manifestos de release.
- Observabilidade mínima (logs e checks simples).

## Sprint 4 — CLI de verificação (planejada)
- Ferramenta CLI para baixar e validar snapshot.
- Verificação de hash e assinatura.
- Documentação de uso e exemplos.

## Sprint 5 — Hardening e auditoria (planejada)
- Revisão de segurança do fluxo.
- Checklist de auditoria e reprodutibilidade.
- Ajustes de documentação com base em uso real.
