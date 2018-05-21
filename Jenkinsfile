#!groovy
@Library('JenkinsMain@ComponentIncludedV2') _

pipeline {
    agent {
        label 'master'
    }
    stage {
        stage("Build") {
            when {
                branch 'development*'
            }
            steps {
                dir(gitConfig.repoName) {
                    script {
                        publisher.build("kacper-build-test");
                    }
                }
            }
        }
    }
}
