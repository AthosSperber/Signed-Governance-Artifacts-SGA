# Verificação via CLI (processo)

## Objetivo
Permitir que um consumidor valide integridade e autenticidade de um snapshot publicado pelo SGA.

## Pré-requisitos
- Chave pública de verificação (placeholder: `PUBLIC_KEY_PLACEHOLDER`).
- URL base de distribuição (placeholder: `https://<CLOUDFRONT_DOMAIN>/artifacts/snapshot/`).

## Contratos mínimos (documento)
- **O que é assinado:** os arquivos `snapshot.json.sha256` e `snapshot.json.meta.json.sha256` (cada hash é assinado separadamente).
- **Formato do `.sha256`:** exatamente o formato do `sha256sum`: `<hex><dois espaços><nome do arquivo>\n`.
- **Algoritmo de assinatura:** Ed25519.
- **Formato do `.sig`:** base64 em arquivo texto contendo apenas a assinatura (uma linha).

Esses contratos serão implementados no MVP e não mudam a estrutura append-only dos paths.

## Passo a passo (placeholder)
1. Definir o `release_id`.
2. Baixar `snapshot.json`, `snapshot.json.sha256`, `snapshot.json.sig`, `snapshot.json.meta.json`, `snapshot.json.meta.json.sha256` e `snapshot.json.meta.json.sig`.
3. Verificar os hashes SHA-256.
4. Verificar as assinaturas (Ed25519) **sobre os arquivos `.sha256`** com a chave pública.

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

# Verificar assinatura (exemplo preferencial com ssh-keygen -Y)
# Requer chave pública em formato SSH (ex.: "ssh-ed25519 AAAA...").
base64 -d snapshot.json.sig > snapshot.json.sig.bin
base64 -d snapshot.json.meta.json.sig > snapshot.json.meta.json.sig.bin

ssh-keygen -Y verify -f PUBLIC_KEY_PLACEHOLDER -I "SGA" \
  -n "snapshot" -s snapshot.json.sig.bin < snapshot.json.sha256
ssh-keygen -Y verify -f PUBLIC_KEY_PLACEHOLDER -I "SGA" \
  -n "snapshot" -s snapshot.json.meta.json.sig.bin < snapshot.json.meta.json.sha256
```

## Observações
- A CLI `sgaverify` é **opcional** e **fora do MVP**; se existir no futuro, apenas encapsulará um verificador Ed25519 equivalente.
- O exemplo com `ssh-keygen -Y verify` é preferencial, mas qualquer verificador Ed25519 que valide a assinatura sobre o arquivo `.sha256` é aceitável.
- Até o MVP, os valores de URL e chave pública permanecerão como placeholders.
