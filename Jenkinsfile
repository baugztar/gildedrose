node {
    stage('clone') {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'c2c71fab-e6c9-496c-94a0-c2beb41246d2', url: 'git@github.com:baugztar/gildedrose.git']]])
    }
    stage('build') {
        sh 'docker run -i --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn install'
    }
    stage('results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archive 'target/*.jar'
    }
    stage('javadoc') {
        sh 'docker run -i --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn site'
        archive 'target/*.jar'
        archive 'target/gildedrose-*.jar'
    }
}
