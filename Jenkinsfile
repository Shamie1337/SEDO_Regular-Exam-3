pipeline {
  agent any

  // Trigger from GitHub webhook on every push
  triggers {
    githubPush()
  }

  stages {
    stage('Checkout') {
      when { branch 'main' }
      steps {
        checkout scm
      }
    }

    stage('Setup .NET') {
      when { branch 'main' }
      steps {
        sh 'dotnet --version'   
      }
    }

    stage('Restore') {
      when { branch 'main' }
      steps {
        sh 'dotnet restore'
      }
    }

    stage('Build') {
      when { branch 'main' }
      steps {
        sh 'dotnet build --configuration Release --no-restore'
      }
    }

    stage('Test') {
      when { branch 'main' }
      steps {
        sh 'dotnet test --configuration Release --no-build --verbosity normal'
      }
    }
  }
}