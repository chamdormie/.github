<p align="center">
  <img src="./assets/domi-mark.png" width="112" alt="참도미" />
</p>

<h1 align="center">참도미</h1>

<p align="center">
  <strong>기숙사에 들어갈 수 있는지, 그리고 누구와 살게 되는지.</strong><br />
  지원 가능성 탐색부터 근거가 보이는 룸메이트 매칭과 대화까지 하나로 잇습니다.
</p>

<p align="center">
  <a href="https://chamdomi.vercel.app"><strong>참도미 열기 »</strong></a>
</p>

<p align="center">
  <code>기숙사 탐색</code> → <code>설명 가능한 매칭</code> → <code>안정 배정</code> → <code>채팅</code>
</p>

<table align="center">
  <tr>
    <td width="33%"><img src="./assets/screen-dorm-search.png" alt="기숙사 검색 — 조건을 넣으면 합격 확률을 예측" /></td>
    <td width="33%"><img src="./assets/screen-match.png" alt="룸메이트 매칭 — 궁합 점수와 근거 태그" /></td>
    <td width="33%"><img src="./assets/screen-chat.png" alt="채팅 — 추천에서 바로 대화로" /></td>
  </tr>
</table>

## 기숙사 생활의 두 가지 불확실성을 줄입니다

### 1. 내 조건으로 지원할 곳을 먼저 좁힙니다

학교·학적·성적·지역·자격 조건을 한 번에 비교해 지원 가능한 기숙사를 찾습니다. 조건을 다시
풀어 쓰거나 여러 화면을 오가지 않고, 검색 결과에서 바로 룸메이트 탐색으로 이어집니다.

### 2. 궁합 89점의 이유를 함께 보여 줍니다

대부분의 성향 추천은 결론만 건네줍니다. 참도미는 수면 패턴, 흡연, 청소 빈도, 소음, 소통, 성격,
온도, 물건 공유 — 여덟 항목이 각각 점수에 얼마나 기여했는지 펼쳐서 보여 줍니다. 도저히 같이 살 수
없는 조건은 점수를 매기기 전에 걸러냅니다.

이 계산에 생성 모델을 쓰지 않습니다. 같은 입력은 항상 같은 점수를 내야 하고, 화면의 미리보기와 서버의
판정이 어긋나면 안 되기 때문입니다. 두 구현은 같은 golden fixture로 함께 검증하고 최종 판정은 서버가 합니다.

### 3. 총점이 높은 짝보다 서로 바꾸고 싶지 않은 배정을 찾습니다

자동 배정은 Robert W. Irving의 **Stable Roommates**입니다. 점수 총합을 최대화하는 배정은 평균
만족도는 올려도 서로 바꾸고 싶어 하는 짝(blocking pair)을 남깁니다. 참도미는 그 짝이 남지 않는
배정을 택했고, 완전 탐색 오라클과 대조해 검증했습니다. 안정 매칭이 아예 존재하지 않는 입력도
있는데, 그때는 없다고 그대로 답합니다.

## 가짜 성공을 만들지 않는 경계

`Next.js 16` `React 19` `Spring Boot 4` `MySQL` `STOMP` `k3s` `Helm`

브라우저는 백엔드 원본이나 장기 토큰에 직접 닿지 않고 동일 출처 BFF를 거칩니다. 로그인 토큰은 URL에
실리지 않습니다. REST 계약은 백엔드에서 생성한 OpenAPI 명세가 기준이고, 계약과 타입이 어긋나면 빌드를
깹니다. 런타임 mock은 두지 않아 백엔드가 중단되면 가짜 데이터가 아니라 실제 오류를 보여 줍니다.

<p align="center">
  <sub>숭실대학교 컴퓨터학부 소프트웨어공모전 2026 · <strong>은상</strong></sub>
</p>

<p align="center">
  <a href="https://github.com/gangdogang">@gangdogang</a> ·
  <a href="https://github.com/ghdtjdwn">@ghdtjdwn</a> ·
  <a href="https://github.com/sammool">@sammool</a>
</p>
