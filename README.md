# Student Management API

API REST de gestion des étudiants développée avec **Spring Boot**, conteneurisée avec **Docker** et intégrée dans un pipeline **CI/CD Jenkins** qui construit l'image et la publie automatiquement sur Docker Hub.

Projet académique réalisé à ESPRIT, axé sur la mise en pratique d'une chaîne DevOps complète : du code à l'image Docker déployable, en passant par l'intégration continue.

## Stack technique

| Catégorie | Technologies |
|---|---|
| Langage / Framework | Java 17, Spring Boot 3.5.5 |
| Persistance | Spring Data JPA, MySQL |
| Documentation API | springdoc-openapi (Swagger UI) |
| Outillage | Lombok, Maven (via Maven Wrapper) |
| Conteneurisation | Docker |
| CI/CD | Jenkins (build + push vers Docker Hub) |

## Pipeline CI/CD

Le `Jenkinsfile` définit un pipeline à deux étapes :

1. **Build Docker Image** — construction de l'image à partir du `Dockerfile`.
2. **Push Docker Image** — publication de l'image sur Docker Hub (`ziedmahjoub/monapp`) via les identifiants stockés dans Jenkins.

Le `Dockerfile` s'appuie sur une image `eclipse-temurin:17-jre-alpine` légère et exécute le jar généré par Maven (`target/*.jar`).

## Prérequis

- Java 17
- MySQL (base créée et accessible)
- Docker (optionnel, pour l'exécution conteneurisée)

## Lancer le projet en local

```bash
# Cloner le repo
git clone https://github.com/ziedmahjoub/projet_devops.git
cd projet_devops

# Configurer la connexion MySQL dans src/main/resources/application.properties
# (URL, utilisateur, mot de passe de votre base locale)

# Lancer l'application
./mvnw spring-boot:run
```

L'application démarre par défaut sur `http://localhost:8080`.
La documentation interactive de l'API (Swagger UI) est disponible sur `http://localhost:8080/swagger-ui.html`.

## Lancer avec Docker

```bash
# Construire le jar
./mvnw clean package -DskipTests

# Construire l'image
docker build -t student-management .

# Lancer le conteneur
docker run -p 8080:8080 student-management
```

## Auteur

**Zied Mahjoub** — Étudiant ingénieur, ESPRIT
[github.com/ziedmahjoub](https://github.com/ziedmahjoub)
