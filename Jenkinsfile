node {

    checkout scm

    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "gustavomr/hello-node"
    registryHost = "127.0.0.1:30400/"
    //imageName = "${registryHost}${appName}:${tag}"
    imageName = "${appName}:${tag}"
    //imageName = "${appName}:v2"
    env.BUILDIMG=imageName

    stage "Build"
       sh "echo ${imageName}"
       //sh "docker login"
       //sh "docker build -t ${imageName} ."
	def image = docker.build("${imageName}")
	image = docker.build("${appName}:latest")
       //sh "docker images"
    
    stage ("Push") {
		docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
	       		//sh "docker push ${imageName}" 
			image.push()
		} 
	}

    stage "Deploy"

        //sh "sed 's#127.0.0.1:30400/hello-kenzan:latest#'$BUILDIMG'#' applications/hello-kenzan/k8s/deployment.yaml | kubectl apply -f -"
        //sh "kubectl rollout status deployment/hello-kenzan"
	//sh "kubectl run hello-node-pod --image=gustavomr/hello_node:latest --port=8080"

	sh "kubectl set image deployment/hello-node-pod hello-node-pod=${imageName} --kubeconfig=admin.conf"
	    
}
