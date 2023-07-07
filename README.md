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

4. Add secrets to a json file, which does not support comments. First way, just
   add to baseline:
   ```bash
   git add secret.json
   git commit  # fails
   detect-secrets scan >.secrets.baseline
   git commit  # succeeds
   ```

5. Better than just adding to baseline is to use the `audit` functionality to
   document the inclusion was intentional. (And not just an add-to-baseline to
   get the warning to go away.)
   ```bash
   detect-secrets audit .secrets.baseline
   git add --update
   git commit  # succeeds
   ```
