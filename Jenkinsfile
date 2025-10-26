pipeline {
  agent any
  triggers { githubPush() }

  options { timestamps() }

  environment {
    IS_MAIN = "${env.BRANCH_NAME == 'main' || env.GIT_BRANCH == 'origin/main'}"
  }

  stages {
    stage('Checkout') {
      when { expression { env.IS_MAIN.toBoolean() } }
      steps { checkout scm }
    }
    stage('Setup .NET') {
      when { expression { env.IS_MAIN.toBoolean() } }
      steps { sh 'dotnet --info' }
    }
    stage('Restore dependencies') {
      when { expression { env.IS_MAIN.toBoolean() } }
      steps { sh 'dotnet restore' }
    }
    stage('Build') {
      when { expression { env.IS_MAIN.toBoolean() } }
      steps { sh 'dotnet build --configuration Release --no-restore' }
    }
    stage('Test') {
      when { expression { env.IS_MAIN.toBoolean() } }
      steps { sh 'dotnet test --configuration Release --no-build --verbosity normal' }
    }
  }
}
