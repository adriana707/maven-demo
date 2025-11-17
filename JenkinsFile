pipeline { 

    agent any 

 

    stages { 

        stage('Build') { 

            steps { 

                sh 'mvn clean package -DskipTests' 

            } 

        } 

 

        stage('Upload to Nexus') { 

            steps { 

                withCredentials([usernamePassword( 

                    credentialsId: 'nexus-admin', 

                    usernameVariable: 'USER', 

                    passwordVariable: 'PASS' 

                )]) { 

                    sh """ 

                    echo "Uploading JAR to Nexus..." 

                    curl -v -u $USER:$PASS --upload-file target/maven-demo-1.0.0.jar \ 

                    http://localhost:8081/repository/maven-releases/maven-demo-1.0.0.jar 

                    """ 

                } 

            } 

        } 

    } 

} 
