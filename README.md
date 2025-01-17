# dcbell-python-plus
![image](https://user-images.githubusercontent.com/88251502/137381241-12a5f0df-7b11-4afe-99b2-9bfad56c0e8f.png)

디시인사이드(dcinside) 갤러리의 지정된 키워드가 포함된 글, 댓글을 실시간으로 텔레그램 채널봇을 통해 알려주는 스크립트

기존 코드: https://github.com/pdjdev/dcbell-python   
(새 글 알림이 필요한 경우 위 리포지토리를 참고하세요)

## 사용 방법

#### 1. BotFather를 통해 텔레그램 로봇을 생성하고, 알림을 받기 원하는 공개 채널도 생성하여 API 토큰과 채널 링크(@포함)를 준비합니다.
#### run.py를 열고, 생성한 봇키와 채널키를 넣습니다.
```
# 텔레그램 설정
TelAPI = "123456789:aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa" # 텔레그램 봇키
TelChan = "@channelid" # 주소
```
> <sub>tip. 비공개 채널에다 알림을 받고 싶은 경우 우선 공개 상태에서 봇을 채널에 추가 & 관리자로 설정한 뒤 채널에 아무 메시지나 보낸 후 해당 메시지의 링크를 복사하여</sub>   
> <sub>`https://t.me/c/[이 부분의 숫자]/123` 를 복사하고 앞에 `-100`을 붙여 `TelChan = "[여기에]"` 넣으면 비공개 채널에서도 알림 전송이 가능합니다.</sub>


### 2. 키워드 알림을 받을 갤러리의 종류에 맞는 링크의 주석을 해제합니다.
```
posturl = 'https://gall.dcinside.com/mgallery/board/lists/?id=[gid]&s_type=search_subject_memo&s_keyword=[keyword]'
cmturl = 'https://gall.dcinside.com/mgallery/board/lists/?id=[gid]&s_type=search_comment&s_keyword=[keyword]'

# 정식 갤러리
# posturl = 'https://gall.dcinside.com/board/lists?id=[gid]&s_type=search_subject_memo&s_keyword=[keyword]'
# cmturl = 'https://gall.dcinside.com/board/lists?id=[gid]&s_type=search_comment&s_keyword=[keyword]'

# 미니 갤러리
# posturl = 'https://gall.dcinside.com/mini/board/lists/?id=[gid]&s_type=search_subject_memo&s_keyword=[keyword]'
# cmturl = 'https://gall.dcinside.com/mini/board/lists/?id=[gid]&s_type=search_comment&s_keyword=[keyword]'
```


### 3. 아래로 내려가 나머지 설정값을 채웁니다.
```# 갤러리 설정
# (중요!!! 정식갤 또는 미니갤의 경우에는 위 URL 주석을 해제하여 알맞게 설정하세요!!!)
gallid = 'galleryid'

# 검색 키워드 채우기 (줄바꿈으로 구분합니다. 권장 키워드수는 1~10개입니다)
kw = '''관심
키워드를
여기에
입력하세요'''
keywords = {}

for k in kw.split('\n'):
    keywords[k] = [0,0]

# 무시닉네임 (본인이 쓰는 닉네임을 입력하세요)
passnick = '''본인의
닉네임을
여기에
입력하세요'''.split('\n')

updTime = 300 # 업데이트 주기 (초)
```
> <sub>해당 스크립트는 약 1초 간격으로 모든 키워드를 순서대로 검색한 뒤 위 주기값만큼 대기하므로</sub>   
> <sub>키워드가 10개 이상이라면 가능한 긴 간격으로 설정해 주세요 (너무 잦으면 서버로의 접근이 잠시 막힙니다)</sub>


### 4. 알림 받을 채널 링크로 가 1.에서 생성했던 봇을 관리자로 추가한 뒤, 코드를 실행하여 알림이 정상적으로 오는지 확인합니다.
![image](https://user-images.githubusercontent.com/88251502/137379979-cf87b7d8-8765-47be-941e-86703a4048e4.png)
<br/><br/>


### 5. 작동이 확인되었다면 스크립트를 직접 돌리거나 Heroku 등에 업로드하여 사용하시면 됩니다.
