왜 사람들은 monorepo 에 열광하는가?
===========================

Monorepo 가 무엇인지 먼저 짚고 넘어가보자
----------------------

Monorepo 는 Mono Repository 의 약자이며, mono 는 한개라는 뜻이며, monorepo 는 한개의 repository 라는 뜻이다.

보통 회사에서는 여러개의 프로젝트에서 공유하는 utils 과 같은 라이브러리를 공유하는경우가 많다.

프로젝트마다 각각 repository 가 있다고 가정 하면 그것을 다 한데 모아 하나의 repository처럼 개발/관리한다는 의미이다.

코드 환경 (예: NodeJS, Ruby, Git)에는 보통 그것에 맞는 package/library managers 이 존재한다.

예를들어서 NodeJS 에서는 NPM/Yarn 이 있고, Ruby 는 Gem 이 있는것처럼 말이다.

이런 package managers 들은 보통 monrepo 를 가능하게 해주는 기능이 포함되어 있는 경우가 많다.

yarn 같은경우 yarn workspaces, git 같은경우 git submodules 이라는 기능이 있다.

Monorepo 가 아닐때 발생하는 골치아픈 상황
-------------------

우선 Monorepo 를 쓰지 않을때 발생하는 문제점에 대해서 알아보자.

예를들어서 utils 라는 라이브러리를 사용하는 프로젝트 kdd-website 가 있다고 가정해보자.

```
kdd-website/package.json
{
  "name": "kdd-website",
  "dependencies": {
    "utils": "1.0.0"
  }
}
```

여기서 utils 에 버그가 발견되 수정해야되는일이 발생할땐 어떻게 해야 할까요?

1. utils 안에 버그를 수정한후 npm 에 버전 1.0.1 로 다시 release 를 한다.     
2. kdd-website/package.json 안에 utils 를 버전 1.0.1 로 바꾸고 npm install / yarn install 를 해준다.    
3. kdd-website 를 다시 실행시킨후 버그가 제대로 고쳐졌는지 확인한다.     

이렇게 아무리 간단한 코드 수정이라도 엄청난 시간과 노력이 들어간다.

버그가 제대로 수정됬는지 release 하기전에는 알기 어렵기때문에 테스트를 하기 위해서 계속 release 를 해야하는 아주 골치 아픈 사태가 발생한다.

Git Submodules 사용하기
-------------------

git 만 사용하여 monorepo 를 만들기 위해서는 git submodule을 사용하면 된다.

git submodule은 쉽게 말해 git repo 안에 또다른 git repo 가 있는것을 의미한다.

```
kdd-website/.git
kdd-website/.gitmodules
kdd-website/libraries/utils/.git
```

이런식으로 되며, kdd-website git 에는 utils git 의 코드내용은 들어가지 않으며, .gitmodules 라는 파일안에 utils 라는 git submodule 이 depdencies 로 들어가며, 위치, 그리고 remote url 도 같이 들어간다

현재 git 에 다른 git 을 submodule 로 추가하고싶으면 아래 command 를 쓰면된다.

`git submodule add https://github.com/vancouver-kdd/kdd-website-utils libraries/utils`

그럼 아래와 같은 파일/폴더가 생성이 된다
```
new file:   .gitmodules

new folder   libraries/utils
```

.gitmodules 안에는 내용이 아래와 비슷하게 들어간다
```
[submodule "kdd-website-utils"]
	path = libraries/utils
	url = https://github.com/vancouver-kdd/kdd-website-utils
```
git submodule 의 장점은 위에서 말한것처럼 utils 에 버그가 있을 경우, 코드를 고치고 테스트를 하기 위해 매번 버전을 올리고 release 하고, 그것을 다시 install 하는 번거로운 작업을 하지 않아도 된다.

kdd-website 안에서 utils 를 변경하면서 바로 kdd-website 를 테스트 할 수 있기 때문이다.

하지만 git을 사용하는게 좀 더 까다로워 진다는 단점이 있다.

보통 코드를 변경할때 kdd-website 와 kdd-website-utils 를 동시에 변경하는경우가 많은데, 두 각기 다른 git 이기 때문에 stage/commit/push 를 각각 해줘야 한다는 단점이 있고, pull 도 마찬가지이다.

