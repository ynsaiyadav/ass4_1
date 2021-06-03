pipeline{
  agent any
	  stages{
		stage("Cloning Git"){
		  steps{
			echo 'Cloning Repo...'
			git credentialsId: '56925a7e-0ac9-441f-9e4a-51abb553e65f', url: 'https://github.com/ynsaiyadav/ass4_1.git'
		  }
		}
		stage('Archive artifacts, pull image and containerize') {
		  steps{
			script{
				archiveArtifacts artifacts: 'template/template.php', onlyIfSuccessful: true
				sh "docker pull $imagename:$BUILD_NUMBER"
				sh "docker images"
				sh "docker container run -d $imagename:$BUILD_NUMBER"
				sh "docker container ls"
			}
		  }
		}
	}
}
