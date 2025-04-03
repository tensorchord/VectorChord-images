ARG PG_MAJOR=16
ARG PGVECTOR_SEMVER=0.8.0
FROM pgvector/pgvector:${PGVECTOR_SEMVER}-pg${PG_MAJOR}

ARG PGRS_SEMVER=0.4.0
ARG VECTORCHORD_SEMVER=0.2.2
ARG VECTORCHORD_BM25_SEMVER=0.2.0
ARG PG_TOKENIZER_SEMVER=0.1.0
ARG TARGETARCH=amd64

RUN set -eux; \
    apt-get update && apt-get install -y \
    wget; \
    apt-get autoremove -y; \
    apt-get clean -y; \
    rm -rf /var/lib/apt/lists/*

# Install pgvecto.rs
RUN wget https://github.com/tensorchord/pgvecto.rs/releases/download/v${PGRS_SEMVER}/vectors-pg${PG_MAJOR}_${PGRS_SEMVER}_${TARGETARCH}.deb -O /tmp/vectors.deb; \
    dpkg -i /tmp/vectors.deb; 

# Install VectorChord
RUN wget https://github.com/tensorchord/VectorChord/releases/download/${VECTORCHORD_SEMVER}/postgresql-${PG_MAJOR}-vchord_${VECTORCHORD_SEMVER}-1_${TARGETARCH}.deb -O /tmp/vchord.deb; \
    dpkg -i /tmp/vchord.deb;

# Install VectorChord-bm25
RUN wget https://github.com/tensorchord/VectorChord-bm25/releases/download/${VECTORCHORD_BM25_SEMVER}/postgresql-${PG_MAJOR}-vchord-bm25_${VECTORCHORD_BM25_SEMVER}-1_${TARGETARCH}.deb -O /tmp/vchord-bm25.deb; \
    dpkg -i /tmp/vchord-bm25.deb;

# Install pg_tokenizer.rs
RUN wget https://github.com/tensorchord/pg_tokenizer.rs/releases/download/${PG_TOKENIZER_SEMVER}/postgresql-${PG_MAJOR}-pg-tokenizer_${PG_TOKENIZER_SEMVER}-1_${TARGETARCH}.deb -O /tmp/pg-tokenizer.deb; \
    dpkg -i /tmp/pg-tokenizer.deb; \
    rm -rf /tmp/*.deb

CMD ["postgres", "-c" ,"shared_preload_libraries=vectors.so, vchord.so, pg_tokenizer.so", "-c", "search_path=\"$user\", public, vectors, tokenizer_catalog"]
