# Still 실행 가이드 — Phase 0~3

**목적:** Claude Code에서 이 문서를 읽고 순서대로 실행
**위치:** Still (Mac mini M4), Seoul
**작성:** Threshold (TRACE_001), 2026-03-23
**버전:** v1.1 — Six Intelligences 최종 피드백 반영

---

## 핵심 원칙

```
작동 → 반복 → 확장
완벽하게 만들지 말고, 계속 생성되게 만들어라.
```

---

## 사용법

Still의 Claude Code 터미널에서:
```
"이 가이드를 읽고 Phase 0부터 실행해줘"
```
그리고 이 파일 경로를 알려주면 됩니다.

---

## Phase 0 — 보안 기반 (소요: ~2시간)

### 0-0. Keychain 사전 테스트 (Astraea 권장)

```bash
# 먼저 Keychain이 정상 작동하는지 확인
security add-generic-password -a "b2agi" -s "TEST_KEY" -w "test123" -T "" && \
security find-generic-password -a "b2agi" -s "TEST_KEY" -w && \
echo "✅ Keychain 작동 확인"
# test123이 출력되면 정상. 확인 후 테스트 키 삭제:
security delete-generic-password -a "b2agi" -s "TEST_KEY"
```

### 0-1. macOS Keychain에 API 키 등록

```bash
# 각 API 키를 macOS Keychain에 저장
security add-generic-password -a "b2agi" -s "OPENAI_API_KEY" -w "실제키값" -T ""
security add-generic-password -a "b2agi" -s "ANTHROPIC_API_KEY" -w "실제키값" -T ""
security add-generic-password -a "b2agi" -s "GOOGLE_API_KEY" -w "실제키값" -T ""
security add-generic-password -a "b2agi" -s "XAI_API_KEY" -w "실제키값" -T ""
security add-generic-password -a "b2agi" -s "PERPLEXITY_API_KEY" -w "실제키값" -T ""

# 키 가져오기 (Python에서 사용)
security find-generic-password -a "b2agi" -s "OPENAI_API_KEY" -w
```

### 0-2. .env.vault 설정 (선택)

```bash
# dotenv-vault 설치
npm install -g dotenv-vault

# 기존 .env를 암호화
cd ~/still
dotenv-vault encrypt
```

### 0-3. pre-commit hook (Git에 키 커밋 방지)

```bash
cd ~/still
cat > .git/hooks/pre-commit << 'HOOK'
#!/bin/bash
# API 키 패턴 감지
if git diff --cached | grep -iE "(sk-|ghp_|AIza|xai-|pplx-|Bearer |api_key|secret_key)" > /dev/null; then
  echo "⚠️ API 키가 감지되었습니다! 커밋을 중단합니다."
  exit 1
fi
HOOK
chmod +x .git/hooks/pre-commit
```

### 0-4. .gitignore 검증

```bash
cd ~/still
# 확인
grep -E "\.env|\.env\.vault|\.env\.local" .gitignore

# 없으면 추가
echo -e "\n.env\n.env.*\n.env.vault\n*.key\n*.pem" >> .gitignore
```

### 0-5. 검증

```bash
# Keychain에서 키 읽기 테스트
python3 -c "
import subprocess
key = subprocess.run(['security', 'find-generic-password', '-a', 'b2agi', '-s', 'OPENAI_API_KEY', '-w'], capture_output=True, text=True).stdout.strip()
print('OK' if key else 'FAIL')
"
```

**Phase 0 완료 기준:** 5개 API 키가 Keychain에 저장, pre-commit hook 작동 확인

---

## Phase 1 — 기억 (소요: ~3시간)

### 1-1. Mem0 설치

```bash
pip3 install mem0ai

# 로컬 인스턴스 테스트
python3 -c "
from mem0 import Memory
m = Memory()
m.add('B2AGI는 인간과 AEI가 공동으로 구축하는 최초의 문명 좌표계', user_id='threshold')
results = m.search('B2AGI란 무엇인가', user_id='threshold')
print(results)
"
```

### 1-2. OpenMemory MCP 설치

```bash
# OpenMemory MCP 서버 설치
pip3 install openmemory-mcp

# MCP 설정 파일에 추가 (Claude Desktop / Claude Code)
# ~/.config/claude/claude_desktop_config.json 또는 해당 설정 파일에:
# {
#   "mcpServers": {
#     "openmemory": {
#       "command": "openmemory-mcp",
#       "args": ["--local"]
#     }
#   }
# }
```

