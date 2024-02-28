pipeline {
    agent {
        label 'linux_000143'
    }
    options {
        timestamps()
        disableConcurrentBuilds()
    }
    stages {
        stage('Clean') {
            steps {
                cleanWs() // Clean the workspace before starting
            }
        }

        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Supriya', refspec: '+refs/changes/*:refs/changes/*', url: 'https://github.com/SupriyaShetkar/dockerhub-Pipeline.git']]])
            }
        }

        stage('Build image') {
            steps {
              def app = docker.build("9763479341/test")
            }
        }

        stage('Push image') {
            steps {
                docker.withRegistry('https://registry.hub.docker.com', 'git') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                }
            }
        }
    }
}
