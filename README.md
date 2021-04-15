Ansible Role Thanos
=========

Deploy various Thanos components with Podman.

Requirements
------------

This requires the containers.podman collection: https://galaxy.ansible.com/containers/podman

Role Variables
--------------

Variable                         | Description
---------------------------------|------------------
thanos_version                   | Thanos Version (Default: 0.18.0)
thanos_podman_network            | Podman network for pods. (Default: podman)
thanos_hostname                  | Pod hostname (Default: thanos)
thanos_domain                    | Pod domain (Default: example.com)
thanos_base_dir: /var/lib/containers
thanos_web_port: 10902
thanos_grpc_port: 10901
thanos_query_frontend_port: 9090
thanos_query_replicas: 2
thanos_memcached_enabled: false
thanos_memcached_count: 0
thanos_cache_config: []
thanos_query_frontend_enabled: false
thanos_query_frontend_command:
  - query-frontend
  - '--http-address=0.0.0.0:{{ thanos_query_frontend_port }}'
  - '--query-frontend.downstream-url=http://localhost:{{ 10902 }}'
  - --query-frontend.log-queries-longer-than=5s
  - --query-range.split-interval=24h
thanos_query_frontend_caching_command: []
thanos_sidecars: []
#thanos_sidecars:
#  - prometheus-sidecar.example.com:10901
thanos_query_command:
  - query
  - '--http-address=0.0.0.0:{{ thanos_web_port }}'
  - '--grpc-address=0.0.0.0:{{ thanos_grpc_port }}'
  - '--query.replica-label={{ thanos_query_replica_label }}'
  - '--store={{ thanos_store_ip }}:{{ thanos_grpc_port }}'
thanos_query_replica_label: prometheus_replica
thanos_store: false # Deploy Thanos store
thanos_store_command:
  - store
  - --data-dir=/data
  - |
    --objstore.config=type: S3 
    config:
      bucket: thanos
      region: us-east-1
      endpoint: s3.example.com
      access_key: secret
      secret_key: secret
      insecure: false
      signature_version2: false
thanos_compact_command:
  - compact
  - --data-dir=/tmp/thanos-compact
  - --wait
  - |
    --objstore.config=type: S3 

Dependencies
------------

No dependencies at this time

Example Playbook
----------------

    - hosts: thanos
      roles:
         - ansible-role-thanos

License
-------

BSD

Author Information
------------------

David Chatterton
david@davidchatterton.com
