---
title: Hexo로 블로그 시작하기
date: 2018-10-13 01:52:47
tags:
    - TIL
    - hexo
---

## 1. Hexo

* 기존에 `Jekyll`로 작업하던 깃헙 블로그를 Hexo로 바꿨다.
* 따라서 새로 배운 `Hexo`의 명령어들을 정리해보려한다.
* [이 분의 블로그 글](https://hyunseob.github.io/2016/02/23/start-hexo/)을 참고함 (잘 정리됨! 자주 참조하자!)

## 설치

기본적인 노드 설치 후, Hexo를 설치하자

    $npm install -g hexo-cli

그 다음 Hexo 디렉토리 스캐폴딩 작업을 하자. 나는 my-blog라는 디렉토리를 생성했다. (꼭 깃헙 repo와 이름이 같을 필요 없음)

    $hexo init <my-blog>

잘 생성 되었는지 로컬에서 확인해보자

    $hexo serve

## 포스팅

매우 간단하다. (임의로 my-posting이라고 포스트명을 지었다)

    $hexo new <my-posting>

draft 문서를 작성하고 싶으면

    $hexo new draft <my-draft>

이렇게 하면 각각 /source/_posts/ 와 /source/_drafts/ 에 my-posting.md 와 같은 파일이 생성된다.

> 태그 플러그인 참조 : https://hexo.io/docs/tag-plugins.html

* draft 문서를 포스팅 하려면, publish 명령어를 사용
    * _drafts 디렉토리에 있던게 _posts 디렉토리로 이동함. 날짜/시간도 넣어진다고한다

            $hexo publish <my-draft>

## 디플로이

우선 _config.yml에 내 github 정보를 입력!

    deploy:
        type: git
        repo: https://github.com/Kihyun92/Kihyun92.github.io.git
        branch: master

그 다음, 정적 파일들을 생성해준다.

    $hexo generate

디플로이를 위한 플러그인 설치!

    $npm install --save hexo-deployer-git

디플로이!

    $hexo deploy

매우 간단하다!

다만, 코드 관리를 다른 repo에서 해야하는게 단점이라고 하신거에 공감.

이제 차근차근 블로그를 꾸며보자!
