# Verificação via CLI (processo)

## Objetivo
Permitir que um consumidor valide integridade e autenticidade de um snapshot publicado pelo SGA.

## Pré-requisitos
- CLI de verificação (ainda **não implementada** — placeholder).
- Chave pública de verificação (placeholder: `PUBLIC_KEY_PLACEHOLDER`).
- URL base de distribuição (placeholder: `https://<CLOUDFRONT_DOMAIN>/artifacts/snapshot/`).

## Passo a passo (placeholder)
1. Definir o `release_id`.
2. Baixar `snapshot.json`, `snapshot.json.sha256` e `snapshot.json.sig`.
3. Verificar o hash SHA-256.
4. Verificar a assinatura com a chave pública.

### Exemplo (placeholder)
```bash
export RELEASE_ID="20250101T120000Z_abcdef0"
export BASE_URL="https://<CLOUDFRONT_DOMAIN>/artifacts/snapshot"

# Baixar artefatos
curl -O "$BASE_URL/$RELEASE_ID/snapshot.json"
curl -O "$BASE_URL/$RELEASE_ID/snapshot.json.sha256"
curl -O "$BASE_URL/$RELEASE_ID/snapshot.json.sig"

# Verificar hash
sha256sum -c snapshot.json.sha256

# Verificar assinatura (exemplo genérico)
sgaverify --pubkey PUBLIC_KEY_PLACEHOLDER --sig snapshot.json.sig --file snapshot.json
```

## Observações
- A CLI `sgaverify` é **planejada** para o MVP e substituirá o comando genérico acima.
- Até o MVP, os valores de URL e chave pública permanecerão como placeholders.
