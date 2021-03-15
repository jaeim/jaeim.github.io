---
title: "[github]README.md 파일만들기"
excerpt: "미루고 미룬 README 작업하기"

categories:
  - Blog
tags: 
  - [Blog, git, github, readme, markdown]
toc: true
toc_sticky: true
date: 2021-03-15
last_modified_at: 2021-03-15

---

<br>

# 1. README.md 생성하기

리드미 파일을 만들고 싶은 리포지토리로 들어가서 가장 하단에 <span style="color:green">Add a README</span> 버튼을 클릭한다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/add_readme.PNG){: .align-center}

그러면 README.md 안의 내용물을 작성할 수 있는 에디터칸이 나오는데 거기서 그동안 검색해온 마크다운 문법대로 작성하면 된다. PREVIEW도 바로바로 확인할 수 있어서 편함!


# 2. 이미지 삽입

지금 깃허브 페이지에 이미지 삽입하는 것 처럼 프로젝트에 폴더를 하나파서 생성하면 되는 줄 알았더니 계속 코드만 나오고 안되는 현상 발생..

이를 해결하려면 **나의 리포지토리 > ISSUES > 삽입하고 싶은 이미 드래그** 하여 생성되는 링크를 붙여넣기하면 된다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/add_img_in_readme.PNG){: .align-center}

참고한 링크 : <https://cutemoomin.tistory.com/112>


# 3. 동영상 삽입

이것 또한 깃허브 페이지에 하는 것처럼 include 키워드를 써서 포함시키려 했지만 또 실패..

스택오버플로우에서 편법?아닌 편법을 사용하여 동영상 삽입하는 방법을 알아냈다.

내가 원했던 건 동영상 링크만 띡 보여주는게 아니라 동영상 재생 썸네일이 보이길 원했다. 물론 깃허브 자체에서 바로 재생할 순 없고 이미지를 클릭하면 유튜브 링크로 넘어가는 형태라 완전히 맘에 들진 않지만 임시방편으로 이 방법을 사용하기로 했다.

1. imgur에 README에 보이고 싶은 동영상 썸네일 업로드하기

2. 아래 코드를 삽입해주기
    ```
    [![Watch the video](imgur에 업로드한 이미지링크)](유튜브 링크)
    ```

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/add_vid_in_readme.PNG){: .align-center}

그러면 아래처럼 나름 내가 원했던대로 동작하는 걸 볼 수 있다.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/readme_ex.PNG){: .align-center}


참고한 링크 : <https://stackoverflow.com/questions/4279611/how-to-embed-a-video-into-github-readme-md/4279746#4279746>

