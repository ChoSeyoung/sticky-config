# sticky-config

[Sticky](https://github.com/ChoSeyoung/sticky) iOS 앱의 원격 설정 파일을 모아두는 저장소입니다.
실제 서빙은 jsDelivr CDN을 통해 이루어집니다.

## force-update.json

설치된 앱 버전과 비교해 강제 업데이트 여부를 결정하는 manifest.

**서빙 URL** (앱 코드가 가리키는 위치):

```
https://cdn.jsdelivr.net/gh/ChoSeyoung/sticky-config@main/force-update.json
```

### 스키마

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| `minimumRequiredVersion` | string | 이 값 미만 버전은 강제로 차단되고 App Store로 안내됩니다. |
| `latestVersion` | string | (예약) 소프트 알림용. 현재 코드는 사용하지 않습니다. |
| `appStoreURL` | string | 차단 화면의 "업데이트" 버튼이 여는 App Store 링크. |
| `title` | string? | 차단 화면 제목. 생략 시 앱 내 기본 문구 사용. |
| `updateMessage` | string? | 차단 화면 본문. 생략 시 앱 내 기본 문구 사용. |

### 운영 규칙

- 앱 측은 fail-open: manifest를 못 받으면 차단하지 않습니다. 잘못된 JSON을 올려도 사용자가 잠기진 않지만, 강제 업데이트도 발동하지 않으니 `JSON.parse` 가능 여부는 푸시 전 반드시 확인하세요.
- 강제 업데이트를 즉시 반영하려면 jsDelivr purge가 필요합니다:
  ```
  curl https://purge.jsdelivr.net/gh/ChoSeyoung/sticky-config@main/force-update.json
  ```
  purge 없이도 12시간 이내에는 반영됩니다.
- `appStoreURL`은 App Store 등록이 끝난 뒤 실제 ID로 교체해야 합니다 (현재는 placeholder).
