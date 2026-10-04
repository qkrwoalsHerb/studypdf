# StudyPDF

강의 PDF 위에 페이지별로 필기하고, 슬라이드를 넘기는 순간에 맞춰 녹음을 나눠 저장하는 웹 노트.

**데모:** https://qkrwoalsHerb.github.io/studypdf/

## 해결한 문제
50분 강의 녹음은 한 덩어리로 남아 "이 슬라이드 설명이 몇 분쯤이었지?"를 찾기 어렵다.
StudyPDF는 **PDF 페이지를 녹음의 색인**으로 쓴다. 3쪽을 보는 동안의 소리는 3쪽에, 다시 돌아와 들은 보충 설명은 3쪽의 두 번째 구간으로 쌓인다. 녹음을 누르면 그 녹음이 시작될 때 쓰던 필기 위치로 커서가 이동한다.

## 기능
| 기능 | 설명 |
|---|---|
| 페이지별 즉시 녹음 | 페이지를 넘기면 이전 녹음을 마감하고 새 녹음을 바로 시작 |
| 짧은 녹음 정리 | 기준 시간(기본 2초, 1~10초) 안에 넘긴 페이지의 녹음은 삭제 |
| 이어 붙이기 | 삭제 대신 직전에 보던 페이지 녹음 뒤에 붙이는 옵션 |
| 필기 위치 연결 | 녹음 구간 클릭 시 당시 필기 위치로 이동 + 재생 |
| 글자별 색 | 6가지 기본색 + 색상 선택기, 굵게 |
| 저장 위치 | 내 컴퓨터 폴더 또는 Google Drive, 최근 위치 10개 |
| 홈 정렬 | 생성순 / 수정순 / 이름순 |

## 기술
클라이언트 전용 (서버 없음) — PDF.js, MediaRecorder API, IndexedDB, File System Access API, Google Identity Services, Google Drive API v3 (`drive.file`)

## 저장 결과물
```
강의노트/자료구조 3주차/
├── lecture.pdf
├── audio/ p3_xxxx_1.webm …
├── index.json   ← 페이지·녹음·필기 위치 색인
└── notes.html   ← 페이지별 필기 모음
```

## 배포
1. 저장소 `studypdf` 생성 (Public) → `index.html`, `README.md` 업로드
2. Settings › Pages › Branch `main` / `/ (root)` → Save

## Google 로그인 설정 (제작자 1회)
사용자는 "Google로 로그인" 버튼만 누른다. 제작자가 한 번만 설정한다.
1. console.cloud.google.com → 새 프로젝트
2. API 및 서비스 › 라이브러리 → **Google Drive API** 사용
3. OAuth 동의 화면 → 외부 → 앱 이름 StudyPDF, 범위 `drive.file`
4. 사용자 인증 정보 › OAuth 클라이언트 ID → 웹 애플리케이션
   - 승인된 JavaScript 원본: `https://inforuby2017.github.io`
5. 발급된 ID를 `index.html` 맨 위 `GOOGLE_CLIENT_ID = ''`에 붙여넣기
6. 동의 화면이 "테스트" 상태면 등록한 테스트 사용자만 로그인 가능 → 누구나 쓰게 하려면 "앱 게시"

## 동작 환경
Chrome·Edge 권장 (폴더 선택 지원). Firefox·Safari는 내 컴퓨터 저장 시 zip으로 내려받음.
