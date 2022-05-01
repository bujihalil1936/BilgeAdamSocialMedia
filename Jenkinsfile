pipeline {
    agent any
    tools {
        jdk 'jdk'
     }
    stages {
        stage("build project") {
            steps {
                    gradle {
                    tasks 'build'
                    options '--stacktrace'
                    gradleOptions '-Pproject.version=${env.BUILD_NUMBER}'
                }
                echo "Java VERSION"
                sh 'java -version'
                echo 'building project...'


            }
        }
    }
}
   
    stage("Dockerfile build"){
        sh 'Dockerfile build -t jhooq-docker-demo .'
        sh 'docker image list'
        sh 'docker tag jhooq-docker-demo bujihalil/jhooq-docker-demo:jhooq-docker-demo'
    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u bujihalil -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  bujihalil/jhooq-docker-demo:jhooq-docker-demo'
    }
    
    stage("kubernetes deployment"){
        sh 'kubectl apply -f .'
        
    }

