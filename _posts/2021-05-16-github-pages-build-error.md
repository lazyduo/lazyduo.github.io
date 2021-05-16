---
title: "GitHub Pages Build Error"
date: 2021-05-16 20:39:00 +0900
classes: wide
tags:
    - tech
    - ETC
    - Github_Pages
---

빡쳐서 쓰는 글. 새로운 포스트 썼을 뿐인데 **Build Error** 메일이 날라왔다.

```
The page build failed for the `master` branch with the following error:

Unable to build page. Please try again later.

For information on troubleshooting Jekyll see:

  https://docs.github.com/articles/troubleshooting-jekyll-builds

If you have any questions you can submit a request at https://support.github.com/contact?repo_id=354839136&page_build_id=253611992
```

말이 안된다. 내가 뭐 Jekyll을 만진 것도 아니고, template 수정 작업을 한 것도 아니고 그냥 포스트 새로 올린 것 뿐인데 에러가 뜬게 진짜 이상했다.

평상 시 같으면 뭐 코드에서 이 부분이 이상하다. 여기서 error가 났다. 라고 알려줬을 텐데 아무 이유도 없이 `Please try again later`라면서 마치 Jekyll 문제인 마냥 써놨다. 그래서 내가 뭐 잘 못한게 있나보다 싶어서 마지막으로 수정 반영 된 branch로 다시 돌아가서 master도 지우고, Repository Rename, config 파일의 url 수정 등등 별 짓을 다했다.

한 3시간은 시도 했는데 계속 push 하자마자 'Build Error' 메일이 날라왔다.

아무리 생각해도 이상해서 Stack Overflow 가 보니 지금 시간에 나랑 비슷한 문제를 겪어서 글 올린 친구들이 있지 않은가?

그래서 결국은 GitHub이 뭔가 이상하다 생각해서 아래 링크 들어가봤더니...

[GitHub Status](https://www.githubstatus.com/)

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/github-pages-error.png){: .align-center}

> Update - GitHub Pages is experiencing degraded performance. We are continuing to investigate. May 16, 10:49 UTC

그렇다. 내 문제가 아니라 GitHub 문제 였다.

뭐.. 이런 일도 있구나 싶다...

<br>

(다음부터는 당황하지 말고 나를 믿자...)