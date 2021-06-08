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
		stage('sonarqube-analysis') {
			environment{
				SONAR_TOKEN = credentials('{hw73}')
			}
			steps{
				sh '''./gradlew sonarqube \
				  -Dsonar.projectKey=team20_price \
				  -Dsonar.host.url=http://140.134.26.54:10990 \
				  -Dsonar.login=7b031ce550a92c3049d58e5a02b125f574480f2d
				'''
			}
		}
    }
}
