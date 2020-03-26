# Ingress snippets

## Sticky sessions

```yml
annotations:
  nginx.ingress.kubernetes.io/affinity: "cookie"
  nginx.ingress.kubernetes.io/session-cookie-name: "route"
  nginx.ingress.kubernetes.io/session-cookie-max-age: "300"
```

## Multiple ingress controllers

```yml
annotations:
  kubernetes.io/ingress.class: ingress-nginx-public
```
