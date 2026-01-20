# Verificação via CLI (processo)

## Objetivo
Permitir que um consumidor valide integridade e autenticidade de um snapshot publicado pelo SGA.

## Pré-requisitos
- CLI de verificação (ainda **não implementada** — placeholder).
- Chave pública de verificação (placeholder: `PUBLIC_KEY_PLACEHOLDER`).
- URL base de distribuição (placeholder: `https://<CLOUDFRONT_DOMAIN>/artifacts/snapshot/`).

## Contratos mínimos (documento)
- **O que é assinado:** o hash SHA-256 de `snapshot.json` e `snapshot.json.meta.json` (hashes calculados separadamente, cada um com sua assinatura).
- **Algoritmo de assinatura:** Ed25519.
- **Formato do `.sig`:** base64 em arquivo texto contendo apenas a assinatura (uma linha).

Esses contratos serão implementados no MVP e não mudam a estrutura append-only dos paths.

## Passo a passo (placeholder)
1. Definir o `release_id`.
2. Baixar `snapshot.json`, `snapshot.json.sha256`, `snapshot.json.sig`, `snapshot.json.meta.json`, `snapshot.json.meta.json.sha256` e `snapshot.json.meta.json.sig`.
3. Verificar os hashes SHA-256.
4. Verificar as assinaturas com a chave pública (Ed25519).

### Exemplo (placeholder)
```bash
export RELEASE_ID="20250101T120000Z_abcdef0"
export BASE_URL="https://<CLOUDFRONT_DOMAIN>/artifacts/snapshot"

# Baixar artefatos
curl -O "$BASE_URL/$RELEASE_ID/snapshot.json"
curl -O "$BASE_URL/$RELEASE_ID/snapshot.json.sha256"
curl -O "$BASE_URL/$RELEASE_ID/snapshot.json.sig"
curl -O "$BASE_URL/$RELEASE_ID/snapshot.json.meta.json"
curl -O "$BASE_URL/$RELEASE_ID/snapshot.json.meta.json.sha256"
curl -O "$BASE_URL/$RELEASE_ID/snapshot.json.meta.json.sig"

# Verificar hash
sha256sum -c snapshot.json.sha256
sha256sum -c snapshot.json.meta.json.sha256

# Verificar assinatura (exemplo genérico)
sgaverify --pubkey PUBLIC_KEY_PLACEHOLDER --sig snapshot.json.sig --file snapshot.json --alg ed25519 --sig-format base64
sgaverify --pubkey PUBLIC_KEY_PLACEHOLDER --sig snapshot.json.meta.json.sig --file snapshot.json.meta.json --alg ed25519 --sig-format base64
```

## Observações
- A CLI `sgaverify` é **planejada** para o MVP e substituirá o comando genérico acima.
- Até o MVP, os valores de URL e chave pública permanecerão como placeholders.
