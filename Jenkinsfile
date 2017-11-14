node {

    checkout scm

    //env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "hello-node-docker"
    registryHost = "127.0.0.1:30400/"
    //imageName = "${registryHost}${appName}:${tag}"
    imageName = "${appName}:${tag}"
    env.BUILDIMG=imageName

    stage "Build"
    
       //sh "docker build -t ${imageName} -f applications/hello-node-docker/Dockerfile applications/hello-node-docker"
       //sh "docker images"
    
    stage "Push"

       //sh "docker push ${imageName}"

    stage "Deploy"

        //sh "sed 's#127.0.0.1:30400/hello-kenzan:latest#'$BUILDIMG'#' applications/hello-kenzan/k8s/deployment.yaml | kubectl apply -f -"
        //sh "kubectl rollout status deployment/hello-kenzan"
	//sh "kubectl run hello-node-pod --image=gustavomr/hello_node:latest --port=8080"

	sh "kubectl set image deployment/hello-node-pod hello-node-pod=gustavomr/hello_node:v2"
}
