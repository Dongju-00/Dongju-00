# 김동주

AI Engineer

모델 학습부터 데이터 수집, 검색, API와 배포까지 직접 연결하는 개발을 해왔습니다.  
지금은 주식·금융 데이터를 다루며 공시 검색과 AI 모의투자 서비스를 만들고 있습니다.

[포트폴리오](https://app.notion.com/p/403890713f1481f886abd44b276d756a) · [개발 기록](https://app.notion.com/p/403890713f148150876ecc1ccf902ac3)

Email : djdj1473@gmail.com

## 수상

| 연도 | 수상 | 프로젝트 |
| :--- | :--- | :--- |
| 2026 | 카카오테크 부트캠프 AI 부하테스트·성능개선 대회 **우수상** | 카카오 약관 RAG |
| 2025 | 한이음 드림업 공모전 창의도전형 **동상** | SugAI |

## 프로젝트

### [스톡스푼](https://github.com/100-hours-a-week/KTB4-11th-AI)

실시간 시장 데이터와 AI 분석을 연결한 모의투자 서비스입니다. 팀 6명 중 AI 개발 2명으로 참여해 시장 데이터 수집, 분석 검증, 공시 학습·검색 평가와 SQS 주문 요청 발행을 맡았습니다.

- 공시 임베딩 LoRA 학습과 GPU 검색 평가를 진행했습니다. 별도 calibration 양성 100문항에서 Qwen3-reranker-4B 재정렬 후 **Recall@5 0.75 → 0.90**을 확인했고, 순위가 나빠진 질문 유형도 따로 기록했습니다.
- 계좌별 순서를 유지하면서 계좌 간 발행을 병렬화했습니다. 1 CPU·512MiB의 테스트에서 요청 1만 건이 **112.986 → 41.938초**로 줄었습니다. 추가 병렬화는 p95가 악화돼 동시성 4를 선택했습니다.

`Python` `PyTorch` `PEFT/LoRA` `LangChain` `PostgreSQL/pgvector` `QuestDB` `SQS FIFO`

[공시 GPU·RAG 평가 기록](https://app.notion.com/p/403890713f1481dcbcddf40d760c4469) · [SQS 병렬도 실험](https://app.notion.com/p/403890713f1481f5bdd0df9c711ee6a8)

### [eric-chatagent](https://github.com/Dongju-00/eric-chatagent)

한국어 언어모델을 직접 구현하고, 일상 대화와 주식 뉴스 질의응답을 연결한 개인 프로젝트입니다.

- 약 **42M 파라미터의 Decoder-only Transformer**를 구현했습니다. 뉴스·대화 데이터를 구성하고 답변 토큰만 학습하는 SFT부터 FastAPI 서빙까지 연결했습니다.
- 뉴스 답변 NLL은 **3.292 → 1.519**로 줄었습니다. 손실 감소은 감소했찌만, 참조 실패와 반복 답변이 부족해 추후 성능 개선할 예정입니다.

`PyTorch` `SentencePiece` `LangGraph` `ChromaDB` `FastAPI` `Docker`

[구현·서빙 회고](https://app.notion.com/p/403890713f148150876ecc1ccf902ac3) · [멀티턴 데이터·학습 기록](https://app.notion.com/p/403890713f1481d3a10ae222e32cc810)

### [카카오 약관 RAG](https://github.com/Dongju-00/kakao-terms-rag)

약관의 조항을 찾아 조건과 예외까지 답하는 RAG 파이프라인입니다. 2인 팀에서 테스트, 성능개선, 문항별 오류 분석, 후보 비교와 제출 검증을 맡았습니다.

- 검색 MRR이 1.0이어도 답변에서 조건·예외가 빠지는 문제가 있었습니다. 모델·프롬프트·조건부 키워드 추출을 통해 공개 테스트 **KeyFact F1 0.7076 → 0.7537**을 확인했습니다.
- T4 16GB에서 Qwen2.5-7B를 NF4 4bit로 로딩하고, 조항 인코딩 후 BGE-M3를 CPU로 옮겼습니다. 초기화 세션의 HTTP **36요청 모두 성공**, 반복별 p95 중앙값은 **82.345초**로 120초 제한을 충족했습니다.

`BM25` `BGE-M3` `RRF` `Qwen2.5` `NF4` `Colab T4`

[실험·기술 선택 기록](https://app.notion.com/p/402890713f148106878ce7adb1de19de)

### [SugAI](https://github.com/Dongju-00/SugAI)

객체 검출·촬영, 당도 예측과 장치 제어를 연결한 딸기 자동 선별 시스템입니다. 데이터 수집·전처리·모델 학습과 Arduino·Jetson 연동을 맡았습니다.

- 학습 사진과 실제 검출 crop의 차이를 확인하고 같은 전처리 과정을 거쳐 재학습했습니다. 촬영 세션을 나눈 5-fold 검증에서 **MAE 1.154**를 기록했습니다. 학습 평균값 기준선 1.864보다 약 38% 낮았습니다.
- 증강, 기존 가중치 미세조정, 모델 축소 등을 비교하고, 성능이 나빠진 구성은 제외하고 촬영 조건과 데이터 중복의 영향도 함께 점검했습니다.

`PyTorch` `YOLOv5` `SORT` `OpenCV` `FastAPI` `Arduino` `Jetson`

[개발 회고](https://app.notion.com/p/403890713f148153a78be35f9e1d901d) · [실험 기록](https://app.notion.com/p/403890713f14811499a2ee69f8f34afa)

### [Pawprint](https://github.com/Dongju-00/KTB-hackerton-team5-ai)

반려견 사진을 행동·상황에 따라 7개 카테고리로 정리하는 분류 모델입니다. 이미지 수집·정제와 모델 학습·평가를 맡았습니다.

- CLIP으로 상황 의사라벨 후보를 만들고 pHash 중복 제거·YOLO 객체 검증을 거쳤습니다. 데이터 균형화와 모델 변경 후 **Top-1 65.26 → 87.00%, Macro F1 0.630 → 0.869**를 관측했습니다.
- 개체 수로 상황 분류를 보정하면 혼동이 줄어들 것이라 예상했지만, 별도 실험의 정확도는 **76.10 → 74.21%**로 낮아져 강제 제한을 제외했습니다.

`PyTorch` `CLIP` `YOLOv8n` `EfficientNet` `pHash`

[데이터·학습·실험 기록](https://app.notion.com/p/402890713f14817884a9eb9017ce5301)

## 주로 사용하는 기술

| 분야 | 기술 |
| :--- | :--- |
| 모델·데이터 | Python, PyTorch, Transformers, PEFT/LoRA, SentencePiece, NumPy, pandas |
| 검색·Agent | LangChain, LangGraph, pgvector, ChromaDB, RAGAS |
| 서비스·운영 | FastAPI, PostgreSQL, QuestDB, Valkey, SQS, Docker, EC2, CloudWatch, GitHub Actions |

## 학력·활동

- 수원대학교 미디어소프트웨어학과 · 2020.03–2027.02
- 수원대학교 학부 연구생 · 2024.06–2025.06
- 카카오테크 부트캠프 AI 실무개발 과정 · 2026.05–2026.11
