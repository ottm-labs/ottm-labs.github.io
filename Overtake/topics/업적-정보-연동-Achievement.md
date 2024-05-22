# 유저 업적 정보 등록(Achievement)
> [Open Api ui](%partner-api-base%/achievement/swagger-ui/index.html)
### 개요

1. OTTM Achievement 서버를 통해 유저의 업적 진행도 정보를 연동할 수 있습니다
2. 달성한 업적에 관련된 메타 정보는 사전에 OTTM과 공유가 되어있어야 합니다.
3. 유저가 OTTM의 멤버인 경우에만 연동이 가능합니다.

### **Flow**

```mermaid
sequenceDiagram
autonumber
participant partner as 협력사
participant ottm_achievement as OTTM_업적
participant ottm_quest as OTTM_퀘스트
participant ottm_web as OTTM_WEB

alt 업적 정보 등록
partner ->> +ottm_achievement: 유저 업적 진행도 등록
end

alt 업적 정보 조회 (OTTM Internal)
ottm_web ->> +ottm_quest: 유저 퀘스트 진행도 확인
ottm_quest ->> +ottm_achievement: 멤버 업적 진행도 조회
ottm_achievement ->> +ottm_quest: 멤버 업적 진행도  응답
ottm_quest ->> +ottm_web: 유저 퀘스트 진행도 응답
end

```