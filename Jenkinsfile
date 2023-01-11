node {
        def majorVersion="1.0.${BUILD_NUMBER}"
	currentBuild.displayName = majorVersion
       // def BUILD_NUMBER="1.0.${BUILD_NUMBER}"
	//currentBuild.displayName = "1.0.${BUILD_NUMBER}"
	def GIT_COMMIT
  stage ('cloning the repository'){
	  
      def scm = git 'https://github.com/shubhamup/Jpetstore-parker-2'
	   GIT_COMMIT = sh(returnStdout: true, script: "@echo off | git rev-parse HEAD").trim()
	// GIT_COMMIT = sh(returnStdout: true, script: "@echo off | git rev-parse HEAD").trim()
	  echo "COMMITID ${GIT_COMMIT}"
	  //echo "BBBB ${scm}"
	  //GIT_COMMIT = scm.GIT_COMMIT
	   //echo "**** ${GIT_COMMIT}"
	  
  }
	
 
  stage ('Build') {
      withMaven(maven: 'Maven3.8.6') {
      sh 'mvn clean package'
	      echo "****${GIT_COMMIT}"
	//step($class: 'UploadBuild', tenantId: "5ade13625558f2c6688d15ce", revision: "${GIT_COMMIT}", appName: "JPetStore", requestor: "admin", id: "${newComponentVersionId}" )
	
	     
    }
  }
  
  stage ('Junit Testcase'){
  withMaven(jdk: 'java1.8', maven: 'Maven3.6.0') {
      sh 'mvn test -Dtest=Runner'	     
    }
  }
	
	stage('SonarQube Analysis'){
	//	def mvnHome = tool name : 'Maven3.6.0', type:'maven'
		//def path = tool name: 'gradle-4.7', type: 'gradle'
		
		withSonarQubeEnv('sonar-server'){
			 //"SONAR_USER_HOME=/opt/bitnami/jenkins/.sonar ${mvnHome}/bin/mvn sonar:sonar"
		//	sh  "mvn sonar:sonar -Dsonar.projectName=JpetStore-velocity"
			//sh "${path}/bin/gradle --info -Dsonar.host.url=http://localhost:9000 sonarqube"
		}
	}
	
	
	
echo "(*******)"
stage('Publish Artificats to UCD'){	
  step([$class: 'UCDeployPublisher',
	        siteName: 'UCD',
	        component: [
	            $class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
	            componentName: 'LTFS_IIB_Deploy',
	            createComponent: [
	                $class: 'com.urbancode.jenkins.plugins.ucdeploy.ComponentHelper$CreateComponentBlock',
	                componentTemplate: '',
	                componentApplication: 'LTFS_IIB_Deploy'
	            ],
	            delivery: [
	                $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeliveryHelper$Push',
	                pushVersion: '1.0.${BUILD_NUMBER}',
	                //baseDir: '/var/jenkins_home/workspace/JPetStore/target',
			 baseDir: 'D:/Installables/Jenkins/workspace/Velocity/Jpetstore/JPetStore-velocity/target/',
	                fileIncludePatterns: '*.war',
	                fileExcludePatterns: '',
	               // pushProperties: 'jenkins.server=Jenkins-app\njenkins.reviewed=false',
	                pushDescription: 'Pushed from Jenkins'
	            ]
	        ]
     ])
	  
          echo "(*******)"
	  echo "Demo1234 ${LTFS_IIB_Deploy_VersionId}"
	  def newComponentVersionId = "${LTFS_IIB_Deploy_VersionId}"
	  echo "git commit ${GIT_COMMIT}"

         step($class: 'UploadBuild', 
         tenantId: "5ade13625558f2c6688d15ce", 
         revision: "${GIT_COMMIT}", 
         appName: "LTFS_IIB_Deploy", 
         requestor: "admin", 
         id: "${newComponentVersionId}", 
         versionName: "1.0.${BUILD_NUMBER}"
      )
}
	//stage ('Deploy to DEV') {
//	step([$class: 'UCDeployPublisher',
//		deploy: [ createSnapshot: [deployWithSnapshot: true, 
//			 snapshotName: "2.0.${BUILD_NUMBER}"],
//			 deployApp: 'JPetStore-velocity', 
//			 deployDesc: 'Requested from Jenkins', 
//			 deployEnv: 'JPetStore-velocity_Dev', 
//			 deployOnlyChanged: false, 
//			 deployProc: 'Deploy-JpetStore-velocity', 
//			 deployReqProps: '', 
//			 deployVersions: "JPetStorevelocityComponent:2.0.${BUILD_NUMBER}"], 
//		siteName: 'UCD_Local'])
 //}
	
	


}
