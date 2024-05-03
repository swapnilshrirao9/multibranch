
pipeline{
   agent any
    parameters{
        string(name: 'person', defaultValue: 'Build', description: 'this for the test' )
    }
   stages{
        stage('gitpull'){
            steps{
                git branch: 'main', url: 'https://github.com/swapnilshrirao9/warfile.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
                sh 'pwd'
                sh 'ls -al'
                sh 'mkdir -p /var/jenkins_home/DATAFORWAR'
                sh 'cp -r target /var/jenkins_home/DATAFORWAR/target-$(date +"%T-%d-%m-%y")'
               
                sh 'ls -l /var/jenkins_home/DATAFORWAR'
                sh 'sleep 10'
            }
        }
              stage('Genrate sonarqube-analysis'){
            steps{
                withSonarQubeEnv(installationName: 'Sonar-jenkins'){
                    sh "mvn clean install  sonar:sonar  -Dsonar.login=admin -Dsonar.password=admin123 -Dsonar.projectKey=test-jenkins-war -Dsonar.projectName='test-jenkins-war'"
        	    }
            }
        }
        stage('Clean Workspace') {
            steps {
                script {
                    // Clean the workspace
                    cleanWs()

                    echo "Workspace cleaned successfully"
                }
            }
        }
        stage('parameters'){
            steps{
                sh 'echo "${person}"'
            }
        }
    }
 }
