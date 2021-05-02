---
title: "Tech > Project LOLHUB > Youtube API"
classes: wide
author_profile: false
toc: true
sidebar:
    nav: "tech"
---

## 개요

LOLHUB 프로젝트의 최종 단계는 클릭 한 번으로 자동으로 Youtube <span><i class="fa fa-youtube"></i></span>에 업로드 하는 것 까지 였습니다. 이 글에서는 Youtube API 사용을 위한 OAuth 자격 증명 방법과 Youtube Handle을 통한 자동 업로드까지 다뤄보도록 하겠습니다.

## OAuth?

Youtube API를 사용하기 위해서는 OAuth 인증이 필수다. OAuth는 인증 표준 protocol 개념으로, 사용자가 아이디와 비밀번호를 제공하지 않고 secret token으로 어플리케이션의 접근 권한을 부여한다. 언뜻 보면 API Key랑 비슷하다고 생각할 수 있으나, 목적 자체가 다르다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/api-key-overview.png){: .align-center}

위 그림처럼, **API Key는 프로젝트**를 식별하고 승인하는 반면에, **Auth Token은 사용자**를 인증하고 승인한다. API Key는 결국 비밀번호와 같이 분실 위험이 있는 안전하지 않은 액세스 방법이기 때문에, 특정 IP 주소 범위, Android 앱, iOS 앱과 같은 환경에서만 사용할 수 있도록 '제한'하여 사용한다. 반면, Auth 체계는 사용자를 식별하는 안전한 방법을 제공하여 사용자의 secret정보를 노출하지 않으면서 API 호출을 가능하도록 한다.
 
여하튼, Youtube도 API를 사용하는데 있어서 어떤 'key'가 왔다갔다하면 보안 문제가 있을 수 있기 때문에, OAuth 2.0 토큰을 통해 안전하게 사용자 정보를 전달하면서 자신의 동영상 데이터 정보나, 업로드 등의 권한을 부여 할 수 있는 것이다.

## Get Credential

