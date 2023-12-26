def buildNumber = Jenkins.instance.getItem('cicd-jenkins-bean-stage').lastSuccessfulBuild.number


pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK11"
    } 

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'Amit@0135'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUSIP = '172.31.49.10' 
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group' 
        NEXUS_LOGIN = 'nexuslogin'
        SONARSERVER = 'sonarserver'
        SONARSCANNER = 'sonarscanner'
        ARTIFACT_NAME = "vprofile-v${buildNumber}.war"
        AWS_S3_BUCKET = 'vprocicdbean201620'
        AWS_EB_APP_NAME = 'vpro-app'
        AWS_EB_ENVIRONMENT = 'Vpro-app-prod'
        AWS_EB_APP_VERSION = "${buildNumber}"        
    }

    stages {

        stage('Deploy to prod-env Bean'){
          steps {
            withAWS(credentials: 'awsbeancreds', region: 'us-east-1') {
               sh 'aws elasticbeanstalk update-environment --application-name $AWS_EB_APP_NAME --environment-name $AWS_EB_ENVIRONMENT --version-label $AWS_EB_APP_VERSION'
            }
          }
        }

    }


    }

    
