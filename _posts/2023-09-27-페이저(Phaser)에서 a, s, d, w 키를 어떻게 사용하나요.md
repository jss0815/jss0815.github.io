---
title: 페이저(Phaser)에서 a, s, d, w 키를 어떻게 사용하나요
date: 2023-09-27 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Phaser
---

## 키보드 이벤트 활성화

페이저(Phaser) 게임 프레임워크에서 키보드 입력을 처리하려면 먼저 `this.input.keyboard.createCursorKeys()` 함수를 사용해 기본 커서 키(상, 하, 좌, 우)를 활성화해야 합니다. 그러나 'a, s, d, w' 같은 특정 알파벳 키를 사용하려면 `this.input.keyboard.addKey()` 함수를 사용해야 합니다.

## 키 이벤트 리스너 설정

키 이벤트 리스너(event listener)란 특정 이벤트(여기서는 키 누름)가 발생했을 때 실행되는 함수입니다. 페이저에서는 이벤트 리스너를 아래와 같이 설정할 수 있습니다.

```javascript
let keyA = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.A);
```

## 키 상태 체크

이제 `update` 함수 내에서 키의 상태를 체크할 수 있습니다. `isDown` 속성을 사용하면 해당 키가 눌렸는지 확인할 수 있습니다.

```javascript
if (keyA.isDown) {
    // 'A' 키가 눌렸을 때 실행할 코드
}
```

## 예제 코드

아래는 페이저를 사용하여 'a, s, d, w' 키 입력을 처리하는 전체 예제 코드입니다.

```javascript
class MyScene extends Phaser.Scene {
    constructor() {
        super({ key: 'MyScene' });
    }
    
    create() {
        let keyA = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.A);
        let keyS = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.S);
        let keyD = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.D);
        let keyW = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.W);
    }
    
    update() {
        if (keyA.isDown) {
            // 'A' 키에 대한 코드
        }
        
        if (keyS.isDown) {
            // 'S' 키에 대한 코드
        }
        
        if (keyD.isDown) {
            // 'D' 키에 대한 코드
        }

        if (keyW.isDown) {
            // 'W' 키에 대한 코드
        }
    }
}
```

이렇게 하면 'a, s, d, w' 키를 감지하고 해당 작업을 수행할 수 있습니다. 페이저에서 키보드 입력을 다루는 것은 이렇게 간단하면서도 효율적입니다. 이 정보가 페이저 게임 개발에 도움이 되길 바랍니다.