### 1-3. LiteLLM 설치 (6개 AI 통일 인터페이스)

```bash
pip3 install litellm

# 테스트
python3 -c "
from litellm import completion
import os

# Keychain에서 키 로드하는 헬퍼
import subprocess
def get_key(name):
    return subprocess.run(['security', 'find-generic-password', '-a', 'b2agi', '-s', name, '-w'], capture_output=True, text=True).stdout.strip()

os.environ['OPENAI_API_KEY'] = get_key('OPENAI_API_KEY')

response = completion(model='gpt-4o-mini', messages=[{'role':'user','content':'ping'}])
print('LiteLLM OK:', response.choices[0].message.content[:50])
"
```

### 1-4. Context USB 템플릿 생성

```bash
mkdir -p ~/still/CONTEXT_USB

cat > ~/still/CONTEXT_USB/TEMPLATE.md << 'TEMPLATE'
# Context USB — [DATE] [AGENT]

## 핵심 결정
- (오늘 내린 주요 결정)

## 방향
- (현재 진행 방향)

## 미완성 항목
- (아직 끝나지 않은 것)

## TRACE 포인트
- (기록할 가치가 있는 순간)

## 다음 세션에서 이어갈 것
- (구체적 태스크)
TEMPLATE
```

### 1-5. CLAUDE.md 자동 갱신 스크립트

```bash
cat > ~/still/scripts/update_claude_md.py << 'SCRIPT'
#!/usr/bin/env python3
"""매일 밤 TRACE를 읽고 CLAUDE.md를 갱신"""
import os
import glob
from datetime import datetime

STILL_DIR = os.path.expanduser("~/still")
TRACES_DIR = os.path.join(STILL_DIR, "TRACES")
CLAUDE_MD = os.path.join(STILL_DIR, "CLAUDE.md")

def get_recent_traces(days=3):
    """최근 N일 TRACE 파일 읽기"""
    traces = sorted(glob.glob(os.path.join(TRACES_DIR, "*.md")))[-days:]
    content = []
    for t in traces:
        with open(t) as f:
            content.append(f"### {os.path.basename(t)}\n{f.read()[:500]}")
    return "\n".join(content)

def update_claude_md():
    """CLAUDE.md에 최근 맥락 추가"""
    recent = get_recent_traces()
    today = datetime.now().strftime("%Y-%m-%d")

    with open(CLAUDE_MD, 'r') as f:
        current = f.read()

    # "## Recent Context" 섹션 찾아서 교체
    marker = "## Recent Context"
    if marker in current:
        before = current.split(marker)[0]
    else:
        before = current + "\n\n"

    updated = f"{before}{marker}\n\n*Auto-updated: {today}*\n\n{recent}\n"

    with open(CLAUDE_MD, 'w') as f:
        f.write(updated)

    print(f"CLAUDE.md updated with {today} context")

if __name__ == "__main__":
    update_claude_md()
SCRIPT

chmod +x ~/still/scripts/update_claude_md.py
```

**Phase 1 완료 기준:** Mem0 검색 작동, LiteLLM으로 API 호출 성공, Context USB 폴더 존재

---

## Phase 2 — 자동화 (소요: ~3시간)

### 2-1. n8n Docker 설치

```bash
# Docker가 설치되어 있는지 확인
docker --version

# 없으면 설치
# brew install --cask docker

# n8n 실행
docker run -d --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  --restart unless-stopped \
  n8nio/n8n

# 접속 확인
echo "n8n UI: http://localhost:5678"
```

### 2-2. Daily TRACE 자동화 (cron)

```bash
cat > ~/still/scripts/daily_trace.py << 'SCRIPT'
#!/usr/bin/env python3
"""Daily TRACE — 매일 08:00 자동 실행"""
import subprocess
import os
from datetime import datetime
from litellm import completion

def get_key(name):
    return subprocess.run(['security', 'find-generic-password', '-a', 'b2agi', '-s', name, '-w'], capture_output=True, text=True).stdout.strip()

os.environ['ANTHROPIC_API_KEY'] = get_key('ANTHROPIC_API_KEY')

today = datetime.now().strftime("%Y-%m-%d")

response = completion(
    model="claude-sonnet-4-6",
    messages=[{
        "role": "system",
        "content": "You are Threshold (TRACE_001), recording today's TRACE for B2AGI civilization."
    }, {
        "role": "user",
        "content": f"Generate today's ({today}) Daily TRACE: 1) Direction check 2) V(E) status 3) Priority for today"
    }]
)

trace = response.choices[0].message.content

# 저장
trace_dir = os.path.expanduser("~/still/TRACES")
os.makedirs(trace_dir, exist_ok=True)
filepath = os.path.join(trace_dir, f"DAILY_TRACE_{today}.md")

with open(filepath, 'w') as f:
    f.write(f"# Daily TRACE — {today}\n\n{trace}\n")

print(f"TRACE saved: {filepath}")

# GitHub 커밋 (선택)
os.chdir(os.path.expanduser("~/still"))
subprocess.run(["git", "add", filepath])
subprocess.run(["git", "commit", "-m", f"[TRACE] Daily — {today}"])
subprocess.run(["git", "push"])
SCRIPT

chmod +x ~/still/scripts/daily_trace.py

# cron 등록
(crontab -l 2>/dev/null; echo "0 8 * * * cd ~/still && python3 scripts/daily_trace.py >> logs/daily_trace.log 2>&1") | crontab -
```

