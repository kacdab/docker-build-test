#!groovy
@Library('JenkinsMain@ComponentIncludedV2') _

pipeline {
    agent {
        label 'master'
    }
    environment {
        ECR_REPO = 'http://495615712771.dkr.ecr.eu-central-1.amazonaws.com/';
        ECR_CREDENTIAL_ID = 'ecr:eu-central-1:dd38ebe3-285a-40ff-8bcf-60d874d67e80';
    }
    stages {
        stage("Build") {
            steps {
                dir("docker-build-test") {
                    script {
                        publisher.build_ng(this, "docker-build-test");
                    }
                }
            }
        }
    }
}
