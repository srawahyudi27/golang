pipeline {

    agent any
    tools {
        go 'go_1.19.4'
    }
    environment {
        GO111MODULE = 'on'
        CGO_ENABLED = 0 
        GOPATH = "${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_ID}"
    }
    stages {

        stage('Build') {

            steps {
                sh 'go build'
            }
        }
        stage('Release') {
            when {
                buildingTag()
            }
            environment {
                GITHUB_TOKEN = credentials('github-token')
            }
            steps {
                echo 'starting the release to goreleaser'
                sh 'curl -sL https://git.io/goreleaser | bash'
            }
        }
    }
}
