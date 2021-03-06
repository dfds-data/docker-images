# Docker images

This repo contains dockerfiles and CI/CD for our public docker images.

## Images

### Kafka Connect

This contains a docker image with the connectors that we use.

### Schema Registry

This contains a docker image with the Postgres driver.

### Connect On-prem

This contains a docker image only with the connectors that we use on-prem.

## Updating images

1. Make your changes to the image
2. Update the `version`-file for the image to give the image a new tag

## Adding another image

1. Create a subfolder (name may only contain alphanumeric characters and underscores)
   with the files `Dockerfile` and `version`. `Dockerfile` will be your recipe
   for building the image, and `version` will hold the image tag.
2. Go to the AWS console and create a public ECR with the same name as the subfolder
3. Add this to `azure-pipelines.yaml`:

```yaml
- template: build-and-push-template.yaml
  parameters:
    subfolder: <your subfolder name here>
```

4. Your image will be built and pushed to ecr
5. Update this readme with info about your new image

## Known issues

Cleanup of untagged images in ECR is manual at the moment.
