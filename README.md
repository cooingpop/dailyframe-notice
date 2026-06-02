# dailyframe-notice

`하루한장` 공지사항 JSON 저장소입니다.

## 가장 단순하게 쓰는 방법

공지 한 개는 아래 정도만 알면 됩니다.

```json
{
  "id": "photo-only-supported",
  "title": "사진만으로도 기록 가능",
  "message": "사진만 올리고 저장해도 오늘 기록이 남아요."
}
```

## notices.json 구조

```json
{
  "version": 1,
  "updatedAt": "2026-06-02T22:30:00+09:00",
  "autoSlideSeconds": 5,
  "notices": []
}
```

## 루트 필드 설명

- `version`
  - 공지 데이터 형식 버전입니다.
  - 지금은 `1`로 고정해두고 그대로 두면 됩니다.
- `updatedAt`
  - 마지막 수정 시간입니다.
  - 사람이 보기 위한 용도에 가깝고, 필요하면 갱신하면 됩니다.
- `autoSlideSeconds`
  - 공지 자동 슬라이드 간격입니다.
- `notices`
  - 실제 공지 목록입니다.

## 공지 한 개에 들어가는 필드

### 꼭 필요한 것

- `title`
  - 공지 제목
- `message`
  - 공지 본문

### 있으면 좋은 것

- `id`
  - 공지 고유값
  - 추천은 짧은 영문 슬러그입니다.
  - 예: `open-launch-calendar-event`
  - 비워도 앱이 자동 생성할 수 있게 되어 있지만, 직접 넣는 걸 추천합니다.
- `type`
  - 공지 성격
  - 예: `notice`, `event`, `challenge`
  - 안 쓰면 기본값은 `notice`
- `order`
  - 노출 순서
  - 안 쓰면 파일에 적힌 순서대로 보여줍니다.

### 기간 노출

- `startAt`
  - 노출 시작 시각
- `endAt`
  - 노출 종료 시각

둘 다 없으면 상시 공지로 봅니다.

예:

```json
{
  "title": "오픈 런칭 이벤트",
  "message": "매일 기록이 3개월 쌓이면 월력을 만들 수 있어요.",
  "startAt": "2026-06-01T00:00:00+09:00",
  "endAt": "2026-08-31T23:59:59+09:00"
}
```

### 탭 동작

- `url`
  - 누르면 외부 브라우저로 이동
- `target`
  - 누르면 앱 내부 화면으로 이동
  - 현재 지원값: `calendar`

둘 다 없으면 탭해도 이동하지 않습니다.

예:

```json
{
  "title": "이벤트 자세히 보기",
  "message": "공지 누르면 외부 페이지로 이동해요.",
  "url": "https://github.com/cooingpop/dailyframe"
}
```

### 오른쪽 작은 배지

- `badge.kind`
  - 현재 어떤 진행값을 붙일지
  - 현재 지원값: `readyMonths`
- `badge.goal`
  - 목표 숫자

예:

```json
{
  "title": "오픈 런칭 이벤트",
  "message": "매일 기록이 3개월 쌓이면 월력을 만들 수 있어요.",
  "badge": {
    "kind": "readyMonths",
    "goal": 3
  }
}
```

## 추천 규칙

- 제목은 짧게
- 본문은 두 줄 안으로
- 기간 공지는 `startAt`, `endAt` 같이 쓰기
- 외부 이동은 `url`만 넣기
- 내부 이동은 `target`만 넣기
- 복잡한 `action`, `style`, `visibility`, `progress` 같은 형태는 이제 직접 안 써도 됩니다.
