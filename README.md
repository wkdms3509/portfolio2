# 좌표 찾기 (Find coordinates)

## 1. 개요

- ClientX, ClientY를 이용하여 화면 상에서 마우스가 움직일 때마다 마우스가 위치한 좌표 값을 보여주는 간단한 내용입니다.

## 2. 사용언어

- JavaScript

## 3. 문제점

- HTML로 작성한 horizontal, vertical, tag, target 클래스를 css에서 position: absolute로 설정하고 top, left 값을 설정해주었는데 이러한 설정이 결국 성능이 나빠지도록 합니다.

![html 작성 모습](https://user-images.githubusercontent.com/63761624/108467587-cb041480-72c8-11eb-815d-586b1ebb6496.PNG)
![css 작성 모습](https://user-images.githubusercontent.com/63761624/108467691-fbe44980-72c8-11eb-8da4-e5e8e9be169b.PNG)

- js 파일에서 이벤트리스너를 통해 'mouseover'가 될 때마다 top과 left의 값을 바꿔준다고 작성함으로써 마우스가 조금만 움직여도 수많은 이벤트가 발생하여 layout부터 paint, composite까지 처음부터 다시 재작업이 일어나야 하므로 성능이 나빠지는 요인이 됩니다.
  ![js 작성 모습](https://user-images.githubusercontent.com/63761624/108477687-e37b2b80-72d6-11eb-803b-9ad84f1e9fbe.PNG)

## 4. 해결방안

- 요소를 움직이려 할 때, top과 left값을 이용하기 보다는 translate을 이용하여 최종적으로 composite만 발생할 수 있도록 만들어야 훨씬 효율적이다.

## 5. 느낀 점

- 그동안 css 작업을 할 때 인터넷 성능을 크게 생각하지 못하고 코드를 작성한 부분이 많았는데, 구글링과 유튜브 등 여러가지 매체를 통해 css를 어떻게 작성하느냐에 따라 인터넷 성능이 크게 달라지는 것을 직접 코드로 작성해보며 그 중요성을 실감할 수 있었습니다. 또한 Blink(구글), Gecko(파이어 폭스), Webkit(사파리), EdgeHTML(microsoft Edge) 등의 인터넷 환경에 따라 css의 옵션들이 성능이 다르게 작용한다는 것도 굉장히 중요한 부분으로써 앞으로 이런 여러가지 부분들을 고려해가며 코드를 작성해야겠다고 느꼈습니다.
