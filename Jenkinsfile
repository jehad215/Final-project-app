pipeline {
    agent any

    stages {

        stage('CI'){
            steps {

                withCredentials([usernamePassword(credentialsId: 'Dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')])            {

                sh """
                    cd backend-app
                    docker build . -t jehad21/app:v$BUILD_NUMBER
                    docker login -u ${USERNAME} -p ${PASSWORD}
                    docker push jehad21/app:v$BUILD_NUMBER
                    cd ..
                """
                }
              }
        }

        stage('CD'){
            steps {

                withCredentials([file(credentialsId: 'svc', variable: 'config')]){
                    sh """
                        gcloud auth activate-service-account --key-file=${config}
                        gcloud container clusters get-credentials private-cluster --zone us-east4-b --project mahmoud-ibrahim-2023
                        sed -i 's/tag/${BUILD_NUMBER}/g' deployment/deployment.yaml
                        kubectl apply -Rf deployment
                    """
                }
            }
 
        }
    }
}