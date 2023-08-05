node{
    stage('code checkout'){ 
        echo 'checkhing out the application code'
        git branch: 'main', url: 'https://github.com/upretimokshada/Practice.git'  
    }
    
    stage('code build'){
        echo 'buildig aoolication...compile..test...package'
        sh 'mvn clean package'   
    }
    
    stage('containerize app'){
        echo "Creating docker image for insureme"
        sh 'docker build -t upretimokshada/insure-me:3.0 .'
    }
    
    stage('push image to dockerHub'){
        echo 'pushing insure-me images to docker hub'
        withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerHubPwd')]) {
            sh "docker login -u upretimokshada -p ${dockerHubPwd}"
            sh 'docker push upretimokshada/insure-me:3.0'
       }
    }
}
