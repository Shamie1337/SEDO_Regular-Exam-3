pipeline {
  agent any
  triggers { githubPush() }

  environment { IS_MAIN = "${env.BRANCH_NAME == 'main' || env.GIT_BRANCH == 'origin/main'}" }

  stages {
    stage('Checkout') {
      when { expression { return env.IS_MAIN.toBoolean() } }
      steps { checkout scm }
    }
    stage('Setup .NET') {
      when { expression { return env.IS_MAIN.toBoolean() } }
      steps { sh 'dotnet --version' }
    }
    stage('Restore') {
      when { expression { return env.IS_MAIN.toBoolean() } }
      steps { sh 'dotnet restore' }
    }
    stage('Build') {
      when { expression { return env.IS_MAIN.toBoolean() } }
      steps { sh 'dotnet build --configuration Release --no-restore' }
    }
    stage('Test') {
      when { expression { return env.IS_MAIN.toBoolean() } }
      steps { sh 'dotnet test --configuration Release --no-build --verbosity normal' }
    }
  }
}
