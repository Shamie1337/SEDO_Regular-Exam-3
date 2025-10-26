pipeline {
  agent any

  options {
    timestamps()
  }

  environment {
  PATH = "/usr/local/share/dotnet:/usr/local/bin:/opt/homebrew/bin:${PATH}"
}

  // Run only for 'main' branch
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
        sh 'dotnet --info'
      }
    }

    stage('Restore dependencies') {
      when { branch 'main' }
      steps {
        sh 'dotnet restore'
      }
    }

    stage('Build') {
      when { branch 'main' }
      steps {
        sh 'dotnet build --no-restore --configuration Release'
      }
    }

    stage('Test') {
      when { branch 'main' }
      steps {
        sh 'dotnet test --no-build --configuration Release --verbosity normal'
      }
    }
  }
}
