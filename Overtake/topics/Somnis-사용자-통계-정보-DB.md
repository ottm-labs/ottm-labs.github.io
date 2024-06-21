# Somnis 업적용 사용자 통계 정보 DB

### 개요
- 이 문서는 Somnis의 업적용 사용자 통계 정보 DB 구성에 대해 설명하고 있습니다.

### 상세
#### DB 필드 값 (MySql)
| id   | 필드명 (DB Column)                   | 필드 설명                              | 값 구분      | 관련 퀘스트                               | 비고         |
|------|---------------------------------------|-----------------------------------------|--------------|-------------------------------------------|--------------|
| 1001 | member_uid                            | 플레이어의 ottm member_uid              | varchar(40)  |                                           | Primary Key  |
| 1002 | updated_at                            | row 값 업데이트 UTC 시간                | timestamp    |                                           |              |
| 1003 | created_at                            | row 값 생성 UTC 시간                    | timestamp    |                                           |              |
| 2001 | player_lv                             | 플레이어 현재 레벨                      | int          | 레벨 달성의 장인                          |              |
| 2002 | nova_consumed                         | 누적 노바 소모량                        | bigint       | 노바 소비왕                               |              |
| 2003 | stage_clear_cnt                       | 누적 스테이지 클리어 횟수               | int          | 스테이지 미션 달성자                      |              |
| 2004 | chapter_clear_cnt                     | 누적 챕터 클리어 횟수                   | int          | 챕터 정리의 달인                          |              |
| 2005 | league_win_cnt                        | 누적 리그전 승리 횟수                   | int          | 리그 최후의 승리자 / 리그전 승리(주간)    |              |
| 2006 | rare_card_lv_up_cnt                   | 누적 희귀 카드 레벨업 횟수              | int          | 희귀 카드 레벨업 달인                     |              |
| 2007 | hero_card_lv_up_cnt                   | 누적 영웅 카드 레벨업 횟수              | int          | 영웅 카드 레벨업 달인                     |              |
| 2008 | nft_fusion_cnt                        | 누적 NFT 카드 합성 진행 횟수            | int          | 카드 합성의 달인                          |              |
| 2009 | nft_special_skill_cnt                 | 누적 NFT 카드 합성 특수 스킬 획득 수    | int          | 특수 스킬 획득의 제왕                     |              |
| 2010 | exclusive_gear_craft_cnt              | 누적 전용 장비 아이템 제작 완료 수      | int          | 전용 장비 제작의 달인                     |              |
| 2011 | gem_acquired                          | 누적 보석 획득량                        | bigint       | 보석 수집의 대가                          |              |
| 2012 | gem_consumed                          | 누적 보석 소모량                        | bigint       | 보석 소비왕                               |              |
| 2013 | mode_win_cnt                          | 누적 모드 승리 총 횟수                  | int          | 모드 승리                                 |              |
| 2014 | normal_card_lv_up_cnt                 | 누적 일반 카드 레벨업 횟수              | int          | 일반 카드 레벨업 달인                     |              |
| 2015 | high_card_lv_up_cnt                   | 누적 고급 카드 레벨업 횟수              | int          | 고급 카드 레벨업 달인                     |              |
| 2016 | nft_fusion_single_survive_cnt         | 누적 NFT카드 합성 -> 1장 생존 횟수      | int          | 카드 합성 재료 1장 생존의 달인            |              |
| 2017 | nft_fusion_all_survive_cnt            | 누적 NFT카드 합성 -> 2장 생존 횟수      | int          | 카드 합성 재료 2장 생존의 달인            |              |
| 2018 | gear_craft_cnt                        | 누적 장비 아이템 제작 완료 수           | int          | 일반 장비 제작의 달인                     |              |
| 2019 | shared_gear_craft_cnt                 | 누적 공용 장비 아이템 제작 완료 수      | int          | 공용 장비 제작의 달인                     |              |
| 2020 | gear_lv_up_attempt_cnt                | 누적 장비 아이템 레벨업 시도 횟수       | int          | 장비 레벨업 시도의 달인                   |              |
| 2021 | wood_collected                        | 누적 통나무 채집량                      | bigint       | 통나무 채집의 달인                        |              |
| 2022 | prism_collected                       | 누적 프리즘 채집량                      | bigint       | 프리즘 채집의 달인                        |              |
| 2023 | plasma_collected                      | 누적 플라즈마 채집량                    | bigint       | 플라즈마 채집의 달인                      |              |
| 2024 | essence_collected                     | 누적 에센스 채집량                      | bigint       | 에센스 채집의 달인                        |              |
| 2025 | league_tower_destroy_cnt              | 누적 리그전 타워 파괴 수                | int          | 리그 타워 파괴자                          |              |
| 2026 | item_craft_cnt                        | 누적 기타 아이템 제작 완료 수           | int          | 재료 아이템 제작의 달인                   |              |
| 2027 | gear_lv_up_cnt                        | 누적 장비 아이템 레벨업 성공 수         | int          | 장비 레벨업 성공의 달인                   |              |
| 2028 | town_exploration_cnt                  | 누적 마을 탐험 완료 횟수                | int          | 탐험의 달인                               |              |
| 2029 | daily_mission_clear_cnt               | 누적 일일 임무 완료 횟수                | int          | 일일 임무 성실자 / 일일 임무 완료(주간)   |              |
| 2030 | weekly_mission_clear_cnt              | 누적 주간 임무 완료 횟수                | int          | 주간 임무 성실자                          |              |
| 2031 | nova_quest_clear_cnt                  | 누적 노바 퀘스트 완료 횟수              | int          | NOVA 퀘스트 완료                          |              |
| 2032 | login_at                              | 마지막 로그인 UTC 시간                  | timestamp    | 게임 접속                                 |              |
| 2033 | league_play_cnt                       | 누적 리그전 플레이 횟수                 | int          | 리그전 플레이                             |              |
| 2034 | mode_play_cnt                         | 누적 모드 플레이 횟수                   | int          | 모드 플레이                               |              |
| 2035 | crew_card_fragment_support_cnt        | 누적 크루 내 카드 조각 요청 지원 갯수   | int          | 카드조각 지원 개수                        |              |
| 2036 | card_lv_up_cnt                        | 누적 카드 레벨업 진행 횟수              | int          | 카드 레벨업                               |              |
| 2037 | item_purchase_cnt                     | 누적 상점 아이템 구매 횟수              | int          | 상점 구매                                 |              |
| 2038 | blueprint_draw_cnt                    | 누적 도안 가챠 진행 횟수                | int          | 도안 가챠 진행                            |              |

