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
        stage("Preparation") {
            steps {
                clearWorkspace();
                checkout(getGitRepoHandler("git@github.com:kacdab/docker-build-test.git", env.BRANCH_NAME, "docker-build-test");
                dir("docker-build-test") {
                    script {
                        gitConfig.readShaFromGit(this);
                        gitConfig.repoName = "docker-build-test";
                        gitConfig.branchName = env.BRANCH_NAME;
                        gitConfig.repoURL = "git@github.com:kacdab/docker-build-test.git";
                    }
                }
            }
        }
        stage("Build") {
            steps {
                dir(gitConfig.repoName) {
                    script {
                        publisher.build(gitConfig.repoName);
                        publisher.push(env.BRANCH_NAME, env.BUILD_NUMBER);
                    }
                }
            }
        }
    }
}
