# Docker Linux 환경 설치

```bash
# apt 인덱스 업데이트
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release

# 2. Docker 공식 GPG 키 추가
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 3. Docker 저장소를 APT 소스에 추가
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 4. APT 패키지 캐시 업데이트
sudo apt-get update

# 6. Docker 서비스 상태 확인
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 7. 사용자 권한 설정
sudo usermod -aG docker $USER # docker 명령어 사용시 sudo 권한 부여하는 설정(재부팅 필수)
newgrp docker    # 설정한 그룹 즉각 인식하는 명령어, 생략시 재부팅 후에만 group 적용
groups
tail /etc/group
```
### 1.Docker 실행
```bash
docker run -d -p 9000:9000 --privileged -v /var/run/docker.sock:/var/run/docker.sock uifd/ui-for-docker
```
```bash
docker run -d -p 9001:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data --restart=always portainer/portainer
```
### 2.9000번으로 access가능한 이미지
```bash
curl http://127.0.0.1:9000
```
![image](https://github.com/user-attachments/assets/0a17f0c4-6239-4935-b085-00cb69bdf3e3)

### 3.container에 openjdk, tomcat 이미지 pull 받아오기
```bash
docker pull openjdk:17
docker pull tomcat:10
docker images
```
![image](https://github.com/user-attachments/assets/7ea0e352-930b-4dea-9327-ce109ec1d399)

### 4.이미지를 컨테이너로 생성
#### tomcat
```bash
docker run --name mytomcat -p 8080:8080 tomcat:10
```
컨테이너 접속시
```bash
docker exec -it 00508b4430ac bash
```
![image](https://github.com/user-attachments/assets/0ec450a7-c657-4f02-a8b1-b7c88e69e642)

#### openjdk
```bash
docker run --name myjdk openjdk:17
```

#### nginx
```
docker run --name mynginx -d -p 80:80 nginx
```
-------

##### host os : window
##### guest os : linux
##### tool : virtual box
##### - NAT로 포트포워딩 
![image](https://github.com/user-attachments/assets/561dde05-b9fb-4f50-96c2-c2d200094622)
### window에서 nginx 접근 가능 확인
![image](https://github.com/user-attachments/assets/e8e2792a-c8d0-4478-9941-e31cb33c543c)

