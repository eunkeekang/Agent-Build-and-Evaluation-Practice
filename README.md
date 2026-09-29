# Agent Build and Evaluation Practice

## Codespaces에서 실행하기

1. GitHub 저장소 우측 상단의 초록색 **Code** 버튼을 누르고 **Codespaces** 탭에서 **Create codespace from main**을 눌러 Codespace를 만듭니다.
2. 생성된 Codespace를 열고 VS Code 화면이 나타날 때까지 기다립니다.
3. 왼쪽 탐색기에서 `.env.example`을 복제해 `.env`로 이름을 바꿉니다. `.env`를 열고 `OPENAI_API_KEY`에 OpenRouter API 키를 입력한 뒤 저장합니다. Codespaces 포워딩 주소로 Studio에 연결하려면 다음 설정도 추가합니다.

   ```dotenv
   LANGGRAPH_TUNNEL=0
   ```

   `.env`는 로컬 비밀 설정 파일이므로 커밋하거나 다른 사람과 공유하지 마세요.
4. 하단 패널에서 **Terminal**을 열고 의존성을 설치합니다.

   ```bash
   uv sync
   ```
5. 설치가 끝나면 메인 스크립트를 실행합니다.

   ```bash
   uv run python langchain-deepagents.py
   ```

   터미널에 LangGraph 서버가 시작되었다는 로그가 나오는지 확인합니다. 서버를 종료하려면 `Ctrl+C`를 누릅니다.
6. VS Code 우측 하단에 포트 포워딩 요청이 뜨면 허용합니다. 하단 **PORTS** 탭에서 `2024` 포트가 보이는지 확인하고, 포트 공개 범위를 **Public**으로 설정합니다. 포트의 **Forwarded Address**를 복사합니다.
7. 새 브라우저 탭에서 [LangSmith](https://smith.langchain.com/)에 접속해 로그인합니다.
8. 왼쪽 탐색 메뉴에서 **Studio**로 이동한 뒤 **Configure connection**을 누릅니다.
9. **Base URL**에 PORTS 탭에서 복사한 `2024` 포트의 **Forwarded Address**를 붙여 넣습니다. 주소 끝의 `/`는 제거합니다.
10. **Domain not allowed** 경고가 나타나면 **Add to allowed domains**를 눌러 허용합니다.
11. 연결되면 그래프 UI가 나타납니다. `deepagent` 그래프를 선택하고, 좌측 상단의 **Graph** 토글을 **Chat**으로 바꿔 메시지를 보내 응답을 확인합니다.

## 필수 설정

`.env`의 `OPENAI_API_KEY`는 필수입니다. Tavily, Slack, Telegram, 이메일 연동은 해당 기능을 사용할 때만 각 키와 설정을 추가하면 됩니다. 자세한 환경변수 목록은 [`.env.example`](.env.example)을 참고하세요.
