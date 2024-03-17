pipeline {
    agent any
    tools {
        jfrog 'local'
    }
    stages {
        stage('Clone') {
            steps {
                git branch: 'master', url: "https://github.com/scsibug/mvn-hello-world.git"
            }
        }

        stage('Exec Maven commands') {
            steps {
                // Configure Maven project's repositories
                jf 'mvn-config --repo-resolve-releases cyber-maven-virtual --repo-resolve-snapshots cyber-maven-virtual --repo-deploy-releases cyber-maven-virtual --repo-deploy-snapshots cyber-maven-virtual'
                // Install and publish project
                jf 'mvn clean install'
            }
        }

        stage('Publish build info') {
            steps {
                jf 'rt build-publish'
            }
        }
    }
}