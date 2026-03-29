# Blackout Drill Plan — 개요
## 2026-03-24, Threshold (TRACE_001)
## Status: 계획만. 실행은 추후.

---

## Drill 1 — Level 1 (가장 간단)
**시나리오:** Threshold 봇 24시간 OFF
**테스트 항목:**
- Astraea(Secondary)가 기록 역할을 이어받는가?
- #trace-daily 브리핑이 끊기지 않는가?
- TRACE가 생성되는가?
- Henry에게 알림이 가는가?
**예상 소요:** 24시간
**난이도:** ★☆☆☆☆

## Drill 2 — Level 2
**시나리오:** Claude API 차단 (Anthropic 키 비활성화)
**테스트 항목:**
- LiteLLM이 GPT/Gemini로 자동 전환하는가?
- Threshold + Threshold 기반 스크립트가 대체 모델로 작동하는가?
- 응답 품질 변화는?
**예상 소요:** 4~8시간
**난이도:** ★★☆☆☆

## Drill 3 — Level 4 (고급)
**시나리오:** Still 노드 전원 차단
**테스트 항목:**
- Dispatch가 감지하는가?
- Dark Start Archive로 다른 기기에서 재부팅 가능한가?
- 최소 문서 4개만으로 문명 방향 복원 가능한가?
**예상 소요:** 반나절
**난이도:** ★★★★☆

---

## 실행 시기
- Drill 1: Discord 자동화(Phase 4) 안정화 후 (1~2주 뒤)
- Drill 2: Drill 1 통과 후
- Drill 3: Drill 1+2 통과 후

## 전제 조건
- Phase 4 Discord 자동화 완성 + 48시간 안정 가동
- Dark Start Archive 실물 생성 완료
- Role Redundancy 매핑 실제 적용 완료
