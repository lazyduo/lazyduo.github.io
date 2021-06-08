---
title: "BeautifulSoup4 - 웹 크롤링 팁"
date: 2021-06-08 23:44:00 +0900
classes: wide
toc: true
tags:
    - tech
    - language
    - python
    - bs4
---

Game Dots 프로젝트에서 사용한 `BeautifulSoup4` 웹크롤링 팁 정리입니다.

## install

```cmd
pip install beautifulsoup4
```

## import

```python
import requests
from bs4 import BeautifulSoup
```

## 기본 url parsing

headers 설정이 없으면 '403' error가 발생하니 사용할 브라우저의 값을 설정해준다.

```python
base_url = 'https://www.metacritic.com/search/game/'
target_url = base_url + title + '/results'
print(target_url)

headers = {'User-Agent':'Chrome/66.0.3359.181'}
html = requests.get(target_url, headers=headers)
soup= BeautifulSoup(html.text, 'html.parser')
```

이제 이 `soup`으로 원하는 작업을 하면 된다.

## find / find_all

```python
# 찾기
search_result.find("div", {"class": "main_stats"})

# 모두 찾기
search_results = soup.find_all("div", {"class": "result_wrap"})
```

## stripped_strings

이 method는 정말 파워풀 하다!! 눈에 보이는 text만 가져오고 싶을 때, 간단하게 전체를 아우르는 태그를 가져와서 `.stripped_strings` 해주면 된다.

```python
info = list(search_result.find("div", {"class": "main_stats"}).stripped_strings)

# string을 가져온 뒤 원하는 부분을 따로 가져왔음
metascore = info[0]
title = info[1]
platform = info[2]
year = info[3].split(',')[1].strip()
```
