node    {
    def app


    stage('Clone repository') {
        checkout scm
    }

        stage("Package jar file with Maven"){
            dir('UserRegistrationManagement'){
                sh "mvn clean package -DskipTests=true"
            }
        }
stage('Deploy to Server') {
         dir('UserRegistrationManagement'){
        sh """
          sudo scp -o StrictHostKeyChecking=no target/*.jar /home/ubuntu/backend/app.jar
           << EOF
                sudo systemctl stop backend-app || true
                sudo mv /home/ubuntu/backend/app.jar /opt/backend/app.jar
                sudo systemctl start backend-app
            EOF
        """
        }
    }
}
