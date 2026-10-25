# ⚽ 축구 공략 (Goal Rush)

수비진을 뚫고 골을 넣는 HTML5 웹게임. 10개 스테이지를 공략하세요!

**🎮 플레이:** https://worksenddl2-source.github.io/soccer-strategy-game/

> 📅 2026-10-25 실습 · HTML 파일 하나(`index.html`)로 동작 · GitHub Pages 배포

---

## 🎯 학습 목표
1. 캔버스 게임의 기본 구조(게임 루프 = 입력 → 갱신 → 그리기)를 이해한다.
2. 스테이지마다 난이도를 숫자로 조절하는 방법을 익힌다.
3. HTML 파일 하나로 된 웹게임을 GitHub Pages에 배포할 수 있다.

---

## 🕹 게임 방법

파란 팀 공격수를 조종해 빨간 수비수와 골키퍼를 뚫고 골을 넣으세요.

- **10개 스테이지**: 올라갈수록 수비수가 많아지고 빨라지며, 골키퍼 반응도 좋아집니다. 필요한 골 수도 1개에서 3개까지 늘어납니다.
- **공격 기회 제한**: 아래 상황이 되면 기회가 하나 줄어듭니다.
  - 태클을 당함 · 패스가 끊김 · 키퍼가 막음 · 공이 나감 · 12초가 지남
- **슛 파워 충전**: 길게 눌러 파워를 모읍니다. 세게 찰수록 더 많이 빗나갑니다.
- **패스**: 동료에게 패스하면 조종하는 선수가 바뀝니다.
- **질주**: 스태미나를 써서 빠르게 달립니다.
- 점수가 매겨지고, 최고 점수는 브라우저에 저장됩니다.

## 🎮 조작법

| 동작 | PC | 모바일 |
|---|---|---|
| 이동·드리블 | WASD / 방향키 | 가상 조이스틱 |
| 슛 | Space 또는 마우스 클릭을 길게 눌러 충전 후 떼기 | 슛 버튼 |
| 조준 | 마우스 | — |
| 패스 | E / 우클릭 | 패스 버튼 |
| 질주 | Shift | 질주 버튼 |

---

## 🧩 코드 구조

모든 코드가 `index.html` 하나에 들어 있습니다. 전형적인 게임 루프 형태입니다.

```
loop() ──┬── update()   입력(inputVec) → 선수 이동(moveToward) → 슛/패스 → 판정(endAttack)
         └── render()   drawPitch → drawPlayer → drawBall → drawAim → drawUI

stageConfig(n) → setupStage() → setupAttack()     스테이지 난이도 → 선수 배치
```

| 함수 | 역할 |
|---|---|
| `stageConfig` | 스테이지 번호로 수비수 수·속도·키퍼 반응·필요 골 수 결정 |
| `setupStage` / `setupAttack` | 스테이지 시작, 공격 기회마다 선수와 공 배치 |
| `inputVec` / `aimPoint` | 키보드·조이스틱 입력을 방향 벡터로, 마우스를 조준점으로 |
| `shoot` / `pass` | 충전한 파워로 슛(파워가 클수록 오차 증가), 동료에게 패스 |
| `endAttack` | 태클·차단·선방·아웃·시간 초과 판정 후 기회 차감 |
| `burst` / `updateParticles` | 골 넣었을 때 파티클 효과 |
| `saveBest` | 최고 점수를 브라우저에 저장 |

---

## 🚀 GitHub Pages 배포 순서

```bash
git init -b main
git add . && git commit -m "Add soccer strategy web game"
gh repo create soccer-strategy-game --public --source=. --remote=origin --push
```
1. 위 명령으로 저장소를 만들고 코드를 올립니다.
2. 저장소 **Settings → Pages**에서 `main` 브랜치를 배포 대상으로 켭니다.
3. 1~2분 기다린 뒤 `https://<계정>.github.io/<저장소>/`에 접속해 확인합니다.

> 💡 GitHub Pages는 `index.html`을 첫 화면으로 보여줍니다. 그래서 게임 파일 이름을 `index.html`로 둡니다.

---

## 📝 확인 문제
1. `update()`와 `render()`를 나누면 어떤 점이 좋을까?
2. 슛 파워가 클수록 빗나가게 만든 이유는?
3. 새 스테이지를 추가하려면 어떤 함수를 고치면 될까?

---

## ⚠️ 상태
- GitHub Pages 배포 완료, 사이트 접속 확인(HTTP 200)
- 스크립트 문법 검사는 통과했지만, 브라우저에서 직접 플레이 테스트는 아직 하지 않았습니다.
