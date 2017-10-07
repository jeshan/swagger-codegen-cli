
# swagger-codegen-cli

The official image doesn't allow calling easily in a CLI environment like Gitlab CI. This image is to allow that.

# Examples
## Gitlab CI
```yaml
swagger:
  image: jeshan/swagger-codegen-cli
  stage: build
  script:
  - 'java -jar /swagger-codegen-cli.jar generate -l java -i server/api/swagger/swagger.yaml -o swagger-java-client'
  artifacts:
    name: "${CI_JOB_NAME}_${CI_COMMIT_REF_NAME}"
    paths: ['swagger-java-client']
```
