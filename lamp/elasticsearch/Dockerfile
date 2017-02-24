FROM elasticsearch:2.2.0

ENV PATH /usr/share/elasticsearch/bin:$PATH

RUN set -ex \
	&& for path in \
		/usr/share/elasticsearch/data \
		/usr/share/elasticsearch/logs \
		/usr/share/elasticsearch/config \
		/usr/share/elasticsearch/config/scripts \
	; do \
		mkdir -p "$path"; \
		chown -R elasticsearch:elasticsearch "$path"; \
	done

COPY config /usr/share/elasticsearch/config

#NOT WORK WITH 2.2.0 VERSION
#RUN /usr/share/elasticsearch/bin/plugin install mobz/elasticsearch-head --verbose

VOLUME ["/var/log/elasticsearch","/usr/share/elasticsearch"]

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 9200 9300

CMD ["elasticsearch"]
