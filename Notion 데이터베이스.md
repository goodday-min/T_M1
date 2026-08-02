

✅ Module 8 - Notion / Create a Data Source Item  
- 역할: 생성된 모든 콘텐츠를 Notion DB에 저장  
- 저장 필드 (6개):  

    | Notion 속성 | 데이터 소스 | 타입 | 설명 |  
    |-------------|------------|------| --- |  
    | 제목 | rss.title | Title | 뉴스 제목 |  
    | 요약 | openai.result | Text | OpenAI 가 요약한 내용 |  
    | 키워드 | textparser.$1 | Text | OpenAI 가 요약한 키워드  |  
    | URL | rss.url | URL | 뉴스 원본 URL |  
    | 날짜 | rss.datecreated | Date | 뉴스 생성 날짜 |  
    | GUID | rss.guid | text |  중복 방지 키 |  

      중복 방지 키 설정 및 선정 이유 : GUID (Globally Unique Identifier)  
      뉴스 자동화 프로그램의 경우 단순 고유 ID 부여를 통해 각 콘텐츠 식별용으로 사용하기 위해 GUID를 사용하였음.  

- Notion 실행 화면(로그) : Make에서 notion 모듈에 데이터가 실행되는 화면  
<img width="427" height="528" alt="image" src="https://github.com/user-attachments/assets/995c86a4-2462-468e-a1a1-3862070a4d71" />


- Notion 데이터베이스 화면   
<img width="1112" height="414" alt="image" src="https://github.com/user-attachments/assets/3d7cbfb2-1cb1-4ead-a319-7ccc2d8dfcd1" />  

- Notion 에서 AI가 요약한 텍스트가 포함된 뉴스 컨텐츠가 저장된 화면  
<img width="474" height="673" alt="image" src="https://github.com/user-attachments/assets/7d5a4733-3abb-4413-b03f-3173b48676fc" />

- Notion 데이터베이스 전체 화면  
<img width="1430" height="647" alt="image" src="https://github.com/user-attachments/assets/3c7e067c-c77e-4492-813c-e6a025fa2d74" />

