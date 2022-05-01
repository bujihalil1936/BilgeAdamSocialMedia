pipeline {
    agent any
    tools {
        jdk 'jdk'
       gradle 'Gradle 7.4.2'
       docker 'docker'
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
