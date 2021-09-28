pipeline {
  agent any
  environment {
    //版本，只改这个就行！！！
    version = '0.1'
    }
  tools {
        maven 'Maven3.8.2'
    }
  parameters {
        // 提供构建的模块选项
        choice(
            description: '你需要选择哪个模块进行构建 ?',
            name: 'moduleName',
            choices: ['mySampleProject']
        )   
        booleanParam(name: 'isAll', defaultValue: false, description: '是否需要全量（包含clean && build）')     
        string(name: 'update', defaultValue: '', description: '本次更新内容?')
    }
  
  stages {
    stage('全量清除旧数据...') {
            when {
                expression {
                    params.isAll == true
                }
            }
            steps {
                echo "开始全量清除"      
                sh "mvn clean install -Dmaven.test.skip=true"
            }
        }
        stage('全量打包应用') {
            when {
                expression {
                    params.isAll == true
                }
            }
            steps {
                echo "开始全量打包"   
                sh "mvn package -Dmaven.test.skip=true"
                echo '打包成功'
            }
        }
        stage('清除旧数据...') {
            when {
                expression {
                    params.isAll == false
                }
            }
            steps {
                echo "开始清除${params.moduleName}模块"      
                sh "mvn clean install -Dmaven.test" 
            }
        }
        stage('打包应用') {
            when {
                expression {
                    params.isAll == false
                }
            }
            steps {
                echo "开始打包${params.moduleName}模块"   
                sh "mvn package -Dmaven.test.skip=true"
                echo '打包成功'
            }
        }
  }
}