[Google API Console](https://console.developers.google.com/apis/credentials)에서 프로젝트를 등록하고 `client_secret` 파일을 받았다면, 아래의 방법으로 Credential을 받으면 된다.

```python
import google_auth_oauthlib.flow as gflow
    
    def new_token(self, mode):
        scopes = ['https://www.googleapis.com/auth/youtube.readonly',
            'https://www.googleapis.com/auth/youtube.force-ssl',
            'https://www.googleapis.com/auth/youtube.upload']

        api_service_name = 'youtube'
        api_version = 'v3'
        client_secrets_file = self.client_secret_file

        # Get credentials and create an API client
        flow = gflow.InstalledAppFlow.from_client_secrets_file(
            client_secrets_file, scopes)

        cred = flow.run_local_server()

        # save access and refresh token
        with open(self.access_token_file, 'wb') as f:
            pickle.dump(cred, f)
        return cred
```
여기서 `scope`는 내가 부여 받을 권한들을 제한해준다. 사용할 기능에 따라서 필요한 scope들을 추가해주면 된다. 예시로 업로드 기능을 가능하게 하기 위해서 `'https://www.googleapis.com/auth/youtube.upload'`를 추가해 주었다.

`google_auth_oauthlib.flow` 라이브러리에서 `InstalledAppFlow.from_client_secrets_file('client_secrets_file', 'scope')`를 하면 `Flow` 객체를 반환 해 준다. 이 class는 유저 정보에 접근 가능한 자격을 얻도록 해준다.

그 후 `flow.run_local_server()`를 하면, 유저의 브라우저에 권한 확인 URL을 띄워 준다. 유저가 권한 동의를 하게 되면 해당 **자격 정보**를 반환해주는 구조다.

## Get Youtube Handle

위에서 `Credential(자격)`을 얻었다면 이제 Youtube 핸들을 얻자. 아래 처럼 `googleapiclient.discovery.build()`로 얻어 올 수 있다. 이때 `credentials`에 앞에서 얻은 자격 정보를 넣어 주면 된다. 그렇게 되면 나(유저)의 계정에 대한 Youtube 핸들을 얻게 된 것이다.

```python
    def get_youtube_handle(self):
        api_service_name = 'youtube'
        api_version = 'v3'
        cred = self.auth()
        youtube = googleapiclient.discovery.build(
            api_service_name, api_version, credentials=cred)
        return youtube
```

이제 이 핸들로 이것저것 해볼 수 있다.

## Get User Data

원하는 유저 정보를 조회해 보자. 위에서 얻은 Youtube 핸들 객체에 여러가지 명령어를 줄 수 있다. 내 채널에 무언가를 작성하기 이전에, 기존 데이터의 정보 조회 부터 해보자.


기본적으로 `request` 작성, `request.execute()`, `response` 구조로 진행 된다. request에 내가 원하는 정보를 주문서 처럼 작성 하면 된다. 아래는 동영상 아이디를 전송해서 해당 아이디와 일치하는 영상의 정보(part)를 얻는 예시 이다. Youtube가 제공 가능한 정보는 이 [링크](https://developers.google.com/youtube/v3/docs/videos?hl=en)를 참고하자. (속성값이 꽤 많다)


```python
    def get_vid_info(self, vid_id):
        self.log.info('getting video\'s info...')

        youtube = self.get_youtube_handle()

        request = youtube.videos().list(
            part='snippet,contentDetails,statistics',
            id=vid_id
        )
        response = request.execute()
        return response
```

## Upload Video & Thumbnail

최종 목표인 동영상 업로드와 썸네일 설정을 해보자. 썸네은 동영상 업로드하는 동시에 올리기가 불가능해서 `request`를 한 번 더 처리 하였다.

`youtube.videos().insert()`로 업로드 해주며, **body** 부분에 세팅하고 싶은 정보들을 넘겨주어 영상 타이틀, 설명, 태그 등을 설정해 줄 수 있다. **media_body** 부분에는 업로드할 영상의 경로를 넣어 주면 된다.

```python
# upload video
request = youtube.videos().insert(
    part='snippet,status',
    body={
        'snippet': {
            'categoryId': '20',  # 20 for 'gaming'
            'description': vid_description,
            'title': vid_title,
            'tags': vid_tags
        },
        'status': {
            'privacyStatus': 'public',  # private, public, unlisted
            'madeForKids': False
        }
    },
    # ivid path to insert
    media_body=MediaFileUpload(kwargs['vid_path'])
)
response = request.execute()
self.log.info(json.dumps(response, indent=4))
yt_vid_id = response['id']

# update thumbnail
request = youtube.thumbnails().set(
    videoId=yt_vid_id,
    media_body=MediaFileUpload(kwargs['vid_thumbnail_path'])
)
response = request.execute()
self.log.info(json.dumps(response, indent=4))
```

하단 `youtube.thumbnails().set()` 부분을 보면 이전에 `insert` 할 때의 응답 데이터로 부터 동영상 `id`를 받아 다시 API 요청을 하고 있음을 알 수 있다. 설정할 **videoId**를 넣어주고, 영상 업로드와 똑같이 **media_body**에 만들어진 썸네일 경로를 넣어주면 완료 된다.

## 마치며

이 부분은 개발할 때 OAuth 부터 막혀서 굉장히 난항을 겪었었다. API 개념도 완전히 안 잡힌 와중에 인증이니 자격이니 뭔 소린지 모르겠는데 심지어 영어 document로 봐야 했었다. 한글 사이트가 있긴 했는데, 정보가 영어판이랑 차이가 났었다.

아무튼 처음에 조금 헤맸지만, 예제 코드를 하나하나 하다 보니까 원하는 기능을 구현 할 수 있었다. 웹에서 버튼 하나만 누르면 입력된 정보로 자동으로 Youtube 채널에 업로드 되고 썸네일도 지정해준다?! 그리고 불과 몇 주 전까지 python도 모르던 사람이 구글이니 유튜브니 하면서 메이저급 서비스랑 연계해서 무언가 해나간다는게 기분이 좋았다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/youtube-api.jpg){: .align-center}

비밀이지만, API 사용 허가 문제로 구현 다 해놓고 실제 구동은 Selenium으로 크롬 드라이버 잡아서 매크로로 해버렸다. 이 방법은 다음 기회에 알아보자.