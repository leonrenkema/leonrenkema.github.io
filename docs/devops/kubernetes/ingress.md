# Ingress snippets

## Sticky sessions

```yaml
annotations:
  nginx.ingress.kubernetes.io/affinity: "cookie"
  nginx.ingress.kubernetes.io/session-cookie-name: "route"
  nginx.ingress.kubernetes.io/session-cookie-max-age: "300"
```

## Multiple ingress controllers

When using multiple ingress controller you should annotate the ingress configuration with an `ingress.class`

```yaml
annotations:
  kubernetes.io/ingress.class: ingress-nginx-public
```
