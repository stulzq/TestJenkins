#!/usr/bin/env groovy Jenkinsfile
pipeline {
    agent {
        node {
            label 'slave-1'
        }
    }
     stages {
        stage('Build') {
            steps {
                if (env.BRANCH_NAME== 'master')
                {
                    echo "branch: ${env.BRANCH_NAME}"
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
