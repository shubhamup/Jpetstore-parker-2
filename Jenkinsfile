node {
        def majorVersion="2.0.${BUILD_NUMBER}"
	currentBuild.displayName = majorVersion
       // def BUILD_NUMBER="2.0.${BUILD_NUMBER}"
	//currentBuild.displayName = "2.0.${BUILD_NUMBER}"
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
	
  }


