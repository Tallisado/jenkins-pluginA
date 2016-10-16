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
    // checkout scm

    /*

    RUN mkdir -p /root/.ssh
    ADD id_rsa /root/.ssh/id_rsa
    RUN chmod 700 /root/.ssh/id_rsa
    RUN echo "Host github.com\n\tStrictHostKeyChecking no\n" >> /root/.ssh/config

    */

    git branch: 'master', credentialsId: '4e882e06-498a-46c3-a2f4-75eb42fdf56b', url: 'git@github.com:tallisado/jenkins-pluginA.git'
    sh 'cat .git/config'
    sh 'mkdir /root/.ssh'
    sh 'touch /root/.ssh/config'
    sh 'touch /root/.ssh/id_rsa_github'
    sh 'echo "Host github.com\n\tStrictHostKeyChecking no\n" >> /root/.ssh/config'

    key = """
    -----BEGIN RSA PRIVATE KEY-----
    MIIEpAIBAAKCAQEA0BWCT1Fy2sJ3BWTuuklJgbMhaExLi+jwUCfoK0lqNuO/mCAX
    W6myNf7Tetz/piMeBJLZ5j9WIdT3pruQYDpSkcK6IV5KXuRepgV7JTBGa+9tuY94
    y66tFGACHFx3SOUJsQMiwSAp5ZlTE6fQhiW4OVYNK8diyPsTgNpP/nxgkjWk7qao
    1pRIrrK2i3QUxQUw4dUILfo7gHq1+0Kf9+n9BOYZlT2xUjfDCnxK+gpyq9NdXAnN
    5xKYhXGVd7UCmnSIFQEDol4rtA1PNHgMCRV7+y5CWin1HfG/aI8HlTu4bE2O3bBH
    lnsemA6Bq+3pt94G3vmwG583S3NdJxt5wPl4MQIDAQABAoIBAQCf8ZiLbXjSTB3+
    iHmzuTeGOXGZYOPE9FUb18Du3OyGqoMP5MLvkz3HoUtfKlZblqyxKUvSXqbPNIrz
    n0K3pLzpC3vUwEx8Kh/Sj237xOKsfoqh0nUwYuDpQ27769tIrbzIUje5qQZrVHJ2
    LkzrgDzd3ZYcK5N0FwIDzkskuufkGXJ4pxWi7BvzdUSqYOnMDEbzyHRaGhxm0kim
    UHSToBUnbNTGnXMU2yxobhDzP04zw8HQGkTGQO9d7FQG8FBRdwwdJsn1w0fPEluR
    QxFhAKWRbtiwqTF3QYyYVKTXkAxSg3eFEigmKAG12ES+Oju4WT17bktJTzPIdhnM
    WirpurotAoGBAPR7zxNzeqy1Sz1nM9ES5RqYC8nYeIUvp1J1XdI2dJreYRIo1GZ+
    wVPLB8ptmOe9U1ttSDCDaJRhkBxj/hDebpwIm4Q/SoO+t03naRweo5Vs3lLJQ9qa
    x54RhyyqsJwekiX30cnVRnhaoKyNXpm2tI0Lns/fUlAW8yah96HtRitbAoGBANni
    w0PDBunloSROcBq7HWTHE/OcuhpxyIqn1H8bp1BlmJkrcX2sf58LhqXKyrjxU2VU
    eEda/FmIJJBzy83aNndkiYXEXkaNUvuyl1jTbc6J28DLenQNi1O/b9MWyryB2lu3
    xeDn4hMRvXulKfHEpva4PofVRIxNUPchpFZTZlxjAoGBANQxVRQryVB29Xuww/91
    Z9WCG9EvicMHDjF6XljiHKiB1Dx/pYHkCAWjFPrzzp9r6hpTKjG5DB6k4wBRJSUc
    +WGB8wCAMjtQXyZFcCwQx6gcWoX921+zsQeXbPwulaSav/wmMDX+XvB8sDGzbWT6
    d5Bngoom6PlMQfPI5fXry1g7AoGAQkvaSDL+Vor1Vhu7xpZqojBk5LoqckNu1qms
    YaSjazYOkYSDes7S4izaonWq600ap/lkw6luoTtojL9/Irqj2f4wThBq8yKrPkSg
    AnoKrk6KHAaN0uQQIcJdHyiPNX55V3D6d612v4ClXArsUVEZ0HZNKH1+5wXbfeax
    n0avHasCgYAGypFA7sgQlvJbymoIsW/ltgtBMuAl/IjwmBLt778QbMe0n+IBGddH
    dzb6VqskVCEmX9+qkiYGeaJAHCMsOSPobpE0DI9aV+RxTznyRpBfVOldWL56aK0L
    9gGCC7/T4V4aQYquTj93wpQqTQAXMJ+KBUULxoZGDNkwJQBMsbWTIQ==
    -----END RSA PRIVATE KEY-----"""

    echo "Dropping SSH RSA: ${key}"
    sh "echo \"${key}\" > ~/.ssh/id_rsa_github"
    sh 'cat ~/.ssh/id_rsa_github'
    sh 'eval `ssh-agent`'
    sh 'ssh-add ~/.ssh/id_rsa_github'
    sh 'ssh-add -l'
    sh "git tag 'l33t-build'"
    // // sh 'rm -rf ~/.ssh/known_hosts'
    sh "git push --tags"



    // sshagent(['4e882e06-498a-46c3-a2f4-75eb42fdf56b']) {
    //   sh 'echo SSH_AUTH_SOCK=$SSH_AUTH_SOCK'
    //   sh 'ls -al $SSH_AUTH_SOCK || true'
    //
    //   sh 'git remote set-url origin git@github.com:tallisado/jenkins-pluginA.git'
    //
    //   sh "git tag 'l33t-build'"
    //   sh 'git push --tags'
    // }

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
