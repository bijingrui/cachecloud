pipeline {
  agent any
  stages {
    stage('gitCode') {
      agent any
      steps {
        sh 'cd /data/cachecloud-master'
      }
    }
    stage('ConfigFile') {
      steps {
        sh 'echo "cp config file to profile local"'
      }
    }
    stage('Build') {
      steps {
        sh 'cd /data/cachecloud/cachecloud/ && mvn clean compile install -Ponline'
      }
    }
    stage('runCheck') {
      parallel {
        stage('CheckParmFromFile') {
          steps {
            sh 'mkdir /data/cachecloud-web -p && cp /data/cachecloud/cachecloud/cachecloud-open-web/src/main/resources/cachecloud-web.conf /data/cachewar/cachecloud-open-web-1.0-SNAPSHOT.conf'
          }
        }
        stage('CheckWarExist') {
          steps {
            sh 'cp /data/cachecloud/cachecloud/cachecloud-open-web/target/cachecloud-open-web-1.0-SNAPSHOT.war /data/cachecloud-web/'
          }
        }
        stage('CheckStartScript') {
          steps {
            sh 'cp /data/cachecloudBak/cachecloud/script/start.sh /data/cachecloud-web/'
          }
        }
      }
    }
    stage('result') {
      steps {
        sh 'cd /data/cachecloud-web/ && sh start.sh'
      }
    }
    stage('CheckResult') {
      steps {
        sh 'ps axu|grep cachecloud |grep -v grep'
      }
    }
  }
}