다운로드링크 : https://play.google.com/store/apps/details?id=com.dontcryjunsu.asd

# 🐶Animal Swipe Defence🐱

![0](https://user-images.githubusercontent.com/31693348/81091380-1f0c5b00-8f3a-11ea-9ef4-57be6bfa1ccc.png)



## 게임소개

**애니멀 스와이프 디펜스**는 맵 타일안에 무작위의 동물들을 생산, 이동, 합체 하여 몰려오는 적들을 섬멸하는 퍼즐 디펜스 게임입니다. 

단순히 유닛을 설치만 하는 다른 디펜스 게임들과 달리, 매 스테이지 동물들의 배치를 신경 써야하는 디펜스/퍼즐 게임입니다. 같은 동물 조합이더라도 배치에 따라 결과는 크게 갈립니다.

***

## 개발

- 로비

  - UI
  - 동물 뽑기
  - Sound

- 게임필드

  - UI
  - Input
    - 생산
    - 이동
  - InGame
    - 자원관리
    - 전투
    - 재배치
  - Sound

***

## Optimize

#### 1. Sprite Atlas

단순히 스프라이트들을 Atlas에 집어넣기만 했는데도 Batch수가 상당히 줄어들었다.단 이미지 규격을 잘맞추지 않으면 Start의 칼이미지 처럼 깨져보이는 이미지들이 보였다.

![image](https://user-images.githubusercontent.com/31693348/109277152-42521f00-785a-11eb-9aeb-f7b7aebae784.png)

***

#### 2. Sorting Order

BlankBox와 Dot만 찍어놓은 화면인데 Batches가 33이나 된다. 분명 같은 스프라이트를 사용하면 드로우콜이 증가하지 않을텐데 이상하게 생각했다.

![image](https://user-images.githubusercontent.com/31693348/109477481-6c564c00-7abb-11eb-859f-c706efa2960b.png)

프레임디버거를 이용해서 확인해보니 이상하게 Dot이 찍힐때도 있고 BlankBox가 찍힐때도 있는걸 확인할 수 있었다. 

![image](https://user-images.githubusercontent.com/31693348/109477922-f56d8300-7abb-11eb-91a5-63b48821ba84.png)

따로 찍어보면 예상과같이 Batches가 1씩 찍힌다.

![image](https://user-images.githubusercontent.com/31693348/109478095-2948a880-7abc-11eb-8494-5561e135bf05.png)

문제는 생각보다 쉽게 해결했다. 왠지 둘의 Order in Layer가 겹쳐서 그렇지 않을까 생각했는데 예상이 적중하였다!

![](https://user-images.githubusercontent.com/31693348/109478243-572ded00-7abc-11eb-90f9-b0d685997fa8.png)

