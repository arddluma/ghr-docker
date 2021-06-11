# ghr-docker
Docker image for ghr tool

Pull image from DockerHub:

```
docker pull ardd97/ghr
```
To build it locally:

```
docker build -t ghr .
```

This repo is using Dockerfile from https://github.com/tsub/docker-ghr - I've updated only the ghr version!

**Automate GitHub releases in CircleCI pipeline**

Note: make sure you've genarated GITHUB_TOKEN 

``` 
publish-github-release:
    docker:
      - image: ardd97/ghr
    steps:
      - checkout
      - run:
          name: "Publish Release on GitHub"
          command: |
            PACKAGE_VERSION="$(jq .version package.json -r)"
            ghr -t "${GITHUB_TOKEN}" -u "${CIRCLE_PROJECT_USERNAME}" -r "${CIRCLE_PROJECT_REPONAME}" -c "${CIRCLE_SHA1}" "$PACKAGE_VERSION"
   
   ```
