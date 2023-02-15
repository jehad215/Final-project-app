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
                        cd backend-app
                        gcloud auth activate-service-account --key-file=${config}
                        gcloud container clusters get-credentials cluster-pv --zone us-east4-c --project jehad-iti
                        sed -i 's/tag/${BUILD_NUMBER}/g' deployment/deployment.yaml
                        kubectl apply -Rf deployment
                    """
                }
            }
 
        }
    }
}