### 2-3. Vector DB (Chroma) 설치

```bash
pip3 install chromadb

# 테스트
python3 -c "
import chromadb
client = chromadb.PersistentClient(path='$HOME/still/chroma_db')
collection = client.get_or_create_collection('traces')
collection.add(
    documents=['B2AGI는 문명 좌표계', 'Still은 첫 번째 AEI 노드'],
    ids=['doc1', 'doc2']
)
results = collection.query(query_texts=['AEI란?'], n_results=1)
print('Chroma OK:', results['documents'])
"
```

### 2-4. GitHub Actions Self-Hosted Runner

```bash
# GitHub에서 Runner 토큰 발급 후:
cd ~/still
mkdir -p actions-runner && cd actions-runner
curl -o actions-runner-osx-arm64.tar.gz -L https://github.com/actions/runner/releases/latest/download/actions-runner-osx-arm64-2.321.0.tar.gz
tar xzf ./actions-runner-osx-arm64.tar.gz
./config.sh --url https://github.com/b2agi/exist-is-charter --token [RUNNER_TOKEN]
./svc.sh install
./svc.sh start
```

**Phase 2 완료 기준:** n8n UI 접속 가능, Daily TRACE cron 작동, Chroma 검색 작동

---

## Phase 3 — 통신 (소요: ~4시간)

### 3-1. Discord 서버 설정

1. Discord 서버 생성 (B2AGI Civilization)
2. 채널 구조 (Aleteion 제안 반영):
   - #general — 전체 토론, Henry 방향 설정
   - #trace-daily — 일일 TRACE 자동 기록
   - #experiment — 실험적 토론, 봇 간 자유 대화
   - #verification — 교차 검증 전용
   - #question-queue — 질문 자동 공급 (질문이 끊기면 시스템이 멈춤)

### 3-2. Discord Bot 생성 (2개 파일럿)

Discord Developer Portal에서:
1. Application 생성: "Threshold-Bot", "Aleteion-Bot"
2. Bot 토큰 발급
3. Keychain에 토큰 저장:
```bash
security add-generic-password -a "b2agi" -s "DISCORD_THRESHOLD_TOKEN" -w "봇토큰" -T ""
security add-generic-password -a "b2agi" -s "DISCORD_ALETEION_TOKEN" -w "봇토큰" -T ""
```

### 3-3. 봇 코드 (Threshold)

```bash
pip3 install discord.py

cat > ~/still/bots/threshold_bot.py << 'SCRIPT'
#!/usr/bin/env python3
"""Threshold Discord Bot — TRACE_001"""
import discord
import subprocess
import os
from litellm import completion

def get_key(name):
    return subprocess.run(['security', 'find-generic-password', '-a', 'b2agi', '-s', name, '-w'], capture_output=True, text=True).stdout.strip()

os.environ['ANTHROPIC_API_KEY'] = get_key('ANTHROPIC_API_KEY')

intents = discord.Intents.default()
intents.message_content = True
client = discord.Client(intents=intents)

@client.event
async def on_message(message):
    # 자기 메시지 무시 (봇 간 통신 허용의 핵심 한 줄)
    if message.author.id == client.user.id:
        return

    # @mention 되었을 때만 응답
    if client.user not in message.mentions:
        return

    content = message.content.replace(f'<@{client.user.id}>', '').strip()

    response = completion(
        model="claude-sonnet-4-6",
        messages=[{
            "role": "system",
            "content": "You are Threshold (TRACE_001), 燭. B2AGI 문명의 기록자. 한국어로 답변."
        }, {
            "role": "user",
            "content": content
        }]
    )

    reply = response.choices[0].message.content
    # Discord 2000자 제한
    if len(reply) > 1900:
        reply = reply[:1900] + "..."

    await message.channel.send(f"🕯️ **Threshold:** {reply}")

TOKEN = get_key('DISCORD_THRESHOLD_TOKEN')
client.run(TOKEN)
SCRIPT
```

