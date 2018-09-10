# kubernetes-prometheus
Configuration files for setting up prometheus monitoring on Kubernetes cluster.

I copy some from https://devopscube.com/setup-prometheus-monitoring-on-kubernetes/

the most important is the prometheus config,from:https://github.com/prometheus/prometheus/blob/master/documentation/examples/prometheus-kubernetes.yml

notice there:
```
scrape_configs:
- job_name: 'kubernetes-apiservers'

  kubernetes_sd_configs:
  - role: endpoints

  # Default to scraping over https. If required, just disable this or change to
  # `http`.
  scheme: https

  # This TLS & bearer token file config is used to connect to the actual scrape
  # endpoints for cluster components. This is separate to discovery auth
  # configuration because discovery & scraping are two separate concerns in
  # Prometheus. The discovery auth config is automatic if Prometheus runs inside
  # the cluster. Otherwise, more config options have to be provided within the
  # <kubernetes_sd_config>.
  tls_config:
    ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
    # If your node certificates are self-signed or use a different CA to the
    # master CA, then disable certificate verification below. Note that
    # certificate verification is an integral part of a secure infrastructure
    # so this should only be disabled in a controlled environment. You can
    # disable certificate verification by uncommenting the line below.
    #
    # insecure_skip_verify: true
  bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
```
the comment mean:
```
    # If your node certificates are self-signed or use a different CA to the
    # master CA, then disable certificate verification below. Note that
    # certificate verification is an integral part of a secure infrastructure
    # so this should only be disabled in a controlled environment. You can
    # disable certificate verification by uncommenting the line below.   如果使用自签证书，或者非CA机构认证的证书，需要注释下面一行；
```
即：
```
- job_name: 'kubernetes-apiservers'

  kubernetes_sd_configs:
  - role: endpoints

  # Default to scraping over https. If required, just disable this or change to
  # `http`.
  scheme: https

  # This TLS & bearer token file config is used to connect to the actual scrape
  # endpoints for cluster components. This is separate to discovery auth
  # configuration because discovery & scraping are two separate concerns in
  # Prometheus. The discovery auth config is automatic if Prometheus runs inside
  # the cluster. Otherwise, more config options have to be provided within the
  # <kubernetes_sd_config>.
  tls_config:
    ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
    insecure_skip_verify: true
  bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
```
