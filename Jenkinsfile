node('master'){
   
   stage('Git checkout'){
                  git 'https://github.com/Rajivshetty/Inglibrary.git'
              }
   
   stage('Code analysis'){
             sh '/opt/maven/bin/mvn clean verify sonar:sonar -Dsonar.password=admin -Dsonar.login=admin'
         }
   stage('Build'){
             sh '/opt/maven/bin/mvn clean install'
         }

   stage('Execution'){
             sh 'export JENKINS_NODE_COOKIE=dontKillMe ;nohup java -Dspring.profiles.active=dev -jar $WORKSPACE/target/*.jar &'
         }
   
   stage('Deploy'){
             sh '/opt/maven/bin/mvn clean deploy '
         }
}
