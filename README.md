# Unraid Templates

Custom Unraid Community Applications templates.

## Available templates

### Hindsight

Self-hosted agent memory system — gives LLM agents persistent, queryable memory with knowledge graph and semantic search. State-of-the-art on the LongMemEval benchmark.

- **Image**: `ghcr.io/vectorize-io/hindsight:latest`
- **Project**: https://hindsight.vectorize.io/
- **Source**: https://github.com/vectorize-io/hindsight (MIT)
- **Web UI**: port `9999` · **API**: port `8888`

#### Highlights

- **Zero-touch first run** — template auto-fixes the bind-mount permission mismatch (Unraid creates paths as `nobody:users` / 99:100, but the upstream image runs as uid 1000). The template starts the container as root, chowns the cache + database paths, then drops privileges before launching the API. No manual `docker exec chown` required.
- **Embedded Postgres by default** — works standalone, no external services required.
- **External pgvector supported** — set `HINDSIGHT_API_DATABASE_URL` to point at any PostgreSQL with the `vector` extension.
- **Persistent model cache** — ~220 MB of embedding/reranker weights cached to `appdata/hindsight/cache/` so container updates don't re-download.
- **All providers supported** — OpenAI, Anthropic, Gemini, Groq, DeepSeek, MiniMax, Vertex AI, plus self-hosted Ollama and LM Studio.

#### Quick install (without Community Applications acceptance)

In Unraid Web UI:

1. **Apps → ⚙ (top-right) → Manage Repositories**
2. Add: `https://github.com/wisdommen/unraid-templates`
3. **Apps → search "Hindsight" → Install**
4. Fill in your LLM API key, click Apply

#### Required environment variables

| Variable | Example |
|---|---|
| `HINDSIGHT_API_LLM_PROVIDER` | `openai` |
| `HINDSIGHT_API_LLM_API_KEY` | `sk-...` |
| `HINDSIGHT_API_LLM_MODEL` | `gpt-4o-mini` |

For self-hosted LLMs (Ollama, LM Studio), also set `HINDSIGHT_API_LLM_BASE_URL`.

## License

Templates are MIT. Wrapped images carry their own licenses (Hindsight is MIT).

## Issues / support

Open an issue at https://github.com/wisdommen/unraid-templates/issues
