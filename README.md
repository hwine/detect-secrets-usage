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

6. Once you've audited secrets, you'll find that if you change line numbers in
   the file, your first commit attempt will show changes made.
   ```bash
   # add property to secret.json
   git add --update
   git commit  # fails
   Detect secrets...........................................................Failed
   - hook id: detect-secrets
   - exit code: 3
   - files were modified by this hook

   The baseline file was updated.
   Probably to keep line numbers of secrets up-to-date.
   Please `git add .secrets.baseline`, thank you.
   # if you want, verify the changes
   git diff .secrets.baseline
   # see that only `line_number` & `generated_at` properties are changed
   git add --update
   git commit  # succeeds
   ```

7. If you have files that contain only hashes, but no secrets (such as
   dependency lock files), you can add those files to your `detect-secrets`
   configuration in the `.pre-commit-config.yaml` file as [described
   here](https://github.com/Yelp/detect-secrets#blocking-secrets-not-in-baseline)
   (at the end of the section).
