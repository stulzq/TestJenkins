#!/usr/bin/env groovy Jenkinsfile
pipeline {
    def cusversion="1.0.0"
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
                script {
                    res1 = sh (script: "git diff --name-only $GIT_PREVIOUS_SUCCESSFUL_COMMIT|grep 'Jenkinsfile2'", returnStatus: true) 
                    echo "res1: ${res1}"
                    echo "cusversion: ${cusversion}"
                
                }
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
