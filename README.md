# mounting_server
개인 컴퓨터에 서버를 마운트하면 IGV를 실행시키거나 스트립트를 짤때 sublime text 같은 text editor로 개인 컴퓨터에서 사용하는 것 처럼 사용할수 있습니다. 

## MacOS
### Install 'FUSE' and 'SSHFS'
    * https://osxfuse.github.io/ 에서 FUSE macOS 3.8.0 과 SSHFS 2.5.0 package를 다운받아서 설치한다. 
    * 설치후 `which sshfs`를 terminal에서 실행시켰을때 PATH가 나오면 다음 스텝으로 넘어가면 됩니다. 

### 터널 연결 커맨드
```bash
$ ssh -t cjyoon@[터널아이피주소] -p [포트넘버] -L [아무숫자1]:[서버10gIP]:[서버10g포트넘버] -N -i ~/.ssh/id_rsa &
```
### 로컬 컴퓨터의 아이디 확인
```bash
$ id
```
에서 나온 자기 아이디의 uid와 gid를 기억한다. 

### 마운트
```bash
$ sshfs [서버아이디]@localhost:[마운트할 서버의 경로] -p [아무숫자1] -o uid=[로컬컴uid] -o gid=[로컬컴gid] -o allow_other -o defer_permissions -o IdentityFile=~/.ssh/id_rsa [로컬컴퓨터의 마운트 할 폴더 경로]
```

### 유의사항
1. 터미널 끄면, 터널이 꺼져서 마운트도 작동안함. 
2. 마운트를 다시하려면 터널을 키고 마운트를 해제후 다시 마운트해야함
```bash
diskutil unmount [로컬컴퓨터의 마운트 된 폴더 경로]
```

