#!groovy

node {
   stage("Checkout"){
        // Checkout code from repository
        echo "setting properties"
        //properties([$class: PipelineTriggersJobProperty([[$class: 'GitHubPushTrigger'], pollSCM('H/15 * * * *')])])
        checkout scm
    }
   stage("Build"){

        def mvnHome = tool 'M3'
        //echo "${mvnHome}/bin:${env.PATH}"
        env.PATH = "${mvnHome}/bin:${env.PATH}" //Do I need this?
        // Run the maven build
        "run maven"
        sh "mvn clean install"
        step([$class: 'ArtifactArchiver', allowEmptyArchive: true, artifacts: '**/target/*.jar', fingerprint: true])
        step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
   }


   
}

// dockerNode(image: "maven:3.3.3-jdk-8") {
//   stage("Checkout SCM"){
//     checkout scm
//   }
//   stage("Unit Testing"){
//     sh 'mvn clean test'
//   }
//   stage("Deploy"){
//     sh 'mvn clean install'
//     step([$class: 'ArtifactArchiver', allowEmptyArchive: true, artifacts: '**/*.jar', fingerprint: true])
//     step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
//   }
//   stage("Coverage"){
//     step([$class: 'JacocoPublisher', execPattern: 'target/coverage-reports/jacoco.exec'])
//   }
//   stage('Analysis') {
//      sh "mvn -Dpmd.failOnViolation=false -Dcpd.failOnViolation=false -Dfindbugs.failOnError=false pmd:check pmd:cpd-check"
//      step([$class: 'PmdPublisher', pattern: 'target/pmd.xml'])
//      step([$class: 'DryPublisher', pattern: 'target/cpd.xml'])
//      step([$class: 'TasksPublisher', high: 'FIXME', low: '', normal: 'TODO', pattern: 'src/**/*.java'])
//   }
// }
//
// dockerNode(image: "maven:3.3.3-jdk-8", sideContainers: ["selenium/standalone-firefox"]) {
//   stage("Checkout"){
//     checkout scm
//   }
//   stage("Acceptance Testing"){
//     sh 'mvn clean test'
//   }
// }
