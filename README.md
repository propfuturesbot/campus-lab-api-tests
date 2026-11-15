# Campus Lab API tests

API tests for the Campus Lab practice server, run by Newman in GitHub Actions on every push and pull request.

- `collections/` the exported Postman collection
- `data/` the data file the collection runs once per row
- `ci.env.json` the environment (base address only, no secrets)
- `.github/workflows/api-tests.yml` the pipeline

The API key is not in this repository. It is stored as the repository secret `CAMPUS_KEY`.
