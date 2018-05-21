#!groovy
@Library('JenkinsMain@ComponentIncludedV2') _

pipeline {
    agent {
        label 'master'
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
                dir(gitConfig.repoName) {
                    script {
                        publisher.build(gitConfig.repoName);
                    }
                }
            }
        }
    }
}
