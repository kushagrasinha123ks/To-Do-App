# To-Do Application

## Highlights

- Hooks
- AWS S3
- CI/CD Pipeline
- AWS CodeBuild
- AWS CodePipeline

## Overview

This project involves developing a To-Do Application with a comprehensive CI/CD pipeline. The application includes functionalities for adding, deleting, and searching tasks, and is built using React with Tailwind CSS for styling and Redux for state management. The deployment process is automated using AWS services.

## Features

- **Task Management:** Add, delete, and search tasks.
- **Styling:** Utilizes Tailwind CSS for responsive and modern design.
- **State Management:** Managed with Redux for efficient state handling.

## CI/CD Pipeline

The CI/CD pipeline is configured to automate the build and deployment process:

1. **Source:** GitHub repository.
2. **Build:** AWS CodeBuild to compile and build the application.
3. **Manual Approval:** AWS CodePipeline includes a manual approval stage.
4. **Deploy:** Artifacts are stored in AWS S3.

## S3 Bucket Policy

The S3 bucket policy ensures that the objects within the bucket are publicly accessible:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "todoappsid",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": [
                "arn:aws:s3:::bucketname/*"
            ]
        }
    ]
}
```

## Buildspec File - buildspec.yaml

```yaml
version: 0.2

phases:
  install:
    runtime-versions:
      nodejs: 18.x
    commands:
      - npm ci

  pre_build:
    commands:
      - echo Installing source NPM dependencies...

  build:
    commands:
      - npm run build

artifacts:
  files:
    - '**/*'
  base-directory: 'dist'

cache:
  paths:
    - 'node_modules/**/*'
```
