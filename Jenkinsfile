#!groovy
@Library('JenkinsMain@ComponentIncludedV2') _

pipeline {
    agent {
        label 'master'
    }
    stages {
        stage("Build") {
            steps {
                script {
                    publisher.build("test");
                }
            }
        }
    }
}
