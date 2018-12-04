#### Custom Helm Chart
```bash
helm create k8s-app
cd k8s-app
```

change yaml
```yaml
# Default values for k8s-app.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

replicaCount: 1

image:
  repository: pamir/webapp
  tag: latest
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 80

ingress:
  enabled: false
  annotations: {}
    # kubernetes.io/ingress.class: nginx
    # kubernetes.io/tls-acme: "true"
  path: /
  hosts:
    - chart-example.local
  tls: []
  #  - secretName: chart-example-tls
  #    hosts:
  #      - chart-example.local

resources: 
  limits:
    cpu: 100m
    memory: 128Mi
  requests:
    cpu: 100m
    memory: 128Mi

nodeSelector: {}

tolerations: []

affinity: {}
```
```bash
helm install --name pn . --namespace app -f values
```

change the container port with variable
```yaml
container:
  port: 8080


---
ports:
- name: http
 containerPort: "{{ .Values.container.port}}"

```
