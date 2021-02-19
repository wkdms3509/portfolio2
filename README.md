# 좌표 찾기 (Find coordinates)

## 1. 개요

ClientX, ClientY를 이용하여 화면 상에서 마우스가 움직일 때마다 마우스가 위치한 좌표 값을 보여주는 간단한 내용이다.
![실행화면](https://user-images.githubusercontent.com/63761624/108488030-41157500-72e3-11eb-9347-3bcba28707a3.PNG){width: 500px; height: 400px;}

## 2. 사용언어

- JavaScript

## 3. 문제점 및 해결방안

- 기본 html 구조
  ![html 기본 구조](https://user-images.githubusercontent.com/63761624/108487709-e7ad4600-72e2-11eb-9927-c9423f0565fc.PNG)

- (1) HTML로 작성한 horizontal, vertical, tag, target 클래스를 css에서 top, left 값을 설정해주었는데 이것이 성능이 나빠지도록 하는 요인이 되었고, 수정 시에 top, left의 속성값을 지우고 translate의 값만 남겨놓았다.

<수정 전>![수정 전 css](https://user-images.githubusercontent.com/63761624/108467691-fbe44980-72c8-11eb-8da4-e5e8e9be169b.PNG) => <수정 후>![수정 후 css](https://user-images.githubusercontent.com/63761624/108483806-7a97b180-72de-11eb-8e2e-f98e62bc0869.PNG)

- (2) js 파일에서 이벤트리스너를 통해 'mouseover'가 될 때마다 각 요소의 top과 left의 값을 바꿔준다고 작성함으로써 마우스가 조금만 움직여도 수많은 이벤트가 발생하여 layout부터 paint, composite까지 처음부터 재작업이 일어나야 하므로 성능이 나빠지는 요인이 되었다. 그래서 js코드 안에 각 요소의 style에서 top, left 값이 아닌 transform으로 translate값을 가져오게 하면서 문제를 해결했다. 이미지 클래스의 경우에는 변수로 target의 rect값을 가져온 후 각각 가로, 세로 높이의 1/2 인 변수를 함께 지정해주면서 이벤트리스너 안에서 target의 style값으로 넣어주었다.
  또한 getBoundingClientRect을 가져올때 이미지가 준비가 되지 않은 경우 화면을 실행했을 때 원하는 위치에 target 이미지가 나타나지 않으므로 모든 이미지와 리소스가 다 준비가 된 상태인 'load'상태에서 target을 호출해야 한다.
  <수정 전>![js 작성 모습](https://user-images.githubusercontent.com/63761624/108477687-e37b2b80-72d6-11eb-803b-9ad84f1e9fbe.PNG) => !<수정 후>[수정 후 js 코드](https://user-images.githubusercontent.com/63761624/108483085-a5353a80-72dd-11eb-8869-175b54fcfaf0.PNG)

- 요소를 움직이려 할 때, top과 left값을 이용하기 보다는 translate을 이용하여 최종적으로 composite만 발생할 수 있도록 만들어야 훨씬 효율적이다.

## 4. 느낀 점

- 그동안 css 작업을 할 때 인터넷 성능을 크게 생각하지 못하고 코드를 작성한 부분이 많았는데, 구글링과 유튜브 등 여러가지 매체를 통해 css를 어떻게 작성하느냐에 따라 인터넷 성능이 크게 달라지는 것을 직접 코드로 작성해보며 그 중요성을 실감할 수 있었다.
  또한 Blink(구글), Gecko(파이어 폭스), Webkit(사파리), EdgeHTML(microsoft Edge) 등의 인터넷 환경에 따라 css의 옵션들이 성능이 다르게 작용한다는 것도 굉장히 중요한 부분으로써 앞으로 이런 여러 부분들을 고려해가며 코드를 작성해야겠다고 느꼈으며,
  결론적으로 layout이나 paint부터 발생할 수 있는 css 속성 값을 이용해서 애니메이션을 하는 것은 좋은 방법이 아니라는 것을 알게되었다.
