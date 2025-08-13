ARG BASE=18-bookworm

FROM postgres:${BASE}

ARG PGTOKENIZER

RUN apt-get update && \
	apt-get install -y --no-install-recommends wget ca-certificates && \
	wget https://github.com/tensorchord/pg_tokenizer.rs/releases/download/${PGTOKENIZER}/postgresql-${PG_MAJOR}-pg-tokenizer_${PGTOKENIZER}-1_$(dpkg --print-architecture).deb -P /tmp && \
	dpkg-deb -x /tmp/postgresql-${PG_MAJOR}-pg-tokenizer_${PGTOKENIZER}-1_$(dpkg --print-architecture).deb /sysroot && \
	apt-get remove -y wget ca-certificates && \
	apt-get purge -y --auto-remove && \
	rm -rf /tmp/* /var/lib/apt/lists/*

FROM scratch

COPY --from=0 /sysroot /
