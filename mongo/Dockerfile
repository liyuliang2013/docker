FROM mongo

RUN rm -rf /var/lib/apt/lists/*

COPY mongod.conf /etc/mongod.conf

RUN chown -R mongodb:mongodb /var/log/mongodb

# Define mountable directories.
VOLUME ["/data/db","/var/log/mongodb"]


# Expose ports.
#   - 27017: process
#   - 28017: http
EXPOSE 27017
EXPOSE 28017


# Define working directory.
WORKDIR /data

# Define default command.
#CMD ["mongod", "--config", "/etc/mongod.conf"]

ENTRYPOINT ["/usr/bin/mongod", "--config", "/etc/mongod.conf"]
CMD ["--quiet"]

