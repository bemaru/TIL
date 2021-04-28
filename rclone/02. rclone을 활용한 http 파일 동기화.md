# 개요
- Rclone ("rsync for cloud storage") is a command line program to sync files and directories to and from different cloud storage providers.
- Rclone은 클라우드 스토리지를 위한 rsync 이며, 다양한 스토리지 프로바이더에 대한 파일,디렉토리의 CLI 동기화를 제공합니다.
- https://rclone.org/
- https://github.com/rclone/rclone
- Supported providers 가 댜앙


# http 웹서버가 apache 인 경우 연동
- https://rclone.org/http/
- rclone config 로 remoteㅇ 대한 정보 세팅
- rclone ls remote:directory 로 조회되는지 테스트
- rclone sync -i remote:directory /home/local/directory 로 동기화 진행
- 여기까지 진행해서 문제없다면 이미 apache 에 directory index 설정이 되어 있는것임

## 추가적인 apache 설정
- 보통은 보안상 directory index 옵션을 꺼둔다
- 내 경우는 아래 방법으로 진행해봄(프로젝트 상황마다 다르겠지만..)
- apache의 http.conf 수정
- 인덱스 모듈 로드
```
LoadModule autoindex_module modules/mod_autoindex.so
```
- 동기화할 디렉토리 옵션 ( index 옵션외에 AuthConfig 로 HTTP 사용자 인증을 추가한다 )
```
<Directory "~/path/to/my_files/">
    Options Indexes FollowSymLinks
    AllowOverride AuthConfig
    Require all granted
</Directory>
```
- 만약 파일동기화에는 HTTP 기본인증을 사용하지만, 개별 파일 다운로드는 인증없이 하고 싶다면
```
## ".ht" 파일 접근제어 옵션 위에 아래 옵션을 추가해서 개별 파일 접근에 대한 인증은 하지 않도록 할 수 있다.
<Files *.*>
    Require all granted
</Files>

## 아마 기본적으로 아래 세팅이 있을것임
<Files ".ht">
    Require all denied
</Files>
```

- AllowOverride AuthConfig 옵션에 대한 세부사항(어떤 계정으로 어떤 경로에 적용할지)을 세팅한다.
- HTTP 기본인증을 적용할 경로에 .htaccess 파일을 추가한다
```
AuthName "브라우져 사용자 로그인창 title"
AuthType Basic
AuthUserFile "/apache/etc/.htpasswd"
AuthGroupFile /dev/null
<Limit GET POST>
require valid-user
</Limit>
```
- /apache/etc/ 에 .htpasswd 추가 ( 계정 설정 )
```
cd apache/etc
../bin/htpasswd -C .htpasswd [username]
```
