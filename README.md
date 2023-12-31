# Common_Shared_Library
Sure, here's a README.md file for your official documentation:

```markdown
# Jenkins Shared Library Integration

This documentation provides instructions on how to incorporate the common-shared-library into your Jenkins pipelines, making it easier to manage and centralize common tasks.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Installation](#installation)
3. [Usage](#usage)
   - [Importing the Shared Library](#importing-the-shared-library)
   - [Utilizing Custom Steps](#utilizing-custom-steps)
4. [Example Jenkinsfile](#example-jenkinsfile)

## Prerequisites

Before you begin, ensure that:

- Jenkins is properly configured and operational in your environment.

## Installation

1. **Install the Library:**
   - Add the `common-shared-library` as a global library in your Jenkins instance. Navigate to "Manage Jenkins" -> "Configure System" -> "Global Pipeline Libraries" and configure it with the library name, version, and source code repository.

2. **Create a Jenkins Pipeline:**
   - Within your Jenkins project, either create a new Jenkinsfile or configure an existing one to utilize the shared library steps and functions.

## Usage

### Importing the Shared Library

Add the following line at the top of your Jenkins pipeline script (Jenkinsfile) to import the `common-shared-library`:

```groovy
@Library('common-shared-library') _
```

This line tells Jenkins to load the shared library.

### Utilizing Custom Steps

Once the library is imported, you can use its custom steps within your Jenkins pipeline script. The library provides several custom steps to simplify common tasks. Here are some examples:

- **Cleaning the Workspace:**

  To clean the workspace in your pipeline, use the `CleanWorkspace` step:

  ```groovy
  stage('Clean Workspace') {
      steps {
          CleanWorkspace()
      }
  }
  ```

- **Cloning a Git Repository:**

  For cloning a Git repository, utilize the `CloneRepo` step:

  ```groovy
  stage('Clone Repository') {
      steps {
          CloneRepo(url: 'https://github.com/your/repo.git', branch: 'main')
      }
  }
  ```

- **Credential Scanning:**

  For scanning code for credentials or sensitive information, employ the `CredentialScanner` step:

  ```groovy
  stage('Credential Scanning') {
      steps {
          CredentialScanner()
      }
  }
  ```

- **License Scanning:**

  To scan code for license compliance, use the `LicenseScanner` step:

  ```groovy
  stage('License Scanning') {
      steps {
          LicenseScanner()
      }
  }
  ```

- **Notifications:**

  For sending notifications (e.g., Slack or email notifications), you can use the `Notifications` step:

  ```groovy
  stage('Send Notifications') {
      steps {
          Notifications(message: 'Build successful')
      }
  }
  ```

### Complete Your Pipeline

Continue building your Jenkins pipeline by adding stages, steps, and configurations as needed. The custom steps from `common-shared-library` can be seamlessly integrated into your pipeline script to simplify and centralize common tasks.

## Example Jenkinsfile

Here's an example Jenkinsfile that demonstrates how to use the `common-shared-library` in a complete pipeline:

```groovy
@Library('common-shared-library') _

pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                CloneRepo(url: 'https://github.com/your/repo.git', branch: 'main')
            }
        }
        
        stage('Build and Test') {
            steps {
                // Your build and test steps here
            }
        }

        stage('Credential Scanning') {
            steps {
                CredentialScanner()
            }
        }

        stage('License Scanning') {
            steps {
                LicenseScanner()
            }
        }

        stage('Clean Workspace') {
            steps {
                CleanWorkspace()
            }
        }

        stage('Send Notifications') {
            steps {
                Notifications(message: 'Build successful')
            }
        }
    }

    post {
        success {
            // Actions to take if the pipeline is successful
            echo 'Pipeline was successful!'
        }
        failure {
            // Actions to take if the pipeline fails
            echo 'Pipeline failed!'
        }
    }
}
```

These shared functions simplify common tasks such as workspace cleanup, repository cloning, credential scanning, and more.
```

Make sure to replace `<https://github.com/your/repo.git>` with the actual Git repository URL, and `'common-shared-library'` with the name of your shared library as configured in Jenkins.

These shared functions simplify common tasks such as workspace cleanup, repository cloning, credential scanning, and more.

// Jenkinsfile

@Library('your-shared-library-name') // Replace 'your-shared-library-name' with the actual name of your shared library.
import greeting

pipeline {
    agent any

    stages {
        stage('Greeting') {
            steps {
                script {
                    def personName = "Alice"
                    
                    def greetingMessage = greeting.greet(personName)
                    def farewellMessage = greeting.farewell(personName)
                    
                    echo "Greeting: $greetingMessage"
                    echo "Farewell: $farewellMessage"
                }
            }
        }
    }
}
