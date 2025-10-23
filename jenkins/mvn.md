
Dockerfile
```
# FROM 10.91.8.106:5000/riskbox/riskbox:0.0.3
# Dùng OpenJDK 21
FROM eclipse-temurin:21-jdk

WORKDIR /app

# Copy file JAR build ra từ Maven
COPY target/*.jar app.jar

# Đặt timezone (tùy chọn)
RUN ln -fs /usr/share/zoneinfo/Asia/Phnom_Penh /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

EXPOSE 8089

# Chạy ứng dụng
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
```



Jenkins Pipeline
```
pipeline {
    agent any
 
    environment {
        REGISTRY = "192.168.56.14:5000" // docker registry
        PROJECT = "mvn-demo-uat"
        IMAGE_NAME = "${REGISTRY}/${PROJECT}/${PROJECT}:${BUILD_NUMBER}"
        TZ = "Asia/Phnom_Penh"
    }
 
    stages {
        stage('Tool Install') {
            steps {
                script {
                    env.JAVA_HOME = tool name: 'jdk21', type: 'jdk'
                    env.MAVEN_HOME = tool name: 'M3911', type: 'maven'
                    env.PATH = "${env.JAVA_HOME}/bin:${env.MAVEN_HOME}/bin:${env.PATH}"
                }
                sh 'java -version'
                sh 'mvn -version'
            }
        }
 
        stage('Cloning Git') {
            steps {
                git branch: 'main',
                    credentialsId: 'gitlab',
                    url: 'https://gitlab.com/javanekogroup/mvn-demo.git'
            }
        }
        
        stage('Maven Build JAR') {
            steps {
                sh '''
                    echo "=== Building JAR package ==="
                    mvn clean package -DskipTests
                    mkdir -p target
                    ls -lh target/
                '''
            }
        }

        stage('Extract JAR (verify only)') {
            steps {
                sh '''
                    echo "=== Extracting JAR for verification ==="
                    rm -rf target/ROOT
                    mkdir -p target/ROOT
                    unzip -o target/*.jar -d target/ROOT > /dev/null
                    echo "JAR extracted successfully."
                '''
            }
        }
 
        stage('Build Docker Image') {
            steps {
                script {
                    sh """
                        echo "=== BUILD DOCKER IMAGE ==="
                        docker build --no-cache -t ${IMAGE_NAME} -f Dockerfile .
                    """
                }
            }
        }
 
        stage('Push Image to Registry') {
            steps {
                script {
                    sh """
                        echo "=== PUSH IMAGE TO REGISTRY ==="
                        docker push ${IMAGE_NAME}
                    """
                }
            }
        }
    }
 
    post {
        success {
            echo "✅ Build & Push successful: ${IMAGE_NAME}"
        }
        failure {
            echo "❌ Build failed at stage: ${env.STAGE_NAME}"
        }
    }
}
```