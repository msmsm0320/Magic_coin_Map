# 중세 탈출 맵: 언리얼 엔진 프로젝트

## 프로젝트 개요
이 프로젝트는 **가상현실 프로그래밍 기말 과제**로, Unreal Engine 5를 사용하여 제작된 게임입니다. 플레이어는 마법에 걸린 여관을 탐험하며 흩어진 보물을 원래 자리로 되돌려 여관의 저주를 풀어야 합니다.

![image](https://github.com/user-attachments/assets/bd7a29fa-badb-4a59-96e7-eb03235dd16b)

---

## 게임 스토리
게임은 **중세 시대**를 배경으로 합니다. 주인공은 여관에서 하룻밤을 묵게 되며, 여관에는 다음과 같은 마법의 보물이 전시되어 있습니다:
- **불의 검**
- **물의 방패**
- **번개의 도끼**
- **빛의 활**
- **어둠의 창**

이 보물들은 건드리면 안 된다고 경고받았지만, 주인공은 호기심에 보물을 만지게 됩니다. 이로 인해 여관 전체가 마법에 걸리게 되고, 플레이어는 여관을 탐험하며 흩어진 보물들을 찾아 원래 자리로 돌려놓아야 합니다.

---

## 게임 요소 및 맵 설명

### Map_01_Interior
- **불의 검**을 찾는 첫 번째 장소입니다. 플레이어는 여관의 첫 번째 구역을 돌아다니며 불의 검을 찾아야 합니다.
- **블루프린트 기능**: 
  - `BGM_2` 배경음악 재생
  - 게임 개요를 `Print String`으로 표시

### Map_02_Interior
- **물의 방패**를 찾는 두 번째 장소입니다. 여러 마법 몬스터들에게 점령된 구역으로, 물의 방패를 찾아야 합니다.
- **블루프린트 기능**:
  - `Land_of_Mystery` 배경음악 재생
  - 크라켄의 공격 상황 재현 (`Collapse01` 효과음)
  - 
![image](https://github.com/user-attachments/assets/59608774-40e3-4c00-a91b-7b864b9cc6f5)
![image](https://github.com/user-attachments/assets/e188d708-de9a-4f28-b381-c3239429ed9c)

### Map_03_Interior
- **번개의 도끼**, **빛의 활**, **어둠의 창**을 찾는 세 번째 장소입니다. 3개의 보물이 있는 만큼 맵 전체가 붕괴된 느낌을 줍니다.
- **블루프린트 기능**:
  - `Epic_Fantasy` 배경음악 재생
  - 장소 설명을 `Print String`으로 표시
![image](https://github.com/user-attachments/assets/428acb4b-cabc-45de-a0b7-55a374068a19)
![image](https://github.com/user-attachments/assets/5a0b7412-60e1-498b-938c-5de484b03177)
 ![image](https://github.com/user-attachments/assets/d87b22f6-e6d1-4cb1-81c7-2afeb62e4b58)

![image](https://github.com/user-attachments/assets/ed2a3d51-eab0-4e59-9628-54ac1a039511)
![image](https://github.com/user-attachments/assets/9c0359f2-c4dc-4994-a01e-f4b49e7c8f31)

![image](https://github.com/user-attachments/assets/212e69d9-2b38-48a1-97fa-89681fa000ba)
![image](https://github.com/user-attachments/assets/144603ca-bdb1-42ab-b72c-d8eb9845e108)

### Map_06_Interior
- 5개의 보물을 모두 모으면 이동하는 마지막 장소입니다.
- **블루프린트 기능**:
  - `Elven_Realm` 배경음악 재생

---

## 주요 구현 내용

### 보물 블루프린트
- 모든 보물(불의 검, 물의 방패, 빛의 활, 번개의 도끼, 어둠의 창)은 동일한 블루프린트를 공유합니다.
  - **기능**:
    - 플레이어가 보물을 획득하면 `Coin Counter` 증가
    - `Print String`으로 획득 메시지 표시
    - `Coin_short` 효과음 재생
    - 보물 객체 제거 (`Destroy Actor`)
![image](https://github.com/user-attachments/assets/d949465c-3566-4bb1-8a4c-4c72927e80ed)

### 기타 게임 메커니즘
- **움직이는 발판**:
  - `InterpToMovement` 컴포넌트를 활용하여 발판이 지정된 위치를 이동하도록 설정
  - 여러 맵에서 6개의 발판 배치
 ![image](https://github.com/user-attachments/assets/53f8b078-25f2-44f6-9ca2-6fb89fbef486)
 ![image](https://github.com/user-attachments/assets/27310bda-e395-4963-9c4c-7c727e497966)
 ![image](https://github.com/user-attachments/assets/b44fd68e-0eca-42e8-ad8f-54d46270a726)

  
- **슈퍼 점프 발판**:
  - `Duration` 값을 0으로 설정하여 빠르게 움직이는 발판을 구현
  - 플레이어가 발판에서 점프하면 높이 뛸 수 있음
![image](https://github.com/user-attachments/assets/faad3ceb-6554-4b54-8c28-76c23b702f47)

- **맵 이동 문**:
  - 플레이어가 문에 닿으면 `Open Level(by Name)`을 통해 다음 맵으로 이동
![image](https://github.com/user-attachments/assets/3e87b2e5-8592-4f62-be7f-bdc33c89336b)

- **몬스터**:
  - 크라켄, 드래곤, 그리폰, 늑대 등 다양한 몬스터 구현
  - 플레이어와 충돌 시 공격 애니메이션 실행
![image](https://github.com/user-attachments/assets/0e043103-7e75-473a-8396-0fc18042f74e)
![image](https://github.com/user-attachments/assets/e2645c30-a273-4dba-8f3c-8bac32020d71)
![image](https://github.com/user-attachments/assets/2fb0eaf9-3a71-4b09-96b5-1da7e27b5ac0)
![image](https://github.com/user-attachments/assets/564c6ee6-b266-4743-8ef1-6a41e4815af6)

![image](https://github.com/user-attachments/assets/b5c8a2dc-4b8a-43a2-9480-8f6bfc293301)
![image](https://github.com/user-attachments/assets/e38ad5c6-b32c-40e8-849c-82d213356d46)

---

## 문제점 및 해결 방안
- **문제**: 맵 이동 시 `CoinCounter` 변수가 초기화되는 현상
  - 게임 종료 조건을 `CoinCounter == 5`로 설정하면 제대로 동작하지 않음
- **해결**: 
  - 마지막 맵(Map_06_Interior)에 보물 3개를 배치하고, `CoinCounter == 3`이 되면 마지막 맵으로 이동하도록 설정

---

## 결론
이번 프로젝트를 통해 **Unreal Engine 5**를 활용한 게임 개발의 기초를 다졌습니다. 블루프린트를 통해 시각적 프로그래밍의 장점을 활용하여 다양한 게임 메커니즘을 구현했고, 여러 에셋을 활용하며 게임의 시각적 완성도를 높였습니다. 또한, **VFX**, **사운드**, **조건 로직** 등을 통해 몰입감 있고 도전적인 게임을 제작할 수 있었습니다.

---

## 실행 방법
1. Unreal Engine 5에서 프로젝트를 엽니다.
2. `Map_01_Interior`부터 시작하여 게임을 진행합니다.
3. 5개의 보물을 모두 찾아 게임을 완성하세요.

---

## 주요 기술 스택
- **Unreal Engine 5**
- 블루프린트 기반 시각적 프로그래밍
- 에셋 활용 및 사용자 정의 에셋 제작
- VFX, 사운드 디자인

---

## 프로젝트 정보
- **과목명**: 가상현실 프로그래밍
- **학생명**: 전민서 (B989046)
