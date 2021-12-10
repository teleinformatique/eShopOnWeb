pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'dotnetBuild eShopOnWeb.sln'
        withDotNet(sdk: 'dotnetsdk')
      }
    }

    stage('Unit') {
      parallel {
        stage('Tests') {
          steps {
            sh 'dotnet test tests/UnitTests'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet publish eShopOnWeb -o  /Users/khadim/Projects/aspnet'
      }
    }

  }
}