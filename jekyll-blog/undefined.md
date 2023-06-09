# 댓글기능을 만들면 좋겠는데 무얼쓰지?

블로그를 운영하는데 있어 댓글기능은 방문자들과의 소통 창구 역할을 하게 되는데\
Github Pages에선 댓글기능을 지원하지 않는다.\
또한, 내가 작성하고 있는 블로그는 **jekyll** 기반으로 **정적** 블로그이기 때문에\
**동적** 기능을 사용하는 댓글 서비스를 운영하는데 있어 기능을 구현하기 막막했다.\
열심히 찾아본 결과 **disqus** 라는 플러그인을 통해 기능을 구현할수 있다 그래서\
내 Gitblog에 적용시키기로 하였다.

## Step 1 - 1

**disqus** 를 사용하기 위해선, [여기](https://blog.disqus.com/)를 접속해 회원가입부터 진행해야한다. ![캡처 1](https://user-images.githubusercontent.com/58337935/140016900-aaaf416f-35ca-40d0-a709-d0adecfcf13b.PNG)

다양한 방법으로 간편가입이 가능하니 가입을 한다.

## Step 1 - 2

가입을 완료하였으면 홈페이지에서 **get started** 버튼을 클릭하면\
다음과 같은 화면이 나온다. ![캡처 2](https://user-images.githubusercontent.com/58337935/140016931-b3a29e0c-e16b-4359-8e0c-5122091b094a.PNG)

두번째 항목 **'I want to install Disqus on my site'** 를 클릭합니다.

## Step 1 - 3

![캡처 3](https://user-images.githubusercontent.com/58337935/140019607-bd627a56-1597-4c96-b984-61dd5714e7fa.PNG)

**Website Name** 에 이름을 입력후 Category 를 설정해준뒤,\
**Create Site** 버튼을 클릭해 다음으로 갑니다.

## Step 1 - 4

![캡처 4](https://user-images.githubusercontent.com/58337935/140022746-4358e25e-425d-4d22-8ae2-8d687e17c489.jpg)

**Basic** 으로도 충분하기 때문에, **Basic** 으로 선택한다.

## Step 1 - 5

![캡처 5](https://user-images.githubusercontent.com/58337935/140022959-6d2150ea-3909-4e97-b286-9428c5854711.png)

**jekyll** 아이콘을 클릭한다.

## Step 1 - 6

![캡처 6](https://user-images.githubusercontent.com/58337935/140023604-ecd9f746-d4ad-4f76-b7f3-0e9ca18e31ac.png)

jekyll 에서 **disqus** 를 사용할수있게 가이드라인을 제공한다.

## Step 2 - 1

**disqus** 설정까지 완료했으니, jekyll project에 적용을 해야한다. 각 테마에 따라 다르지만, \_config.yml에 적용한다.

jekyll project에 **disqus.html** 이 없다면 \_include 에 생성하여\
다음과 같이 적용한다.

s.src에 **github page link** 를 설정해주고 저장하면 된다.

## Step 2 - 2

각 페이지에서 사용여부를 선택해 disqus를 사용하려먼\
.md 파일 상단부분에 **comments: true or false** 를 설정해주면 된다.

모든 .md 파일에 적용을 하려면 post의 footer를 담당하면 html 파일에\
아래의 코드를 추가시켜준다.

적용뒤, 실행해보면 .md 파일에 disqus가 생긴걸 볼수 있다.

![캡처 7](https://user-images.githubusercontent.com/58337935/140027025-7c983060-7134-4d77-b957-0fb6a472f7e3.jpg)

댓글을 달면

![캡처 8](https://user-images.githubusercontent.com/58337935/140027167-9e2f2d9f-cfe0-421f-83d5-76fa4937e444.jpg)

정상작동하는것을 확인할 수 있다.
