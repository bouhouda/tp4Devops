pipeline {
    environment {
        registry = "bouhouda/tp4"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }

    agent any

    stages {
        stage('Cloning Git') {
            steps {
                echo "Clonage du repository depuis GitHub..."
                git 'https://github.com/bouhouda/tp4Devops'
            }
        }

        stage('Building Image') {
            steps {
                script {
                    echo "Construction de l'image Docker..."
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Test Image') {
            steps {
                script {
                    echo "Exécution des tests sur l'image Docker..."
                    echo "Tests passed"  // Ici, ajouter les commandes réelles de test si nécessaire
                }
            }
        }

        stage('Publish Image') {
            steps {
                script {
                    echo "Connexion à DockerHub et publication de l'image..."
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()  // Push de l'image vers DockerHub
                    }
                }
            }
        }

        stage('Deploy Image') {
            steps {
                script {
                    echo "Déploiement de l'image Docker..."
                    bat "docker run -d ${registry}:${BUILD_NUMBER}"
                }
            }
        }
    }
}
