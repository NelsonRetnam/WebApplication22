node{
    stage("Git Clone"){
        git credentialsId: 'Github-Credentials', url: 'https://github.com/NelsonRetnam/WebApplication22.git'
    }
    stage("Maven Clean Build"){
        sh 'dotnet restore WebApplication22.sln'
    }
    stage("Build Docker Image"){
        sh "pwd"
        sh "docker build -t nelson6r/webapplication22 -f WebApplication22/Dockerfile ."
    }
    stage("Docker Push"){
        withCredentials([string(credentialsId: 'Dockerhub_Credentials', variable: 'Dockerhub_Credentials')]) {
            sh "docker login -u nelson6r -p ${Dockerhub_Credentials}"
        }
        sh "docker push nelson6r/webapplication22 "
    }
    stage("Deploy in k8s"){
        kubernetesDeploy(
                configs: 'WebApplication22/deployment.yml',
                kubeconfigId: 'Kubernetes_Cluster_Config',
                enableConfigSubstitution: true
            )
    }
}