우리가 처음에 clone 을 할때 `git clone https://github.com/vancouver-kdd/kdd-website` 와 같이 하면 libraries/utils 라는 폴더는 비어있는 상태로 클론이 된다.

아래와 같은 command 로 clone 을 해야지만 submodule 까지 같이 클론이 된다

`git clone --recurse-submodules https://github.com/vancouver-kdd/kdd-website`

여기서 이미 `git clone` 을 `--recurse-submodules` 없이 하였다면 아래의 커맨드를 돌려주면된다.

`git submodule update --init --recursive`

git client 를 쓰면 좀더 수월해지지만 git 이 다르기때문에 commit 할때마다 utils 따로 kdd-website 따로 해야하고, 그리고 comment 도 따로 적고, git history 도 두개로 나눠지니 blame 하기도 쉽지 않다, 그래서 .gitmodule 에 현재 사용하고있는 submodule 의 commit hash 가 보통 포함이 되며, 그럴경우 utils 코드만 변경을 하여도 .gitmodule 이라는 파일에 commit hash 가 달라지고 kdd-website 의 git 까지 푸쉬해야하는 번거로운 상황이 발생한다. 그래도 monorepo 를 사용하지 않았을때보다는 훨씬 낫다.

마지막으로 git 마다 nodejs 같은 프로젝트를 사용하여 dependencies 가 있을 경우 git clone/pull 후에 git 폴더마다 들어가서 yarn install/npm install 을 해주어야 한다.

git submodule 의 10프로 부족한점을 채워주는 yarn workspace
-------------------

yarn 은 npm 을 대채해줄수있는 node package manager 이다. parallel install 이 가능하여 속도가 npm 보다 월등히 빠르며, yarn 버전 2에 plug'n'play 기능을 사용할경우 yarn version 1 보다 월등히 더 빨라진다고 한다.

yarn 에서는 npm 처럼 workspace 기능이 있는데 바로 monorepo 를 사용 가능하게 해준다.

root/package.json
```
{
  "private": true,
  "workspaces": ["kdd-website", "utils"]
}
```
이렇게 할 경우 yarn install 을 한번만 해주면 kdd-website/package.json 하고 utils/package.json 의 dependencies 들을 모조리 다 같이 깔아준다.

utils/package.json:
```
{
  "name": "utils",
  "version": "1.0.0",
  "dependencies": {
    "lodash": "5.0.0"
   }
}
```
kdd-website/package.json:
```
{
  "name": "kdd-website",
  "version": "1.0.0",

  "dependencies": {
    "utils": "1.0.0"
  }
}
```
그러면 아래와 같은 폴더 구성이 생길것이다. 

```
/package.json
/yarn.lock

/node_modules
/node_modules/lodash
/node_modules/utils -> /utils

/utils/package.json
/kdd-website/package.json
```
여기서 중요한점은 node_modules/utils 는 /utils 를 symlink로 연결되어 있기 때문에 utils 파일을 변경하게 되면 node_modules/utils 도 같이 변경된다.

여기서 한가지 중요한점은 /node_modules/utils 에 utils 는 폴더 이름이 아니고 utils/package.json#name 을 사용한다는 점이다.

즉 utils/package.json#name 이 kdd-website-utils 였다면 아래와 같이 된다.

`/node_modules/kdd-website-utils -> /utils`

그리고 import 할때는 아래와 같이 한다.

`import utils from 'kdd-website-utils'`

yarn workspace 의 단점은 

node 프로젝트에서만 사용이 가능하다는 점이다.

yarn workspace 보다 조금더 특별한 기능이 필요하다면 lerna 라는 툴을 사용할수도 있다.


포스팅 원문 출처: 

https://www.youtube.com/watch?v=flbz_5aMikw

https://git-scm.com/book/en/v2/Git-Tools-Submodules

https://yarnpkg.com/getting-started/migration

https://yarnpkg.com/features/pnp#compatibility-table

https://classic.yarnpkg.com/lang/en/docs/workspaces/