#### 필드 ID 설명
- 1*** : 데이터 운영/관리를 위한 값
- 2*** : 사용자 업적 검증값으로 사용될 값

#### DB Table 생성 예시 코드 (MySql)
```SQL
create table somnis_player_stats
(
	member_uid varchar(40) not null comment '회원 아이디'
		primary key,
	blueprint_draw_cnt int default 0 not null comment '누적 도안 가챠 진행 횟수',
	card_lv_up_cnt int default 0 not null comment '누적 카드 레벨업 진행 횟수',
	chapter_clear_cnt int default 0 not null comment '누적 챕터 클리어 횟수',
	created_at timestamp default CURRENT_TIMESTAMP not null comment 'row 값 생성 시간 ',
	crew_card_fragment_support_cnt int default 0 not null comment '누적 크루 내 카드 조각 요청 지원 갯수',
	daily_mission_clear_cnt int default 0 not null comment '누적 일일 임무 완료 횟수',
	essence_collected bigint default 0 not null comment '누적 에센스 채집량',
	exclusive_gear_craft_cnt int default 0 not null comment '누적 전용 장비 아이템 제작 완료 수',
	gear_craft_cnt int default 0 not null comment '누적 장비 아이템 제작 완료 수',
	gear_lv_up_attempt_cnt int default 0 not null comment '누적 장비 아이템 레벨업 시도 횟수',
	gear_lv_up_cnt int default 0 not null comment '누적 장비 아이템 레벨업 성공 수',
	gem_acquired bigint default 0 not null comment '누적 보석 획득량',
	gem_consumed bigint default 0 not null comment '누적 보석 소모량',
	hero_card_lv_up_cnt int default 0 not null comment '누적 영웅 카드 레벨업 횟수',
	high_card_lv_up_cnt int default 0 not null comment '누적 고급 카드 레벨업 횟수',
	item_craft_cnt int default 0 not null comment '누적 기타 아이템 제작 완료 수',
	item_purchase_cnt int default 0 not null comment '누적 상점 아이템 구매 횟수',
	league_play_cnt int default 0 not null comment '누적 리그전 플레이 횟수',
	league_tower_destroy_cnt int default 0 not null comment '누적 리그전 타워 파괴 수',
	league_win_cnt int default 0 not null comment '누적 리그전 승리 횟수',
	login_at timestamp default CURRENT_TIMESTAMP not null comment '로그인 시간',
	mode_play_cnt int default 0 not null comment '누적 모드 플레이 횟수',
	mode_win_cnt int default 0 not null comment '누적 모드 승리 총 횟수',
	nft_fusion_all_survive_cnt int default 0 not null comment '누적 NFT카드 합성 -> 2장 생존 횟수',
	nft_fusion_cnt int default 0 not null comment '누적 NFT 카드 합성 진행 횟수',
	nft_fusion_single_survive_cnt int default 0 not null comment '누적 NFT카드 합성 -> 1장 생존 횟수',
	nft_special_skill_cnt int default 0 not null comment '누적 NFT 카드 합성 특수 스킬 획득 수',
	normal_card_lv_up_cnt int default 0 not null comment '누적 일반 카드 레벨업 횟수',
	nova_consumed bigint default 0 not null comment '누적 노바 소모량',
	nova_quest_clear_cnt int default 0 not null comment '누적 노바 퀘스트 완료 횟수',
	plasma_collected bigint default 0 not null comment '누적 플라즈마 채집량',
	player_lv int default 1 not null comment '플레이어 현재 레벨',
	prism_collected bigint default 0 not null comment '누적 프리즘 채집량',
	rare_card_lv_up_cnt int default 0 not null comment '누적 희귀 카드 레벨업 횟수',
	shared_gear_craft_cnt int default 0 not null comment '누적 공용 장비 아이템 제작 완료 수',
	stage_clear_cnt int default 0 not null comment '누적 스테이지 클리어 횟수',
	town_exploration_cnt int default 0 not null comment '누적 마을 탐험 완료 횟수',
	updated_at timestamp default CURRENT_TIMESTAMP not null comment 'row 값 업데이트 시간',
	weekly_mission_clear_cnt int default 0 not null comment '누적 주간 임무 완료 횟수',
	wood_collected bigint default 0 not null comment '누적 통나무 채집량'
);

```

#### OTTM 업적의 검증 (추후 업데이트 예정)

