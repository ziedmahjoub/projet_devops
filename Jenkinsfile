pipeline {
    agent any
    
    stages {
        // ÉTAPE 1 : Récupérer le code depuis GitHub
        stage('Récupération du code') {
            steps {
                echo '========== Clonage du repository =========='
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: "*/main"]],
                    userRemoteConfigs: [[
                        url: "https://github.com/ziedmahjoub/projet_devops.git",
                        credentialsId: 'github-credentials'
                    ]]
                ])
                echo '✅ Code récupéré avec succès'
            }
        }
        
        // ÉTAPE 2 : Nettoyer les anciens builds
        stage('Nettoyage') {
            steps {
                echo '========== Nettoyage des builds antérieurs =========='
                sh 'mvn clean'
                echo '✅ Nettoyage terminé'
            }
        }
        
        // ÉTAPE 3 : Compiler le projet
        stage('Build') {
            steps {
                echo '========== Compilation du projet =========='
                sh 'mvn package -DskipTests'
                echo '✅ Build réussi'
            }
        }
        
        // ÉTAPE 4 : Exécuter les tests
        stage('Tests Unitaires') {
            steps {
                echo '========== Exécution des tests unitaires =========='
                sh 'mvn test'
                echo '✅ Tests unitaires réussis'
            }
        }
        
        // ÉTAPE 5 : Sauvegarder les résultats
        stage('Résultats') {
            steps {
                echo '========== Archivage des résultats =========='
                junit 'target/surefire-reports/*.xml'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                echo '✅ Résultats archivés'
            }
        }
    }
    
    // Messages finaux
    post {
        success {
            echo '🎉 Pipeline exécutée avec succès!'
        }
        failure {
            echo '❌ Erreur lors de l\'exécution de la pipeline'
        }
        always {
            echo '========== Fin de la pipeline =========='
        }
    }
} 
