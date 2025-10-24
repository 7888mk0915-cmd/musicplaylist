# musicplaylist
thisisreal

diff --git a/README.md b/README.md

index d097df6802ad557afef6ed0612e8025d4bc285a9..81ee836d9e2cc32dfa79f4a9728f85c91a670bb9 100644
--- a/README.md
+++ b/README.md
@@ -1,2 +1,52 @@
-# musicplaylist
-thisisreal
+# makeplaylist
+
+플레이리스트 캡쳐 이미지를 업로드하면 서버가 OCR을 통해 곡 제목과 아티스트를 추출하고, YouTube에서 검색해 링크를 달아주는 서비스입니다.
+
+## 구성
+
+- **백엔드**: FastAPI 기반 REST API (`server/`). 이미지 업로드, OCR 처리, YouTube 검색 및 플레이리스트 저장 기능을 제공합니다.
+- **프론트엔드**: 정적 HTML/CSS/JavaScript (`frontend/`). 여러 장의 이미지를 업로드하고 생성된 플레이리스트를 확인할 수 있는 단일 페이지 UI입니다.
+
+## 준비 사항
+
+1. Python 3.11 이상 설치
+2. (선택) Node.js 없이 정적 파일을 그대로 제공하므로 별도 빌드 과정이 필요 없습니다.
+3. [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) 바이너리 설치 (예: macOS의 경우 `brew install tesseract`, Ubuntu의 경우 `sudo apt-get install tesseract-ocr`).
+4. YouTube Data API v3 키 발급 후 `server/.env` 파일에 `YOUTUBE_API_KEY`를 설정합니다. (API 키가 없으면 곡 검색 없이 플레이리스트만 생성됩니다.)
+
+## 설치 및 실행
+
+```bash
+# 서버 의존성 설치
+cd server
+python -m venv .venv
+source .venv/bin/activate
+pip install -r requirements.txt
+
+# 환경 변수 설정
+cp .env.example .env
+# .env 파일을 열어 YOUTUBE_API_KEY 값을 입력하세요.
+
+# 서버 실행
+uvicorn app.main:app --reload
+```
+
+서버가 실행되면 <http://localhost:8000>에서 프론트엔드가, <http://localhost:8000/api/docs>에서 API 문서가 열립니다.
+
+## 주요 API
+
+- `POST /api/upload`: 이미지 파일 리스트(`files`)를 업로드하면 곡 정보와 YouTube 링크가 담긴 플레이리스트를 생성합니다.
+- `GET /api/playlist/{playlist_id}`: 생성된 플레이리스트를 조회합니다.
+
+## 프론트엔드 개발
+
+정적 자산이므로 별도 빌드 없이 `frontend/index.html`을 열거나, FastAPI 서버가 자동으로 서빙합니다. UI 스크립트는 `frontend/src/app.js`, 스타일은 `frontend/src/style.css`에 있습니다.
+
+## 테스트 이미지 팁
+
+- 곡 제목과 아티스트가 명확히 보이는 고해상도 이미지를 사용하세요.
+- 한 번에 많은 이미지를 업로드하면 OCR 시간이 길어질 수 있습니다. 3~5장 정도를 권장합니다.
+
+## 라이선스
+
+이 프로젝트는 학습 목적으로 제작되었습니다.
