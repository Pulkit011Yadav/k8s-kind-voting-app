@Library("Jenkins_shared_library")_
pipeline{
    agent { label 'worker' }
    stages{
        stage("code clone"){
            steps{
                codeclone("https://github.com/Pulkit011Yadav/k8s-kind-voting-app.git" , "main")
            }
        }
        stage("pull"){
            steps{
                dockerpull("pulkit011yadav/votingapp-vote" , "latest")
                dockerpull("pulkit011yadav/votingapp-result" , "latest")
                dockerpull("pulkit011yadav/votingapp-worker" , "latest")
            }
        }
        stage("deploy"){
            steps{
                dockerdeploy()
            }
        }
    }
}
