pipeline { 

    agent any 

 

    stages { 

        stage('Build') { 

            steps { 

                // build the JAR from pom.xml 

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

                    sh ''' 

                        echo "Listing target directory..." 

                        ls -R 

 

                        if [ -f target/maven-demo-1.0.0.jar ]; then 

                          echo "Uploading JAR to Nexus..." 

                          curl -v -u "$USER:$PASS" \ 

                            --upload-file target/maven-demo-1.0.0.jar \ 

                            http://localhost:8081/repository/maven-releases/com/example/maven-demo/1.0.0/maven-demo-1.0.0.jar 

                        else 

                          echo "JAR not found in target/" 

                          ls target || true 

                          exit 1 

                        fi 

                    ''' 

                } 

            } 

        } 

    } 

} 
