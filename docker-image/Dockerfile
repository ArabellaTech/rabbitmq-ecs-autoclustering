FROM rabbitmq:3-management

RUN apt-get -y update \
    && apt-get -y install jq \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists

RUN rabbitmq-plugins --offline enable rabbitmq_peer_discovery_aws \
    && echo "cluster_formation.peer_discovery_backend = rabbit_peer_discovery_aws" >> /etc/rabbitmq/rabbitmq.conf \
    && echo "cluster_formation.node_cleanup.only_log_warning = false" >> /etc/rabbitmq/rabbitmq.conf \
    && echo "cluster_formation.aws.use_autoscaling_group = true" >> /etc/rabbitmq/rabbitmq.conf

COPY docker-cluster-entrypoint.sh /usr/local/bin/
COPY rabbitmq-definitions.json.template /etc/rabbitmq/

ENTRYPOINT ["docker-cluster-entrypoint.sh"]
CMD ["rabbitmq-server"]
