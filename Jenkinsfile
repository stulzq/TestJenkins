#!/usr/bin/env groovy Jenkinsfile
pipeline {
    agent {
        node {
            label 'slave-1'
        }
    }
    triggers {
      githubPush()
    }
     stages {
        stage('Build') {
            steps {
                echo "branch: ${env.BRANCH_NAME}"
                script {
                    result = sh (script: "git log -1 | grep '\\[ci skip\\]'", returnStatus: true) 
                    if (result != 0) {
                        echo "performing build..."
                    } else {
                        echo "not running..."
                    }
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            when {
                branch "test"
            }
            steps {
                echo 'testaaaa'
            }
        }
    }
    post { always { script { echo "${currentBuild.result}" } } }
}
