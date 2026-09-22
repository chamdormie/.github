<p align="center">
  <img src="./assets/domi-mark.png" width="92" alt="참도미" />
</p>

<h2 align="center">참도미 <sub><sup>Cham Domi</sup></sub></h2>

<p align="center">
  기숙사에 들어갈 수 있는지, 그리고 누구와 살게 되는지.
</p>

<p align="center">
  <a href="https://chamdomi.vercel.app"><strong>서비스 사용해 보기 »</strong></a>
</p>

<p align="center">
  숭실대학교 컴퓨터학부 소프트웨어공모전 2026 · <strong>은상</strong>
</p>

<table align="center">
  <tr>
    <td width="33%"><img src="./assets/screen-dorm-search.png" alt="기숙사 검색 — 조건을 입력하면 합격 확률을 예측" /></td>
    <td width="33%"><img src="./assets/screen-match.png" alt="룸메이트 매칭 — 궁합 점수와 성향 태그" /></td>
    <td width="33%"><img src="./assets/screen-chat.png" alt="채팅 — 추천에서 바로 대화로" /></td>
  </tr>
  <tr>
    <td align="center"><sub>조건을 넣으면 합격 확률을 예측</sub></td>
    <td align="center"><sub>궁합 점수와 근거 태그</sub></td>
    <td align="center"><sub>추천에서 바로 대화까지</sub></td>
  </tr>
</table>

기숙사 지원 시즌마다 반복되던 일이 있습니다. 모집 공고를 직접 읽고 내 점수로 들어갈 수 있는지
가늠하고, 룸메이트를 구하려고 여러 커뮤니티 글을 뒤지고, 겨우 연락이 닿으면 외부 메신저로 옮겨
가는 일입니다. 참도미는 이 과정을 한 서비스 안에 모았습니다.

### 추천에 근거를 붙였습니다

성향 추천은 대체로 "이 사람이 잘 맞습니다"라는 결론만 줍니다. 참도미는 **왜 그 사람인지**를 같이
보여 줍니다. 수면 패턴, 흡연, 청소 빈도, 소음, 소통, 성격, 온도, 물건 공유 — 각 항목이 점수에 얼마나
기여했는지 펼쳐서 확인할 수 있고, 같이 살 수 없는 조건은 점수를 매기기 전에 걸러냅니다.

**이 계산에는 LLM을 쓰지 않았습니다.** 입력이 정해진 범주이고, 같은 입력은 항상 같은 결과가 나와야
하며, 화면의 미리보기와 서버의 판정이 어긋나면 안 되기 때문입니다. 두 구현은 같은 golden fixture로
함께 검증하고 최종 판정 권한은 서버에 둡니다. 여기에 생성 모델을 넣으면 추천이 더 좋아진다는 근거
없이 비용과 지연, 비결정성만 늘어난다고 판단했습니다.

관리자 자동 배정은 Robert W. Irving의 **Stable Roommates** 알고리즘을 씁니다. 점수 총합을 최대로
만드는 방식이 전체 만족도는 높일 수 있지만, 서로 바꾸고 싶어 하는 짝(blocking pair)이 남지 않는
개인별 안정성은 보장하지 못합니다. 그래서 총합보다 안정성을 골랐고, 구현은 완전 탐색 오라클과 대조해
검증했습니다. 안정 매칭이 아예 존재하지 않는 입력도 있는데, 그때는 응답이 그 사실을 숨기지 않고
그대로 알려 줍니다.

### 만든 방식

프론트엔드는 Next.js 16과 React 19, 백엔드는 Spring Boot 4와 MySQL, 실시간 채팅은 STOMP,
운영은 k3s와 Helm입니다. 브라우저는 백엔드 원본이나 장기 토큰에 직접 닿지 않고 동일 출처 BFF를
거치며, 로그인 토큰은 URL에 실리지 않습니다. REST 계약은 백엔드 구현에서 생성한 OpenAPI 명세가
기준이고, CI가 명세를 다시 생성해 커밋된 계약과 구현이 어긋나면 실패합니다. 런타임 mock이나 가짜
fallback 데이터는 두지 않았습니다. 백엔드가 응답하지 않으면 화면에 실제 오류가 보입니다.

제품 코드(`FE`, `BE`, `infra`)는 비공개입니다. 동작하는 서비스는
[chamdomi.vercel.app](https://chamdomi.vercel.app)에서 바로 볼 수 있습니다.

숭실대학교 학생 3인이 만들었습니다 —
[@gangdogang](https://github.com/gangdogang) ·
[@ghdtjdwn](https://github.com/ghdtjdwn) ·
[@sammool](https://github.com/sammool)
