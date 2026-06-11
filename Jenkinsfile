pipeline {
agent any

```
stages {

    stage('Clone') {
        steps {
            echo 'Repository cloned successfully'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t flask-app:${BUILD_NUMBER} .'
        }
    }

    stage('List Docker Images') {
        steps {
            sh 'docker images'
        }
    }
}
```

}
