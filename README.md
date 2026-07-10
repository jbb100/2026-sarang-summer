# 미션 원정대 네컷 만들기

2026 여름캠프(7/18~19) 현장에서 아이들 사진 4장을 템플릿에 자동 배치해 네컷 이미지를 만드는 도구.

**👉 사용하기: https://jbb100.github.io/2026-sarang-summer/** (PC·모바일 모두 지원, `QR코드.png` 공유 가능)

**🗝️ 코스 3 안내 페이지(어린이용): https://jbb100.github.io/2026-sarang-summer/course3.html** — 골든슛 챌린지 · 말씀 암호 해독 · 신뢰의 미로 (`course3.html`)

**🗺️ 전체 코스 안내(운영용, 9개): https://jbb100.github.io/2026-sarang-summer/courses.html** — 열정·사랑·순종 테마별 3개씩, 난이도순 정리 (`courses.html`)

사진은 서버로 전송되지 않고 전부 기기 안에서만 처리됩니다.

## 현장에서 쓰는 법

**`미션원정대_네컷.html` 파일 하나만 있으면 됩니다.** 인터넷 연결 불필요.

1. 운영용 노트북에 `미션원정대_네컷.html`을 복사 (USB, 카톡 등)
2. 더블클릭해서 브라우저(Chrome/Safari/Edge)로 열기
3. **사진 선택** 버튼으로 4장 선택 — 빈 칸에 순서대로 자동 배치
   - 또는 사진 파일을 원하는 칸에 직접 드래그&드롭
4. 필요하면 미세조정:
   - 사진 드래그 → 위치 이동
   - 마우스 휠 / 슬라이더 → 확대·축소
   - 회전 / 교체 / 삭제 버튼
5. **PNG로 저장** → 다운로드 폴더에 `미션원정대_날짜_시각.png` 생성

폰으로 찍은 사진(세로/가로/EXIF 회전)도 자동으로 올바르게 처리됩니다.

## 출력 규격

- 결과물: 724×2172px (1:3 비율)
- 2×6인치 네컷 스트립 인쇄 시 약 360dpi — 포토프린터·인쇄소 모두 충분한 품질

## 파일 구성

| 파일 | 용도 |
|---|---|
| `미션원정대_네컷.html` | **배포용** — 이미지 내장 완전 독립형, 이 파일만 전달하면 됨 |
| `index.html` | 개발용 소스 (assets 폴더 참조) |
| `assets/template.png` | 템플릿 원본 |
| `assets/overlay.png` | 사진 칸을 투명하게 뚫은 오버레이 (깃발/장식이 사진 위에 보이도록) |

## 수정할 때

`index.html`을 고친 뒤 아래 명령으로 배포용 파일을 다시 만듭니다:

```bash
python3 - <<'EOF'
import base64
html = open('index.html').read()
for name in ['template', 'overlay']:
    b64 = base64.b64encode(open(f'assets/{name}.png', 'rb').read()).decode()
    html = html.replace(f"'assets/{name}.png'", f"'data:image/png;base64,{b64}'")
open('미션원정대_네컷.html', 'w').write(html)
EOF
```

템플릿 이미지를 교체하면 사진 칸 좌표(`index.html`의 `SLOTS`)와 오버레이를 다시 만들어야 합니다.
