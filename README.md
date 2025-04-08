# VectorChord Images

## VectorChord Suite Image

```bash
docker run   \           
  --name vchord-suite  \
  -e POSTGRES_PASSWORD=postgres  \
  -p 5432:5432 \
  -d tensorchord/vchord-suite:pg17-20250408
  # If you want to use ghcr image, you can change the image to `ghcr.io/tensorchord/vchord-suite:pg17-20250408`.
  # if you want to use the latest version, you can use the tag `pg17-latest`.
```

```sql
CREATE EXTENSION IF NOT EXISTS vectors CASCADE;
CREATE EXTENSION IF NOT EXISTS vchord CASCADE;
CREATE EXTENSION IF NOT EXISTS pg_tokenizer CASCADE;
CREATE EXTENSION IF NOT EXISTS vchord_bm25 CASCADE;
\dx
pg_tokenizer | 0.1.0   | tokenizer_catalog | pg_tokenizer
plpgsql      | 1.0     | pg_catalog        | PL/pgSQL procedural language
vchord       | 0.2.2   | public            | vchord: Vector database plugin for Postgres, written in Rust, specifically designed for LLM
vchord_bm25  | 0.2.0   | bm25_catalog      | vchord_bm25: A postgresql extension for bm25 ranking algorithm
vector       | 0.8.0   | public            | vector data type and ivfflat and hnsw access methods
```