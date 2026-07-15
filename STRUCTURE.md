# STRUCTURE — summerhill-hub

단일 파일 정적 **링크 허브**(벤토 그리드). Cloudflare Workers 정적 자산 배포.
카테고리 = 링크트리식 세로 버튼 스택이 아닌 **브랜디드 미니사이트**(Bento/Taap 계열). 링크트리와의 차이 = 자체 도메인 + 브랜드 디자인 + 이미지 블록.

```
summerhill-hub/
├─ index.html        # 허브 본체
├─ sh-c1.jpg / sh-c3.jpg / sh-g2.jpg / sh-about.jpg   # summerhill-sample 에서 재활용
├─ wrangler.toml     # name=summerhill-hub
├─ .assetsignore     # .git·문서·index_*.html 제외
└─ CHANGELOG.md / STRUCTURE.md
```

## 디자인 토큰 (summerhill-sample 과 동일 — 사장님이 "예쁘다"고 한 톤 유지)
- 크림 `#FCFBF9` / cream2 `#F4EFE6` / card `#FFFFFF`
- ink `#2F2C27` / **ink-soft `#797368`** / ink-faint `#A9A296`
- berry `#8B6B47` / berry-deep `#6F5436` / line `#ECE4D6`
- 폰트: Gaegu(손글씨 제목) + Pretendard(본문) — **CDN**(탐색·무료시안 기준)
- ⚠️ **`--ink-soft`만 원본(#7C766B)과 다름** — 크림 위 4.36 미달이라 #797368로 조정. 원페이지와 톤 비교 시 이 1픽셀 차이는 의도된 것.
- ⚠️ **`--ink-faint`는 크림 위 2.45라 텍스트에 쓰지 말 것**(현재 미사용).

## 레이아웃 규칙
- **카드형 = 사진 위 / 라벨은 카드 아래.** 사진 위에 글씨를 얹지 않는다 → 밝은 디저트 사진을 어둡게 덮을 필요가 없고 대비가 항상 확보됨. **이 규칙을 깨면 CHANGELOG의 대비 표가 재발한다.**
- 그리드 2열: big(1/-1, 16:9) / small ×2(4:3) / wide(1/-1, 가로형 96~120px 썸네일) / kakao(1/-1, 솔리드 berry)
- radius 20px + hover lift/shadow = summerhill 고유 언어(네일어반의 각진·플랫과 반대). `@media(hover:hover)` 로 터치 sticky hover 차단.

## 링크 (5)
| 블록 | URL | 노후 |
|---|---|---|
| 클래스 공지·수업 신청 | m.blog.naver.com/summerhill_dessert/223362425603 | **연 1회**(26년 공지) → AS 접점 |
| 카페창업 올인원 | m.blog.naver.com/summerhill_dessert/224320222442 | 상시글 |
| 인스타그램 | instagram.com/summerhill_dessert | 영구 |
| 블로그 전체 보기 | m.blog.naver.com/PostList.naver?blogId=summerhill_dessert&tab=1 | 영구 |
| 카카오톡 | pf.kakao.com/_zxjyNxj | 영구 |

정적 사이트라 납품 후 사장님이 링크를 직접 못 고침 → **안 썩는 링크 위주로 설계**, 썩는 하나(연간 공지)는 AS로 교체.
