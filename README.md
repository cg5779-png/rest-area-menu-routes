# rest-area-menu-routes

한국 고속도로 노선 모양 데이터입니다. 고속도로 휴게소 대표메뉴 앱 「휴슐랭」이 지금 달리는 고속도로와 방향, 다음 휴게소까지의 거리를 계산할 때 씁니다.

이 데이터는 [오픈스트리트맵(OpenStreetMap)](https://www.openstreetmap.org)에서 가공했습니다. 원본과 같은 **ODbL 1.0** 라이선스로 공개합니다.

## 파일

- `routes.json`: 고속도로 노선별 모양

```json
{
  "source": "고속도로 모양: © OpenStreetMap contributors",
  "license": "ODbL 1.0",
  "builtAt": "2026-10-11",
  "routes": [
    {
      "id": "0010",
      "name": "경부선",
      "directions": ["부산", "서울"],
      "path": [[37.5287, 127.009], [37.472, 127.039]]
    }
  ]
}
```

| 항목 | 뜻 |
|---|---|
| `id` | 한국도로공사 노선 코드 (앱에서만 쓰는 구간 코드는 `0650-pohang`처럼 뒤에 이름이 붙음) |
| `name` | 노선 이름 |
| `directions` | `[선의 끝 쪽으로 가는 방향 이름, 시작 쪽으로 가는 방향 이름]` |
| `path` | `[위도, 경도]` 점들. 실제 길에서 약 100m 넘게 벗어나지 않는 선에서 점을 줄였고, 좌표는 소수점 4자리까지만 씀 |
| `loop` | 순환선이면 `true` (선의 끝이 시작으로 이어짐) |
| `gaps` | 빈 구간 번호 목록. `i`는 `path[i]`→`path[i+1]` 사이를 뜻함. 다른 고속도로와 함께 쓰는 구간처럼 이 노선의 도로 자료가 없어 직선으로 이은 곳 |
| `landmarks` | 순환선에서 "다음 큰 지점"으로 보여 주는 곳 (앱 개발자가 직접 정한 대략적인 위치이며, 오픈스트리트맵 자료가 아님) |

## 만든 방법

1. [Overpass API](https://overpass-api.de)로 오픈스트리트맵의 한국 고속국도 노선 관계(`type=route`, `route=road`, `network=KR:expressway`)를 내려받았습니다.
2. 노선의 도로 조각들을 한쪽 차로를 따라 하나의 선으로 이었습니다.
3. 한 노선 번호에 여러 구간이 함께 들어 있는 경우(예: 동해선의 부산–포항, 포항–영덕, 삼척–속초 구간)에는 구간별로 잘랐습니다.
4. 더글러스-포이커 방식으로 점을 줄였습니다(허용 오차 약 100m).

## 라이선스

이 데이터베이스(`routes.json`)는 [Open Database License (ODbL) v1.0](https://opendatacommons.org/licenses/odbl/1-0/)을 따릅니다.

- 출처: **© OpenStreetMap contributors** — <https://www.openstreetmap.org/copyright>
- 이 데이터를 쓰거나 고쳐서 배포할 때도 같은 ODbL 조건과 출처 표시를 지켜 주세요.

휴게소·메뉴 정보는 이 저장소에 들어 있지 않습니다. 그 정보는 한국도로공사 공공데이터를 따로 사용합니다.
