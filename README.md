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

## Secret Management

Secrets are encrypted using `sops` and stored in the repository.

### Encrypting secrets

Everyone can encrypt the secrets using the following command:

```bash
# Encrypt the .env secret file
sops -e .env > enc.env
# Encrypt the .yaml secret file
sops -e secret.yaml > secret.enc.yaml
```

The public key used for encryption: [`deploy-key.pub`](deploy-key.pub)
The SOPS configuration file: [`.sops.yaml`](.sops.yaml)

### Decrypting secrets

Only the deployment environment can decrypt the secrets.
