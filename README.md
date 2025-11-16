# Cloudflare Geo Test – kururugroup

이 프로젝트는 **Cloudflare Pages** 에서 호스팅되는 단일 정적 웹 페이지이며,  
Cloudflare의 `/cdn-cgi/trace` 엔드포인트를 이용해 접속자의 기본 GEO 정보를 표시합니다.

페이지에서는 다음 정보를 보여줍니다:

- 클라이언트 IP 주소  
- 국가 코드(ISO-3166-1 alpha-2)  
- Cloudflare POP(Edge 데이터센터 위치)

또한 **Cloudflare Worker**를 설정하면 Response Header에  
`KG-IP`, `KG-COUNTRY`, `KG-COLO` 와 같은 커스텀 GEO 헤더를 추가할 수도 있습니다.

---

## 🔧 기술 스택

- **Cloudflare Pages** – 정적 웹사이트 호스팅
- **Cloudflare Workers** (선택사항) – GEO 기반 헤더 추가 및 동적 로직 처리
- **Cloudflare CDN / Edge Network**
- **Vanilla JavaScript** – Trace 파싱 및 UI 출력

---

## 📍 주요 기능

### 1. Cloudflare Geo 정보 표시
`/cdn-cgi/trace` 호출 결과에서 다음 데이터를 추출해 화면에 렌더링합니다:

- `ip` – 실제 클라이언트 IP  
- `loc` – 국가 코드  
- `colo` – Cloudflare POP 코드(ICN, KIX, HKG 등)

또한 raw trace 내용을 그대로 아래에 출력하여 디버깅이 용이합니다.

---

## 📌 2. Worker 기반 커스텀 GEO 헤더 (선택)

Worker를 설정할 경우 응답 헤더에 다음과 같은 항목을 자동 추가할 수 있습니다:
