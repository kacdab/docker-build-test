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
                checkout(getGitRepoHandler(getRepoURL(), env.BRANCH_NAME, getRepoName()));
                dir(getRepoName()) {
                    script {
                        gitConfig.readShaFromGit(this);
                        gitConfig.repoName = getRepoName();
                        gitConfig.branchName = env.BRANCH_NAME;
                        gitConfig.repoURL = getRepoURL();
                    }
                }
                script {
                    publisher.init(this, env.ECR_REPO, env.ECR_CREDENTIAL_ID);
                }
            }
        }
        stage("Build") {
            steps {
                script {
                    docker.build("test");
                }
            }
        }
    }
}
