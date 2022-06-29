# devops-pipeline-step-functions-example

[![aws-cli](https://img.shields.io/badge/awscli-v1.17.X-orange.svg)](https://aws.amazon.com/cli/)
[![java](https://img.shields.io/badge/java-v11.0.X-red.svg)](https://www.oracle.com/java/technologies/javase-downloads.html)

>A simple aws state machine project to test ADL DevOps AWS Step Function Pipelines.
>
>Developed with all :heart: in the world by ADL DevOps team

## Table of Contents

- [Prerequisites](#prerequisites)
- [Quickstart](#quickstart)
- [Testing](#testing)
- [Deploy](#deploy)
- [Contributing](#contributing)
- [Further Reading / Useful Links](#further-reading--useful-links)

## Prerequisites

You will need the following things properly installed on your computer:

* [Java SE](https://www.oracle.com/java/technologies/javase-downloads.html)
* [AWS cli](https://aws.amazon.com/cli/)
* [AWS step functions local](https://docs.aws.amazon.com/step-functions/latest/dg/sfn-local.html)

## Quickstart

Execute the step functions local jar in background with the command `java -jar StepFunctionsLocal.jar &` and that's it! You now have a local aws environment for deploy, update, run a destroy your step functions. 

## Testing

First at all, you need to create a dummy state machine locally running: 
`aws stepfunctions --endpoint-url http://localhost:8083 create-state-machine --definition "{\
  \"Comment\": \"A Hello World example of the Amazon States Language using a Pass state\",\
  \"StartAt\": \"HelloWorld\",\
  \"States\": {\
    \"HelloWorld\": {\
      \"Type\": \"Pass\",\
      \"End\": true\
    }\
}}" --name "State machine test" --role-arn "arn:aws:iam::012345678901:role/DummyRole"` 

The execution of this command gives the state machine arn as output.

Then, for test the update operation, run `aws stepfunctions --endpoint-url http://localhost:8083 update-state-machine --state-machine-arn ${ARN} --definition "$(cat step_function.json)"` where the ARN variable is in the output of the previous command.

The update operation realizes a syntactic and semantic validation.

## Deploy

For deployment, run the command `aws stepfunctions update-state-machine --state-machine-arn ${ARN} --definition "$(cat step_function.json)"` but now the ARN variable is the actual ARN of the state machine to update.

## Contributing

If you find this repo useful here's how you can help:

1. Send a Pull Request with your awesome new features and bug fixes
2. Wait for a Coronita :beer: you deserve it.

## Further Reading / Useful Links

* [Setting up aws step functions locally](https://docs.aws.amazon.com/step-functions/latest/dg/sfn-local.html)
* [You can set up your step functions local environment with docker too!](https://docs.aws.amazon.com/step-functions/latest/dg/sfn-local-docker.html)
