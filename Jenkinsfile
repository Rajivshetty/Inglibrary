node('master'){
   
   stage('Git checkout'){
                  git 'https://github.com/Rajivshetty/Inglibrary-backend.git'
              }
   
   stage('Build'){
             sh '/opt/maven/bin/mvn clean verify sonar:sonar'
         }
   
   stage('Code analysis'){
                  withSonarQubeEnv('sonar') 
                  {
                        sh '/opt/maven/bin/mvn clean package sonar:sonar -Dsonar.password=admin -Dsonar.login=admin'
                  }
         }
  
   stage("Quality Gate"){
                  timeout(time: 30, unit: 'SECONDS') 
                  { 
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') 
                        {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                  }
   
   stage('Deploy'){
             sh '/opt/maven/bin/mvn clean deploy '
         }
      
      stage('Execution'){
             sh 'export JENKINS_NODE_COOKIE=dontKillMe ;nohup java -Dspring.profiles.active=dev -jar $WORKSPACE/target/*.jar &'
         }
}
