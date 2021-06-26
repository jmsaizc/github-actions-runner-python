# github-actions-runner-python
Simple Docker image for starting self-hosted Github Actions python runner

Thanks to 👤 **Samuel Berthe** for sharing

* Twitter: [@samuelberthe](https://twitter.com/samuelberthe)
* Github: [@samber](https://github.com/samber)

## Steps

Add your self-hosted runner from your repository settings:

- Go to repository > settings > actions
- Click on "Add runner"
- Copy the URL and token

Start a runner:

```
docker build -t gh-runner-python:latest .

docker run -d \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /tmp:/tmp \
    -e GH_REPOSITORY=xxxxxxxxxxxx \
    -e GH_RUNNER_TOKEN=xxxxxxxxxxxxx \
    -e GH_RUNNER_LABELS=label1,label2 \
    gh-runner-python:latest
```

Workflow example:

```yaml
# .github/workflows/main.yml

on:
  - push

jobs:
  frontend:
    runs-on: self-hosted
    steps:
      - uses: actions/checkout@v2
      - name: Fetch dependencies
        run: yarn
      - name: Build application
        run: npm run build
      - name: Execute tests
        run: npm run test
```

