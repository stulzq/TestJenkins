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
                echo "branch: ${env.BRANCH_NAME}"
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
                echo 'test'
            }
        }
    }
}
