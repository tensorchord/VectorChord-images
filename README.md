# VectorChord Images

This repository contains the resources to build VectorChord Suite images and the Postgre Docker images for [VectorChord Cloud](https://cloud.vectorchord.ai).

## VectorChord Suite Image

You can use the `tensorchord/vchord-suite` image to run multiple extensions which are provided by TensorChord. The image is based on the official Postgres image and includes the following extensions:
```bash
docker run \
  --name vchord-suite \
  -e POSTGRES_PASSWORD=postgres \
  -p 5432:5432 \
  -d tensorchord/vchord-suite:pg18-latest
  # If you want to use ghcr image, you can change the image to `ghcr.io/tensorchord/vchord-suite:pg18-latest`.
  # if you want to use the specific version, you can use the tag `pg17-20250815`, supported version can be found in the support matrix.
```

```sql
CREATE EXTENSION IF NOT EXISTS vchord CASCADE;
CREATE EXTENSION IF NOT EXISTS pg_tokenizer CASCADE;
CREATE EXTENSION IF NOT EXISTS vchord_bm25 CASCADE;
\dx
pg_tokenizer | 0.1.0   | tokenizer_catalog | pg_tokenizer
vchord       | 0.5.3   | public            | vchord: Vector database plugin for Postgres, written in Rust, specifically designed for LLM
vchord_bm25  | 0.2.2   | bm25_catalog      | vchord_bm25: A postgresql extension for bm25 ranking algorithm
vector       | 0.8.1   | public            | vector data type and ivfflat and hnsw access methods
```

### Support Matrix

#### Hardware Compatibility

| CPU Architecture | status |
| ---------------- | ------ |
| x86_64           | ✅      |
| ARM64            | ✅      |

#### Extension Compatibility

##### 20250929 (latest)

| Extension Name | Github Repo                                                         | Version |
| -------------- | ------------------------------------------------------------------- | ------- |
| vchord         | [VectorChord](https://github.com/tensorchord/VectorChord)           | 0.5.3   |
| pg_tokenizer   | [pg_tokenizer.rs](https://github.com/tensorchord/pg_tokenizer.rs)   | 0.1.1   |
| vchord_bm25    | [VectorChord-bm25](https://github.com/tensorchord/VectorChord-bm25) | 0.2.2   |
| vector         | [pgvector](https://github.com/pgvector/pgvector)                    | 0.8.1   |

##### 20250915

| Extension Name | Github Repo                                                         | Version |
| -------------- | ------------------------------------------------------------------- | ------- |
| vchord         | [VectorChord](https://github.com/tensorchord/VectorChord)           | 0.5.2   |
| pg_tokenizer   | [pg_tokenizer.rs](https://github.com/tensorchord/pg_tokenizer.rs)   | 0.1.0   |
| vchord_bm25    | [VectorChord-bm25](https://github.com/tensorchord/VectorChord-bm25) | 0.2.1   |
| vector         | [pgvector](https://github.com/pgvector/pgvector)                    | 0.8.1   |

##### 20250901

| Extension Name | Github Repo                                                         | Version |
| -------------- | ------------------------------------------------------------------- | ------- |
| vchord         | [VectorChord](https://github.com/tensorchord/VectorChord)           | 0.5.0   |
| pg_tokenizer   | [pg_tokenizer.rs](https://github.com/tensorchord/pg_tokenizer.rs)   | 0.1.0   |
| vchord_bm25    | [VectorChord-bm25](https://github.com/tensorchord/VectorChord-bm25) | 0.2.1   |
| vector         | [pgvector](https://github.com/pgvector/pgvector)                    | 0.8.0   |
