# Arquitetura (MVP alvo)

## Visão geral
O SGA atua como camada de publicação e distribuição de artefatos de governança. Ele **não** gera artefatos e **não** é o consumidor final. A arquitetura separa responsabilidades para garantir auditabilidade e reduzir acoplamentos.

### Diagrama ASCII
```
+-------------------+        +---------------------------+        +-------------------+
| governanca-system | -----> | SGA (assina/publica)      | -----> | ConexaoSolar      |
| (gera snapshot)   |        | S3 + CloudFront + GH A    |        | (consome/verifica)|
+-------------------+        +---------------------------+        +-------------------+
```

## Contratos conceituais mínimos

### A) Convenção de paths append-only
Proposta de paths (não sobrescrever releases):
```
/artifacts/snapshot/<release_id>/snapshot.json
/artifacts/snapshot/<release_id>/snapshot.json.sha256
/artifacts/snapshot/<release_id>/snapshot.json.sig
/artifacts/snapshot/<release_id>/snapshot.json.meta.json
/artifacts/snapshot/<release_id>/snapshot.json.meta.json.sha256
/artifacts/snapshot/<release_id>/snapshot.json.meta.json.sig
```
- `release_id` = `YYYYMMDDTHHMMSSZ_<gitsha7>`.
- `snapshot.json.meta.json` **faz parte do MVP** por baixo custo e maior auditabilidade. Ele registra timestamp de geração, origem do artefato e `release_id`, e é publicado como artefato imutável junto ao snapshot. O hash e a assinatura cobrem `snapshot.json` e `snapshot.json.meta.json`.

### B) Separação de responsabilidades
- **governanca-system:** gera o snapshot.
- **SGA:** assina, publica e distribui.
- **ConexaoSolar:** consome e verifica.

### C) Imutabilidade e versionamento
- Paths são append-only: novos releases recebem novos `release_id`.
- Releases não são sobrescritos, mesmo em correções.
- S3 versioning será habilitado no MVP para reforçar imutabilidade (detalhado na fase de infraestrutura).

### D) Política de cache conceitual
- Artefatos são imutáveis por `release_id`.
- Cache pode ser longo (ex.: `Cache-Control: max-age=31536000, immutable`).
- Não há invalidação por conteúdo; somente novos releases.

## Limitações atuais
- URLs de distribuição e chaves de assinatura são placeholders.
- Não há pipeline nem infraestrutura implementados nesta fase.
