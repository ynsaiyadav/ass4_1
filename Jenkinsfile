pipeline{
  agent any
  environment{
	imagename = "ynsaiyadav/ass4_1"
	dockerImage = ''
  }
	  stages{
		stage("Cloning Git"){
		  steps{
			echo 'Cloning Repo...'
			git credentialsId: '56925a7e-0ac9-441f-9e4a-51abb553e65f', url: 'https://github.com/ynsaiyadav/ass4_1.git'
		  }
		}
		stage('Building image') {
			steps{
				script {
					dockerImage = docker.build imagename + ":$BUILD_NUMBER"
				}
			}
		}
		stage('Deploy Image') {
			steps{
				script {
					docker.withRegistry( 'https://registry.hub.docker.com', 'dockerHub' ) {
						dockerImage.push("$BUILD_NUMBER")
						dockerImage.push('latest')
					}
				}
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
		stage('Remove Unused docker image') {
			steps{
				script{
					sh "docker rmi -f $imagename:$BUILD_NUMBER"
					sh "docker rmi -f $imagename:latest"
					sh 'docker stop $(docker ps -a -q)'
					sh "docker container ls"
					sh "docker ps"
				}
			}
		}
	}
}

