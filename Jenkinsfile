node{

   def tomcatWeb = 'C:\\apache-tomcat-8.5.64\\webapps'
   def tomcatBin = 'C:\\apache-tomcat-8.5.64\\bin'
   def CATATINA_HOME = 'C:\\apache-tomcat-8.5.64'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/ManuelKumar/jenkinswar.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'   
      bat "${mvnHome}/bin/mvn package"
      }
   stage('SonarQube Analysis') {
		def mvnHome = tool name:'maven-3', type: 'maven'
		withSonarQubeEnv('sonar-1') {
		bat "${mvnHome}/bin/mvn sonar:sonar"
		}	
    		//echo  Sonar Run Complete
	}
   
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.bat"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
     bat "copy target\\jenkinswar.war \"${tomcatWeb}\\jenkinswar.war\""
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
         bat "${tomcatBin}\\startup.bat"
         sleep(time:100,unit:"SECONDS")
   }
}
