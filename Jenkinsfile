pipeline {
    agent any
    parameters {
        string(name: "repoName", description: "Repo name", defaultValue: "")
        string(name: "username", description: "Owner of repo", defaultValue: "")
    }
    environment {
        myname = "vedant"
    }
    stages {
        stage("clean"){
            steps{
                deleteDir()
            }
        }
        stage("Select Repository") {
            steps {
                script {
                    def branches = sh(script: "git ls-remote --heads https://github.com/${params.username}/${params.repoName}.git", returnStdout: true).split('\n').collect { it.replaceAll(/.*refs\/heads\//, '') }
                    branchChoice = input(
                        id: 'repoInput', message: 'Select a branch:', parameters: [choice(name: 'REPO_BRANCH', choices: branches)]
                    )
                }
            }
        }
        stage("Display Branch Info") {
            steps {
            	echo "branch selected is ${branchChoice}"
                script {
                    def repoDir = "${env.WORKSPACE}/${params.repoName}"
                    echo "Repository directory: ${repoDir}"
                    def branchFile = "${repoDir}/${branchChoice}.txt"
                    echo "Branch file path: ${branchFile}"
                    def fileContents = readFile(branchFile)
                    echo "Selected branch is ${branchChoice}"
                    echo "Contents of ${branchFile}:\n${fileContents}"
                }
            }
        }
    }
}
