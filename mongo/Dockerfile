FROM mongo

RUN rm -rf /var/lib/apt/lists/*

# Define mountable directories.
VOLUME ["/data/db","/var/log/mongo"]

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["mongod"]

# Expose ports.
#   - 27017: process
#   - 28017: http
EXPOSE 27017
EXPOSE 28017

