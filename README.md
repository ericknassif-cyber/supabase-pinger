# supabase-pinger

Pinga projetos Supabase a cada 5 dias para evitar pausa automática no free tier.

## Como funciona

Um workflow GitHub Actions roda automaticamente a cada 5 dias e faz um HEAD request
ao endpoint REST de cada projeto listado. Se algum projeto falhar (ex: já foi pausado),
o workflow marca como falho e você recebe um email automático do GitHub com o nome
exato do projeto que falhou.

## Como adicionar um projeto

1. No Supabase: abra o projeto → **Settings → API**
   - Copie a **Project URL** (ex: `https://abcdefgh.supabase.co`)
   - Copie a **anon / public key**

2. Neste repositório: **Settings → Secrets and variables → Actions → `PROJECTS_JSON`**

3. Edite o valor do secret adicionando uma nova entrada ao array JSON:

```json
[
  { "name": "cliente-nome-prod",  "url": "https://xxxx.supabase.co", "anon_key": "eyJ..." },
  { "name": "cliente-nome-demo",  "url": "https://yyyy.supabase.co", "anon_key": "eyJ..." }
]
```

> Use nomes descritivos em `name` — eles aparecem diretamente nos logs de erro.

## Como testar manualmente

Vá em **Actions → Ping Supabase Projects → Run workflow**.

## Resposta a falhas

Se receber um email de falha do GitHub:

1. Clique no link do workflow na notificação
2. Veja qual projeto aparece com ❌ no log
3. Acesse **app.supabase.com**, encontre o projeto e clique em **Restore**
