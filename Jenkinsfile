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
                dir('maven-examples/maven-example') {
                    // Configure Maven project's repositories
                    jf 'mvn-config --repo-resolve-releases cyber-maven-default --repo-resolve-snapshots cyber-maven-default --repo-deploy-releases cyber-maven-default --repo-deploy-snapshots cyber-maven-default'

                    // Install and publish project
                    jf 'mvn clean install'
                }
            }
        }

        stage('Publish build info') {
            steps {
                jf 'rt build-publish'
            }
        }
    }
}