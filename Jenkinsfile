pipeline {
    agent any
    stages {
        
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqubeServer') {
                    bat "mvn clean verify sonar:sonar"
                }
            }
        }
        stage("Quality gate") {
            steps {
                timeout(time: 2, unit: 'MINUTES'){
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        
    }
    post{
            success{
                bat "curl http://Kevin:123456@localhost:8080/job/Final/job/Desplegar_a_produccion/build?token=1234"
                bat "echo Tarea Desplegar en servidor de produccion Iniciada correctamente"
            }
            failure{
                bat "curl http://Kevin:123456@localhost:8080/job/Final/job/Notificar/build?token=4321"
                bat "echo Tarea notificar al correo Iniciada correctamente"
            }
        }
}
