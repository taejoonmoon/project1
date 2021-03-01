node('master') {
    stage('Preparation') { // for display purposes
    sh """
    rm -rf project1
	git clone https://github.com/taejoonmoon/project1
	cd project1
	docker build -t myapp:$BUILD_NUMBER .
    """
    }

      stage('Push') {
            // 도커헙 계정 정보 가져오기 
            withCredentials([[$class: 'UsernamePasswordMultiBinding',
              credentialsId: 'docker-hub',
              usernameVariable: 'DOCKERHUB_USER',
              passwordVariable: 'DOCKERHUB_PASSWORD']]) {
              // 이미지 패키징 & 업로드
              sh """
                docker login -u ${DOCKERHUB_USER} -p ${DOCKERHUB_PASSWORD}
                docker tag myapp:$BUILD_NUMBER ${DOCKERHUB_USER}/myapp:$BUILD_NUMBER
                docker push ${DOCKERHUB_USER}/myapp:$BUILD_NUMBER
              """
              }
	}
}
