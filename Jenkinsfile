#!groovy

dockerNode(image: "maven:3.3.3-jdk-8") {
  stage("Checkout"){
      checkout scm
  }
  stage("Build"){
    sh "git config --global user.email 'tvanek@klipfolio.com'"
    sh "git config --global user.name 'Tallis Vanek'"
    sh "git clean -f && git reset --hard origin/master"
    def pom = readMavenPom file: 'pom.xml'
    def version = pom.version.replace("-SNAPSHOT", ".${currentBuild.number}")
    def PWD = pwd();
    // sh 'ls -al /usr/share/maven/conf/settings.xml || true'
    // sh 'cp settings.xml -al /usr/share/maven/conf/settings.xml || true'
    // sh 'cat /usr/share/maven/conf/settings.xml'
// -DaltDeploymentRepository=jenkins::default::url
// -DaltDeploymentRepository=id::layout::http://159.203.16.201:8080/plugin/repository/
    sh "mvn --settings ${PWD}/settings.xml --global-settings ${PWD}/settings.xml -Pjenkins -DreleaseVersion=${version} -DdevelopmentVersion=${pom.version} -DpushChanges=false -DlocalCheckout=true -DpreparationGoals=initialize release:prepare release:perform -B"


    // sh "mvn -Pupstream clean deploy"


    // sh 'cp settings.xml  /usr/share/maven/ref/settings.xml'
    // withMaven(mavenLocalRepo: '.repository',  mavenSettingsConfig: "settings.xml", mavenSettingsFilePath: "/usr/share/maven/conf/") {
    //   // Run the maven build
    //   sh "mvn -DreleaseVersion=${version} -DdevelopmentVersion=${pom.version} -DpushChanges=false -DlocalCheckout=true -DpreparationGoals=initialize release:prepare release:perform -B"
    //
    //
    //   // sh "mvn -Pupstream clean deploy"
    // }

    // step([$class: 'ArtifactArchiver', allowEmptyArchive: true, artifacts: '**/target/*.jar', fingerprint: true])
    // step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
  }
  stage("Publish"){
    sh "git push ${pom.artifactId}-${version}"
  }

  //  stage ('Triggering application level upstreams') {
  //     build job: 'jenkins-appA', parameters: [[$class: 'StringParameterValue', name: 'systemname', value: systemname]]
  //  }
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
