ARG BASE=18-bookworm

FROM postgres:${BASE}

ARG VCHORDBM25
ARG PGTOKENIZER
ARG VCHORD
ARG PGVECTOR

RUN apt-get update && \
    apt-get install -y --no-install-recommends wget ca-certificates && \
    wget https://github.com/tensorchord/VectorChord-bm25/releases/download/${VCHORDBM25}/postgresql-${PG_MAJOR}-vchord-bm25_${VCHORDBM25}-1_$(dpkg --print-architecture).deb -P /tmp && \
    wget https://github.com/tensorchord/pg_tokenizer.rs/releases/download/${PGTOKENIZER}/postgresql-${PG_MAJOR}-pg-tokenizer_${PGTOKENIZER}-1_$(dpkg --print-architecture).deb -P /tmp && \
    wget https://github.com/tensorchord/VectorChord/releases/download/${VCHORD}/postgresql-${PG_MAJOR}-vchord_${VCHORD}-1_$(dpkg --print-architecture).deb -P /tmp && \
    apt-get install -y postgresql-${PG_MAJOR}-pgvector=${PGVECTOR}-* && \
    apt-get install -y /tmp/postgresql-${PG_MAJOR}-vchord_${VCHORD}-1_$(dpkg --print-architecture).deb && \
    apt-get install -y /tmp/postgresql-${PG_MAJOR}-pg-tokenizer_${PGTOKENIZER}-1_$(dpkg --print-architecture).deb && \
    apt-get install -y /tmp/postgresql-${PG_MAJOR}-vchord-bm25_${VCHORDBM25}-1_$(dpkg --print-architecture).deb && \
    apt-get remove -y wget ca-certificates && \
    apt-get purge -y --auto-remove && \
    rm -rf /tmp/* /var/lib/apt/lists/*

CMD ["postgres", "-c" ,"shared_preload_libraries=vchord,vchord_bm25,vector,pg_tokenizer", "-c", "search_path=\"$user\", public, bm25_catalog, tokenizer_catalog"]
