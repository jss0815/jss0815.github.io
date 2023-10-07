---
title: Phaser에서 A, S, D, W 키 사용 방법
date: 2023-09-13 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Phaser
---

## 키보드 이벤트를 Phaser에 연결하기

Phaser는 인기 있는 HTML5 게임 프레임워크입니다. 이 프레임워크를 사용하여 게임 개발을 하다 보면, 자주 A, S, D, W 키를 이용한 캐릭터 움직임을 구현하고 싶을 수 있습니다. 이러한 기능은 Phaser의 `this.input.keyboard.createCursorKeys()` 함수를 확장하여 구현할 수 있습니다.

## 코드 예시와 설명

다음은 Phaser 3에서 A, S, D, W 키를 사용하여 캐릭터를 움직이는 간단한 예시입니다.

```javascript
// 게임 설정
const config = {
    type: Phaser.AUTO,
    width: 800,
    height: 600,
    scene: {
        create: create,
        update: update
    }
};

// 게임 객체 생성
const game = new Phaser.Game(config);

// create 함수
function create() {
    // WASD 키 객체 생성
    this.keys = this.input.keyboard.addKeys('W,S,A,D');
}

// update 함수
function update() {
    // W 키가 눌렸을 경우
    if (this.keys.W.isDown) {
        // 캐릭터 위로 움직임
    }
    // A 키가 눌렸을 경우
    if (this.keys.A.isDown) {
        // 캐릭터 왼쪽으로 움직임
    }
    // S 키가 눌렸을 경우
    if (this.keys.S.isDown) {
        // 캐릭터 아래로 움직임
    }
    // D 키가 눌렸을 경우
    if (this.keys.D.isDown) {
        // 캐릭터 오른쪽으로 움직임
    }
}
```

이 코드에서 `addKeys('W,S,A,D')` 함수는 WASD 키를 게임에 연결합니다. `update()` 함수 내에서는 각 키가 눌렸을 때 어떤 동작을 해야 하는지를 정의합니다.

## 주의사항

WASD 키를 사용하기 전에, 반드시 게임 씬(scene)에서 `create()` 함수를 통해 키 설정을 해야 합니다. 또한 `update()` 함수에서는 실시간으로 키 입력을 확인하여 캐릭터를 움직이게 됩니다.

## 정리

Phaser에서 WASD 키를 사용하여 캐릭터를 움직이려면, 키 설정을 `create()` 함수에서 하고, 실제 움직임은 `update()` 함수에서 구현하면 됩니다. 이렇게 하면 복잡한 설정 없이도 쉽게 키보드 입력을 게임에 적용할 수 있습니다.