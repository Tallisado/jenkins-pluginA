#!/usr/bin/env groovy

@NonCPS
def printEach(text) {
  text.split("\r?\n").each {
    println it
  }
}

dockerNode(image: "maven:3.3.3-jdk-8") {
  stage("Checkout"){
    // sh 'whoami'
    // sh 'ls ~/.ssh'
    checkout scm

    // git branch: 'master', credentialsId: '20686e54-62d6-423d-aedf-505f68e72094', url: 'git@github.com:tallisado/jenkins-pluginA.git'

    sshagent(['4e882e06-498a-46c3-a2f4-75eb42fdf56b']) {
      sh 'echo SSH_AUTH_SOCK=$SSH_AUTH_SOCK'
      sh 'ls -al $SSH_AUTH_SOCK || true'

      sh 'git remote set-url origin git@github.com:tallisado/jenkins-pluginA.git'

      sh "git tag 'l33t-build'"
      sh 'git push --tags'
    }

    // GIT_COMMIT_REVISION = sh (
    //     script: 'git rev-parse HEAD',
    //     returnStdout: true
    // ).trim()
    //
    // echo "Git REVISION: ${GIT_COMMIT_REVISION}"
    //
    // sh 'git tag "l33t build'
    // sh 'git push --tags'

    // ches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/jglick/simple-maven-project-with-tests']]]


    // sh 'echo $env.BRANCH_NAME'
    // sh 'git rev-parse --abbrev-ref HEAD > GIT_BRANCH;
    //     git_branch = readFile('GIT_BRANCH').trim();
    //     echo $git_branch;
    //    '
    // checkout scm: [$class: 'GitSCM', bran
    // ches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/jglick/simple-maven-project-with-tests']]]
    echo "${BRANCH_NAME} ${env.BRANCH_NAME}"
    sh 'env'
    sh 'env > env.txt'
    sh 'cat env.txt'
    // printEach(readFile('env.txt'))


  }
  stage("Build"){
//     sh "git config --global user.email 'tvanek@klipfolio.com'"
//     sh "git config --global user.name 'Tallis Vanek'"
//     sh "git clean -f && git reset --hard origin/master"
//     def pom = readMavenPom file: 'pom.xml'
//     def version = pom.version.replace("-SNAPSHOT", ".${currentBuild.number}")
//     def PWD = pwd();
//     // sh 'ls -al /usr/share/maven/conf/settings.xml || true'
//     // sh 'cp settings.xml -al /usr/share/maven/conf/settings.xml || true'
//     // sh 'cat /usr/share/maven/conf/settings.xml'
// // -DaltDeploymentRepository=jenkins::default::url
// // -DaltDeploymentRepository=id::layout::http://159.203.16.201:8080/plugin/repository/
//     sh "mvn --settings ${PWD}/settings.xml --global-settings ${PWD}/settings.xml -DreleaseVersion=${version} -DdevelopmentVersion=${pom.version} -DpushChanges=false -DlocalCheckout=true -DpreparationGoals=initialize release:prepare -B"
//     sh "mvn --settings ${PWD}/settings.xml --global-settings ${PWD}/settings.xml -DreleaseVersion=${version} -DdevelopmentVersion=${pom.version} -DpushChanges=false -DlocalCheckout=true -DpreparationGoals=initialize release:perform -B"


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
    // def pom = readMavenPom file: 'pom.xml'
    // def version = pom.version.replace("-SNAPSHOT", ".${currentBuild.number}")
    //
    // sh 'whoami'
    // sh 'cat .git/config'
    // sh 'git remote set-url origin git@github.com:tallisado/jenkins-pluginA.git'
    // // sh "git push master ${pom.artifactId}-${version}"
    // sh 'git push --tags'

    // EG: java-archive-2.20.86

    // sh "git name-rev --tags --name-only $(git rev-parse HEAD)"
    // sh "git status"
    // sh "git branch temp-branch"
    // sh "git checkout master"
    // sh "git merge temp-branch"
    // sh "git push origin master"
  }

  // stage("Downstream Applications"){
  //   build job: 'jenkins-appA', parameters: [[$class: 'StringParameterValue', name: 'target', value: "GG"]]
    // http://159.203.16.201:8080/job/tallisado/job/jenkins-appA/master
  // }

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
