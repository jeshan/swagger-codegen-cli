
# swagger-codegen-cli

The official image doesn't allow calling easily in a CI environment like Gitlab CI. This image is to allow that.

# Examples
## Docker Compose
Run:

`docker-compose up`

This will look for a file called swagger.yaml in the current directory, compile a java client and output it into a directory called swagger-java-client. But chances are you want to customise this. Use the following options:

- SRC_PATH=/path/to/your/project
- SPEC_RELATIVE_PATH=$RELATIVE_TO_SRC_PATH/swagger.yaml
- SWAGGER_LANG=java

Either modify them in .env or run them as follows:

`SRC_PATH=/path/to/your/project SPEC_RELATIVE_PATH=$RELATIVE_TO_SRC_PATH/swagger.yaml SWAGGER_LANG=java docker-compose up`

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
