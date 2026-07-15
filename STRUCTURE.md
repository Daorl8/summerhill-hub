# STRUCTURE — summerhill-hub

단일 파일 정적 **링크 허브**(벤토 그리드). Cloudflare Workers 정적 자산 배포.
카테고리 = 링크트리식 세로 버튼 스택이 아닌 **브랜디드 미니사이트**(Bento/Taap 계열). 링크트리와의 차이 = 자체 도메인 + 브랜드 디자인 + 이미지 블록.

```
summerhill-hub/
├─ index.html        # 허브 본체
├─ og.jpg            # 1200x630 카톡/OG 전용. ⚠️ **jpg 유지** — 카카오 크롤러의 webp 렌더 보장 없음
├─ sh-c1.webp (1288x724) / sh-c3.webp · sh-g2.webp (632x474) / sh-blog.webp (240x240)
│                    # 표시 크기 2x 로 프리크롭 — object-fit 이 아니라 파일 자체가 맞는 비율
├─ sh-avatar.webp    # 상단 아바타 222px (사장님 실제 케이크 사진, CSS 로 원형)
├─ f-gaegu-b.woff2 / f-pre-r.woff2 / f-pre-sb.woff2   # self-host 서브셋
├─ wrangler.toml     # name=summerhill-hub
├─ .assetsignore     # .git·문서·index_*.html 제외
└─ CHANGELOG.md / STRUCTURE.md
```

## 디자인 토큰 (summerhill-sample 과 동일 — 사장님이 "예쁘다"고 한 톤 유지)
- 크림 `#FCFBF9` / cream2 `#F4EFE6` / card `#FFFFFF`
- ink `#2F2C27` / **ink-soft `#797368`**  (ink-faint 삭제됨 — 크림 위 2.45 미달)
- **caramel `#C9A87C`** = 리본·카톡블록 **면**. 글씨는 **잉크**(6.21) / 부제는 **on-caramel `#4B3823`**(4.96)
- berry `#8B6B47` = **테두리 전용**(크림 위 4.73 → 밝은 면이 배경과 안 갈라지는 걸 테두리로 해결) / berry-deep `#6F5436` = 포커스 아웃라인
- line `#ECE4D6` / ease `cubic-bezier(.22,.61,.36,1)`
- ⚠️ **berry-deep 을 caramel 위 텍스트에 쓰지 말 것 — 3.13 미달.** 반드시 `--on-caramel`.
- 폰트: Gaegu(손글씨 제목 700) + Pretendard(본문 400/600) — **self-host 서브셋**(`f-gaegu-b.woff2` 12.8KB / `f-pre-r.woff2` 10.8 / `f-pre-sb.woff2` 10.8). **외부 도메인 0.**
- ⚠️ **카피를 수정하면 서브셋을 다시 뜰 것.** 페이지에 쓰는 글자만 들어있어서, 새 글자는 폴백(맑은고딕)으로 튄다. 생성 = `fontTools` + 로컬 원본(`fonts/fonts-main/ofl/gaegu`, `fonts/Pretendard-1.3.9`).
- ⚠️ **`--ink-soft`만 원본(#7C766B)과 다름** — 크림 위 4.36 미달이라 #797368로 조정. 원페이지와 톤 비교 시 이 1픽셀 차이는 의도된 것.
- ⚠️ 흰 글씨는 이제 **어디에도 안 씀**. caramel 위 흰 글씨는 2.24 미달.

## 레이아웃 규칙
- **카드형 = 사진 위 / 라벨은 카드 아래.** 사진 위에 글씨를 얹지 않는다 → 밝은 디저트 사진을 어둡게 덮을 필요가 없고 대비가 항상 확보됨. **이 규칙을 깨면 CHANGELOG의 대비 표가 재발한다.**
- 그리드 2열: big(1/-1, 16:9) / small ×2(4:3) / wide(1/-1, 가로형 96~120px 썸네일) / kakao(1/-1, **솔리드 caramel + berry 테두리 + 잉크 글씨**)
- 호버 = 카드 `translateY(-5px)`+그림자 **0.42s** / 사진 `scale(1.055)` **0.7s**, **같은 ease 곡선**. ⚠️ 예전엔 .18s/.5s 로 따로 놀아 어긋나 보였음.
- ⚠️ **`prefers-reduced-motion` 게이트 없음(의도적)** — 있으면 OS 동작줄이기 켠 사람에게 트랜지션이 통째로 죽어 "뚝뚝 끊김"으로 보임. 다올 판단=전원 강제. → [[reduced-motion-kills-smooth-scroll]]
- 카드 썸네일은 `alt=""`(장식) — 라벨이 목적지를 이미 설명하므로 alt 를 넣으면 스크린리더가 링크명에 합쳐 읽음.
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
