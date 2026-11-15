# 07 — Quality Assurance and Approval

> 문서 역할: 번역 품질, 오류 심각도, 리뷰 상태 및 승인 책임 구분  
> 적용 범위: 모든 번역·검수·배포 검토  
> 문서 상태: SKELETON  
> 기준 근거: `UNKNOWN` (원본 조사 후 기록)  
> 최종 갱신: 미기록

## A. 오류 등급
| 등급 | 뜻 | 예 |
|---|---|---|
| P0 | 데이터 손상·기술 구조 위험 | ID/태그/선택지 연결 훼손 |
| P1 | 의미·서사·안전한 해석 문제 | 반전 정보 오노출, 부정 반전 |
| P2 | 정책·용어·관계 일관성 | 승인 용어/호칭의 잘못된 적용 |
| P3 | 스타일·가독성 | 과도한 장문, 부자연스러운 호흡 |

## B. 검사 방법
자동 점검 가능한 ID·태그·누락과, 문맥 검토가 필요한 의미·관계·시점을 분리한다.

## C. 단위 QA 체크리스트
원문 충실성, 부정·조건·수치, 화자·수신자, 시점·분기, 승인 용어, 표기, 기술 보존, 적용한 문서 경로를 기록한다.

## D. 세 가지 상태 축
- **근거:** `UNKNOWN`/`OBSERVED`/`CONTEXT_CONFIRMED`/`INFERRED`/`CONFLICTED`
- **언어·번역:** `UNTRANSLATED`/`DRAFT`/`CONTEXT_REVIEW`/`LANGUAGE_REVIEW`/`APPROVED_TEXT`/`REJECTED`
- **기술·배포:** `NOT_TESTED`/`TECH_REVIEW`/`RUNTIME_VERIFIED`/`RELEASE_APPROVED`

## E. 승인과 이슈
승인자·승인 일자·적용 범위 없이는 `APPROVED_TEXT`로 표시하지 않는다. 충돌은 [ISSUES](../operations/ISSUES.md), 결정은 [DECISIONS](../operations/DECISIONS.md)에 기록한다.

## F. 검수 이력
문맥/언어 승인과 실제 매체 검증은 별도 [QA 로그](../operations/QA_LOG.md)로 기록한다. 수행하지 않은 검증은 통과로 보고하지 않는다.
