ARG BASE=18-bookworm

FROM postgres:${BASE}

ARG VCHORD
ARG PGVECTOR

RUN apt-get update && \
	apt-get install -y --no-install-recommends wget ca-certificates && \
	wget https://github.com/tensorchord/VectorChord/releases/download/${VCHORD}/postgresql-${PG_MAJOR}-vchord_${VCHORD}-1_$(dpkg --print-architecture).deb -P /tmp && \
	apt-get install -y postgresql-${PG_MAJOR}-pgvector=${PGVECTOR}-* && \
	apt-get install -y /tmp/postgresql-${PG_MAJOR}-vchord_${VCHORD}-1_$(dpkg --print-architecture).deb && \
	apt-get remove -y wget ca-certificates && \
	apt-get purge -y --auto-remove && \
	rm -rf /tmp/* /var/lib/apt/lists/*

CMD ["postgres", "-c" ,"shared_preload_libraries=vchord,vector"]
