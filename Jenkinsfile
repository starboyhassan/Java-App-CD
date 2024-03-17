
pipeline {
    agent { label "Jenkins-Agent" }
    environment {
              APP_NAME = "Java-App"
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
               steps {
                   git branch: 'main', url: 'https://github.com/starboyhassan/Java-App-CD'
               }
        }

        stage("Update the Deployment Tags") {
            steps {
                    // Read deployment YAML file
                    def yaml = readFile 'deployment.yaml'
                    // Replace image tag
                    yaml = yaml.replaceAll(/image: 767397888237.dkr.ecr.us-east-1.amazonaws.com\/java-project-repo:${APP_NAME}-\d+/, "image: 767397888237.dkr.ecr.us-east-1.amazonaws.com/java-project-repo:${APP_NAME}-${IMAGE_TAG}")
                    // Write updated YAML back to file
                    writeFile file: 'deployment.yaml', text: yaml

            }
        }

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                   git config --global user.name "StarboyHassan"
                   git add deployment.yaml
                   git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                  sh "git push https://github.com/starboyhassan/Java-App-CD main"
                }
            }
        }
      
    }
}