Intial commit - empty repo

1. Initial setup
```bash
detect-secrets scan >.secrets.baseline
git add .secrets.baseline
```

2. Commit `secret.conf` fails as expected. (overridden with `SKIP=detect-secrets
   git commit`

3. Add another secret to `secret.conf`, but use 2 forms of [inline
   Allowlisting](https://github.com/Yelp/detect-secrets/blob/master/README.md#Inline-Allowlisting).
   `detect-secrets` does not hinder the commit.
