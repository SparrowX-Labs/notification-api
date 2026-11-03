# Notification API

FastAPI notification lifecycle service for SparrowX. It creates, lists, retrieves, and updates notifications, persists them in the Crossplane-managed `notificationdb` PostgreSQL database, and exposes health and Prometheus endpoints.

The main API is under `/api/notifications/`; `/health` is the container probe, `/api/notifications/health` is the smoke-test endpoint, `/metrics` exposes Prometheus metrics, and `/docs`/`/redoc` provide API documentation.

Argo CD deploys the Helm values for `dev` and `prod` as separate namespaces on the same EKS cluster. Shared CI/CD workflows build immutable images, run tests and security checks, synchronize Argo CD, and validate the deployment.

Define `HEALTH_CHECK_PATH` and optionally override `AWS_ROLE_NAME`. AWS configuration, URLs, and Argo CD credentials are inherited from the organization.

## Local development

```bash
python -m pip install -r requirements-dev.txt
pytest
uvicorn src.main:app --reload --port 8000
```

Runtime database variables are `DB_HOST`, `DB_PORT`, `DB_NAME`, `DB_USERNAME`, `DB_PASSWORD`, and optional `CORS_ALLOW_ORIGINS`.

## License

See [LICENSE.md](LICENSE.md).
