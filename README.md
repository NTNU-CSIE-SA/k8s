# Kubernetes Deployments

Applications are formed with kustomize and can be deployed to a Kubernetes cluster using the following command:

```bash
kubectl apply -k <app-dir>
```

Some applications may require additional configuration, secrets are managed by `.env` files.

## Deployment steps

1. Deploy the cloudflared as ingress controller first
2. Deploy the ArgoCD
3. Deploy the rest of the applications through ArgoCD

## Notes

- The kubernetes `.env` parser keeps `"` characters in the value, so it's important to not surround the value with `"` characters.
