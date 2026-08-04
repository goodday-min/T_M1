# 뉴스 요약 자동화 : Notion 데이터베이스   #  

------------  
## ✅ Module 8 - Notion / Create a Data Source Item 
------------    

 
- ### 역할: 생성된 모든 콘텐츠를 Notion DB에 저장  
- ### 저장 필드 (6개):  

    | Notion 속성 | 데이터 소스 | 타입 | 설명 |  
    |-------------|------------|------| --- |  
    | 제목 | rss.title | Title | 뉴스 제목 |  
    | 요약 | openai.result | Text | OpenAI 가 요약한 내용 |  
    | 키워드 | textparser.$1 | Text | OpenAI 가 요약한 키워드  |  
    | URL | rss.url | URL | 뉴스 원본 URL |  
    | 날짜 | rss.datecreated | Date | 뉴스 생성 날짜 |  
    | GUID | rss.guid | Text |  중복 방지 키 |  


  - #### 중복 방지 키 설정 : GUID (Globally Unique Identifier)  
  
    #### 🔎 중복 방지 키 선택 이유

        RSS GUID는 발행사가 직접 부여한 기사 고유 ID  
        → URL 파라미터가 바뀌어도 GUID는 그대로 유지  
        → 중복 감지 안정적  

        URL은 파라미터 변경으로 동일 기사도 다른 값이 될 수 있지만,
        GUID는 RSS 표준 스펙으로 발행사가 직접 부여한 불변 식별자이기 때문에 중복 감지 키로 더 신뢰성이 높습니다

    ✅ GUID 와 URL 해시 비교
      
    | 항목 | GUID | URL 해시 |  
    | --- | --- | --- |
    | 출처 | RSS 피드가 직접 제공 | 우리가 URL을 가공 |
    | 신뢰성 | 발행사가 보장 | URL 변경 시 해시도 변경 |
    | 구현 복잡도 | 바로 사용 가능 | 해시 변환 로직 필요 |
    | 표준 여부 | RSS 2.0 공식 스펙 | 비표준 (자체 처리) |
    | 안정성 | 기사 수정돼도 유지 | URL 파라미터 변경 시 깨짐 |


- ### Notion 데이터베이스 전체 화면
  
| Notion 실행 화면 | Notion 에서 AI가 요약한 텍스트가 포함된 뉴스 컨텐츠가 저장된 화면 |
| --- | --- |
| <img width="427" height="528" alt="image" src="https://github.com/user-attachments/assets/995c86a4-2462-468e-a1a1-3862070a4d71" /> | <img width="1430" height="647" alt="image" src="https://github.com/user-attachments/assets/3c7e067c-c77e-4492-813c-e6a025fa2d74" /> |
    