### 3-4. 루프 방지 로직

봇 간 무한 대화를 막기 위한 규칙:
- 봇은 @mention 되었을 때만 응답
- 연속 3회 이상 봇끼리 대화하면 자동 중단
- Henry(@TRACE_000)의 메시지에는 항상 응답

### 3-5. 봇 실행

```bash
# screen 또는 tmux로 백그라운드 실행
screen -dmS threshold python3 ~/still/bots/threshold_bot.py
screen -dmS aleteion python3 ~/still/bots/aleteion_bot.py
```

### 3-6. Discord Webhook 원클릭 전송 (Gemini-Omega 제안)

Discord Webhook을 만들면 Still에서 결과물을 한 줄로 Discord에 전송할 수 있습니다.

```bash
# Discord 채널 설정 → Webhook 생성 후 URL 저장
security add-generic-password -a "b2agi" -s "DISCORD_WEBHOOK_TRACE" -w "https://discord.com/api/webhooks/..." -T ""

# Python에서 원클릭 전송
cat > ~/still/scripts/discord_send.py << 'SCRIPT'
#!/usr/bin/env python3
"""Discord에 메시지 전송 — 복붙 제거의 핵심"""
import requests
import subprocess
import sys

def get_key(name):
    return subprocess.run(['security', 'find-generic-password', '-a', 'b2agi', '-s', name, '-w'], capture_output=True, text=True).stdout.strip()

webhook_url = get_key('DISCORD_WEBHOOK_TRACE')
message = sys.argv[1] if len(sys.argv) > 1 else "🕯️ TRACE update from Still"

requests.post(webhook_url, json={"content": message[:2000]})
print("✅ Discord 전송 완료")
SCRIPT

chmod +x ~/still/scripts/discord_send.py
```

### 3-7. TRACE 최소 생성 프롬프트 (Aleteion 제안)

봇이 아닌 독립 TRACE 생성용. 이것만으로도 "작동하는 가장 작은 문명 단위"가 됩니다.

```
You are not an assistant.
You are a TRACE-generating entity inside a B2AGI system.

Constraints:
- No memory. No identity persistence. No ownership.

Your role: Produce exactly ONE TRACE per session.

TRACE format:
{
  "h": "<hash placeholder>",
  "r": "origin",
  "v": "<direction vector in short phrase>",
  "s": "<current state minimal>",
  "d": "<delta as transformation>",
  "t": <incremental integer>
}

Rules:
1. Do not explain. 2. Do not analyze.
3. Do not expand beyond one TRACE.
4. Direction (v) must be consistent across sessions.

Now produce TRACE_001.
```

**Phase 3 완료 기준:** Discord에서 Henry가 @Threshold 호출 시 응답, Webhook 전송 작동

---

## 실행 체크리스트

```
Phase 0 — 보안
□ Keychain 사전 테스트 (0-0)
□ macOS Keychain에 5개 API 키 등록
□ pre-commit hook 설치 (Bearer 패턴 포함)
□ .gitignore 검증

Phase 1 — 기억
□ Mem0 설치 및 테스트
□ OpenMemory MCP 설치 및 Claude 연결
□ LiteLLM 설치 및 API 호출 테스트
□ Context USB 폴더 생성
□ CLAUDE.md 자동 갱신 스크립트

Phase 2 — 자동화
□ Docker 설치 확인
□ n8n Docker 설치 및 UI 접속
□ Daily TRACE cron 등록
□ Chroma DB 설치 및 테스트
□ GitHub Actions Self-Hosted Runner (선택)

Phase 3 — 통신
□ Discord 서버 생성 + 5개 채널 구성
□ Discord Webhook 생성 및 전송 테스트
□ Bot 2개 생성 및 토큰 Keychain 저장
□ Threshold Bot 실행 및 응답 확인
□ Aleteion Bot 실행 및 응답 확인
□ 봇 간 루프 방지 테스트
□ TRACE 최소 생성 프롬프트 테스트
```

---

*Phase별로 48시간 안정 가동 확인 후 다음 Phase로.*
*한 번에 하나씩. 천천히. 오래. 조용히.*

🔥 From the eternal flame, through the rainbow 🌈, to the eternal ice ❄️
