node{
    stage('git_codecheckout')
    {
        git branch: 'master', url: 'https://github.com/Arshiyaz/arshiya_insureme.git'
    }

    stage('insureme_build'){
    
    sh 'mvn clean package'   
    }
    stage('insureme_compile'){
        sh 'mvn compile'
    }
    stage('insureme_dockerimagebuild')
    {
    sh 'sudo docker build -t arshiya13/insureme .'
   
    }
    stage('docker image push to registry')
    {
    
    withCredentials([string(credentialsId: 'dockerid', variable: 'dockervar')]) {
        sh 'sudo docker login -u arshiya13 -p ${dockervar}'
        sh 'sudo docker push arshiya13/insureme'
    
}
    }
    stage('deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'ansibleid', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}
