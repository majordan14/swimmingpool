pipeline {
    agent any
    /* insert Declarative Pipeline here */
    stages {
        stage('run-test') {
            /* when {
                anyOf {
                    branch 'master'
                    branch 'dev'
                }
            } */
            stage('sonarqube-analysis') {
            environment {
                SONAR_TOKEN = credentials('{sonarcube-token}')
            }
            steps{
                sh '''./gradlew sonarqube \
                   -Dsonar.projectKey={D0977701swimmingkey} \
                   -Dsonar.host.url=http://140.134.26.54:10990 \
                   -Dsonar.login=$253e164e51a59cb35354ff25df09f8eba7b39e80
            }
            
            steps {
                sh 'chmod +x ./gradlew'
                sh './gradlew test'
                jacoco(
                    classPattern: 'app/build/classes',
                    inclusionPattern: '**/*.class',
                    exclusionPattern: '**/*Test*.class',
                    execPattern: 'app/build/jacoco/**/*.exec'
                )
            }
        }
    }
}
