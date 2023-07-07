Intial commit - empty repo

1. Initial setup
```bash
detect-secrets scan >.secrets.baseline
git add .secrets.baseline
```

2. Commit `secret.conf` fails as expected. (overridden with `SKIP=detect-secrets
   git commit`
