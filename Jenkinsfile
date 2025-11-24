@Library("Jenkins_shared_library")_
pipeline{
    agent { label "dev" }
    stages{
        stage("code clone"){
           steps{
               codeclone("https://github.com/Pulkit011Yadav/k8s-kind-voting-app.git" , "main")
           }
        }
        stage("docker build"){
            steps{
                dockerbuild("votingapp-vote" ,"latest" , "vote" , "vote/Dockerfile")
                dockerbuild("votingapp-worker" ,"latest" , "worker" , "worker/Dockerfile")
                dockerbuild("votingapp-result" ,"latest" , "result" , "result/Dockerfile")
            }
        }
        stage("docker push"){
            steps{
                dockerpush("dockerhub_creds" , "votingapp-vote" ,"latest")
                dockerpush("dockerhub_creds" , "votingapp-worker" ,"latest")
                dockerpush("dockerhub_creds" , "votingapp-result" ,"latest")
            }
        }
        stage("docker pull"){
            steps{
                dockerpull("pulkit011yadav/votingapp-vote" , "latest")
                dockerpull("pulkit011yadav/votingapp-result" , "latest")
                dockerpull("pulkit011yadav/votingapp-worker" , "latest")
            }
        }
        stage("deploy"){
            steps{
                sh "docker compose -f docker-compose.yml down || true"
                sh "docker compose -f docker-compose.yml up -d --force-recreate"
                sh "echo 'deploying is successfull'"
            }
        }
    }
}
