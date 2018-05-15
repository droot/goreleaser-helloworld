# goreleaser-helloworld
Hello World sample for GoReleaser

Steps to test the build locally:
container-builder-local --config=./cloudbuild.yaml --dryrun=false --substitutions=_GOOS=$GOOS,_GOARCH=$GOARCH,_GITHUB_TOKEN=$(cat ~/.github.tokens) --write-workspace=/tmp/goreleaser-o .

Steps to make GITHUB_TOKEN available in container builder:
Follow the steps at this link --> https://cloud.google.com/container-builder/docs/securing-builds/use-encrypted-secrets-credentials
 - First enable KMS API in your project
 - Create the keyring
 gcloud kms keyrings create github-tokens --location=global
 - Create the Key
 gcloud kms keys create gh-release-token --location=global --keyring=github-tokens --purpose=encryption


 Publishing GoReleaser docker images:

 Go to GoReleaser project:
  1. build the image: docker build -t golang_with_goreleaser:1.10-stretch .
  2. Run docker tag --> docker tag golang_with_goreleaser gcr.io/kustomize-199618/golang_with_goreleaser:1.10-stretch
  3. gcloud auth configure-docker
  4. docker push gcr.io/kustomize-199618/golang_with_goreleaser:1.10-stretch 

