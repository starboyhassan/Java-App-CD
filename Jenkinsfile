
pipeline {
    agent { label "Jenkins-Agent" }
    environment {
              REPO_PATTERN = "767397888237.dkr.ecr.us-east-1.amazonaws.com/java-project-repo:java-app"
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
                sh """
                    cat deployment.yaml
                    sed -i 's#${REPO_PATTERN}.*#${REPO_PATTERN}-${IMAGE_TAG}#g' deployment.yaml
                    cat deployment.yaml
                """
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
    post {
        success {
            script {
                // Slack notification on successful build
                slackSend(
                    channel: "jenkinschannel",
                    color: "#00FF80",
                    message:"SUCCESSED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
                )
            }
        }
        
        failure {
            script {
                // Slack notification on failed build
                slackSend(
                    channel: "jenkinschannel",
                    color: "#FF0000",
                    message:"FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
                )
            }
        }
    }
}