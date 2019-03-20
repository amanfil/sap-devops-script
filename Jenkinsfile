env.DISPLAY=":0"
node(label: 'master') {
    def BUILD_BRANCH = "dev" // this should eventually come from a parameter or evaluated based on the parameter
  	def MAJOR_MINOR = "${params.RELEASE_VERSION}" //eventually this may come from the version.txt file (or other) which is in the root
    def VERSION_IMAGE_LABEL = "${MAJOR_MINOR}.${BUILD_NUMBER}-${BUILD_BRANCH}" //use semantic versioning
    def LATEST_DOCKER_IMAGE_LABEL = "latest-dev"
    def IMAGE_NAME = "util-sonar-runner"
    def DOCKER_REPO = "docker"
    def WORKING_BRANCH = ""
	def STREAM = "${params.STREAM}"

    currentBuild.result = "SUCCESS"
    try {
		stage('Checkout'){
			branch = "${params.BRANCH_SPECIFIER}"
			WORKING_BRANCH = "${params.BRANCH_SPECIFIER}"
			echo "Branch Specifier is ${branch}"
			checkout([$class: 'GitSCM', branches: [[name: "${branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'a6e6d971-7ca6-4e96-8c2e-f173c57c5a0c', url: 'https://github.com/amanfil/sap-devops-script.git']]])
		}
		
	stage('Build Docker Image'){
     	 sh "logoutdocker"
      	 sh "logindocker"
      	 sh "cd ${workspace}"
	    
         sh "docker build -t ${DOCKER_REPO}/${IMAGE_NAME}:latest -f sonar-scanner/Dockerfile ."
      }
	    
      /*stage ('Tag Docker Image') {
      	    sh "docker tag ${DOCKER_REPO}/${IMAGE_NAME}:latest ${DOCKER_REPO}/${IMAGE_NAME}:latest"
	  }
   stage('Docker Image Upload to Artifactory'){
      sh "logoutdocker"
      sh "logindocker"
        {
            sh "docker push ${DOCKER_REPO}/${IMAGE_NAME}:latest"
          
        }
      sh "logoutdocker"
      sh "docker rmi -f ${DOCKER_REPO}/${IMAGE_NAME}:latest"
	}*/
}
    catch (err) {
        currentBuild.result = "FAILURE"
        throw err
    }

}
