pipeline{
  agent any
	  stages{
		stage("Cloning Git"){
		  steps{
			echo 'Cloning Repo...'
			git credentialsId: '56925a7e-0ac9-441f-9e4a-51abb553e65f', url: 'https://github.com/ynsaiyadav/ass4_1.git'
		  }
		}
		stage('Archive artifacts') {
		  steps{
			script{
				archiveArtifacts artifacts: 'template/template.php', onlyIfSuccessful: true
			}
		  }
		}
	}
}
