# (팀 미션) 뉴스 요약 자동화 #  

매일 수많은 뉴스가 쌓이는 정보중에서 "내가 정말 놓치면 안 되는 중요한 키워드"나 "특정 주제"가 포함된 정보들을 요약된 내용을 모아서 볼 수 있는 시나리오입니다.  

목표  
*RSS 피드에서 자동으로 뉴스를 수집하고, AI로 요약한 후, 노션 데이터베이스에 저장하는 완전 자동화 워크플로우 구축*  

------------  
## ⭐  시스템 아키텍처  ⭐   
------------  
####  최종 파이프라인 (단일 흐름)   :  RSS(2) → OpenAI(5) → Notion(8)  

1. 각 단계별 구조 및 역할  
    - Trigger (1개): RSS (새 정보 도착)
    - Filter (1개): 필터를 사용하여 뉴스 제목에 '특정 키워드(네이버)'가 있으면 넘어 감
    - OpenAI (1개): AI 요약
    - Action (1개): Notion 기록 (데이터베이스 기록)

2. 주요 기능  
     ✅ RSS 피드 자동 감지 (새 항목만)  
     ✅ 키워드 필터링 (네이버 주식 관련)  
     ✅ AI 요약 (OpenAI GPT-4o-mini)  
     ✅ URL 자동 정제 및 디코딩  
     ✅ 노션 자동 저장  
     
####  WORKFLOW 
<img width="739" height="486" alt="image" src="https://github.com/user-attachments/assets/7ae0af1d-fbc3-4255-99f7-79fe9df26709" />

1. 모듈별 상세 설명  
### 📌 Module 2 - RSS
  - *역할: 새 정보 감지*
  - *주기: 15분 간격으로 정기적으로 실행*  

### 📌 Module 5 - OpenAI / Generate a completion ⭐ 핵심 모듈
  - *역할: 뉴스 요약*  
  - *모델: GPT-4o*  
  - *프롬프트 구조*  
    
            너는 주식 투자 정보를 정리하는 애널리스트야.
            뉴스를 투자자 관점에서 간결하게 요약해줘.
            아래 뉴스를 다음 형식으로 정리해줘:
            
            📌 제목: (핵심을 담은 한 줄 제목)
            
            📝 요약:
            - (핵심 내용 1)
            - (핵심 내용 2)
            - (핵심 내용 3)
            
            🏷️ 키워드: (쉼표로 구분된 핵심 키워드 3~5개)
            
            ---
            뉴스 내용:
            {{2.title}}+{{2.description}}

### 📌 Module 8 - Notion Generate a completion ⭐ 핵심 모듈Create a Data Source Item  
- **역할:** 생성된 모든 콘텐츠를 Notion DB에 저장  
- **저장 필드 (11개):**  

    | Notion 속성 | 데이터 소스 | 타입 |
    |-------------|------------|------|
    | 제목 | rss.title | Title |
    | 요약 | blog.content | Text |
    | 키워드 | textparser.$1 | Text |
    | URL | rss.url | URL |
    | Date | rss.datecreated | Date |
    

------------

5. 에러처리 

------------
자동화 툴(Make.com)에서 에러 처리는 **"흐름이 끊기지 않게 하는 것"**과 **"문제가 생겼을 때 알림을 받는 것"**이 핵심입니다. 질문하신 워크플로우에서 에러 처리가 꼭 필요한 지점과 방법을 단계별로 짚어드릴게요.

1. 에러 처리가 가장 필요한 핵심 지점 (Top 3)
  - OpenAI (Generate a completion): 가장 에러가 잦은 구간입니다. (API 호출 한도 초과, 서버 타임아웃, 부적절한 콘텐츠 필터링 등)
  - Notion (Create a Database Item): 네트워크 오류나 데이터베이스 속성 불일치로 실패할 수 있습니다.
  - Text Parser (Match pattern): RSS에서 가져온 텍스트 형식이 바뀌어 정규표현식(Regex)이 매칭되지 않을 때 에러가 날 수 있습니다.








