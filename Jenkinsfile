#!/usr/bin/env groovy Jenkinsfile
pipeline {
    agent {
        node {
            label 'slave-1'
        }
    }
    environment {
        NUGET_KEY     = credentials('CanalSharp_Nuget_key')
    }
    triggers {
      githubPush()
    }
     stages {
        stage('Build') {
            steps {
                echo "branch: ${env.BRANCH_NAME}"
                echo "current SHA: ${env.GIT_COMMIT}"
                echo "previous SHA: ${env.GIT_PREVIOUS_SUCCESSFUL_COMMIT}"
                sh (script: "git diff --stat $GIT_PREVIOUS_SUCCESSFUL_COMMIT $GIT_COMMIT", returnStatus: false) 
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
                echo "${env.NUGET_KEY}"
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
    post { always { script { currentBuild.result = 'NOT_BUILT' } } }
}
