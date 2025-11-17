pipeline { 

    agent any 

 

    stages { 

        stage('Build') { 

            steps { 

                sh 'mvn clean package -DskipTests' 

            } 

        } 

 

        stage('Upload to Nexus') { 

            environment { 

                USER = credentials('nexus-admin').username 

                PASS = credentials('nexus-admin').password 

            } 

            steps { 

                sh """ 

                curl -v -u "$USER:$PASS"\

                --upload-file target/maven-demo-1.0.jar \ 

                http://localhost:8081/repository/maven-releases/com/example/maven-demo/1.0/maven-demo-1.0.jar 

                """ 

            } 

        } 

    } 

} 
