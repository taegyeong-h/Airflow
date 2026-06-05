# PostgreSQL `BDP` DB 정보

스키마 이름은 소문자로 사용한다. *(대문자는 쿼리 사용시, 쌍따옴표를 붙여야하는 불편함을 최소화 하기 위함. PostgreSQL DBMS 특성.)*

## ODS (Operational Data Source) 스키마
- `ods` 스키마 테이블들은 원천데이터를 최대한 가공없이, 그대로 저장 보관한다.  
*( 외부 데이터를 그대로 옮긴 보관용이여서 "Staging Area"에 가깝지만, 임시 저장용은 아니라 <u>추후에도 계속 사용하기 위해 데이터 보관 관리</u>가 계속 진행되어야 하기에 'ods'명이 더 적절하다고 판단함. )*
- 테이블 네이밍 규칙 : `{원천 API 시스템명}`_`{API명 또는 데이터 유추 가능한 이름}`

### KRX(한국거래소) 데이터  

> [!Note]
> 전일자 데이터는 영업일 기준 익일 오전 8시부터 조회 가능
> - API 목록 : https://openapi.krx.co.kr/contents/OPP/INFO/service/OPPINFO004.cmd  
> - API 인증키 : `새로발급필요`  
> - API 인증키 유효기간 : 2026/03/26  
> - 모든 API의 사용기한 : 2026/01/20  
> - API 일일 이용 한도 : 10,000회/일  

 | 테이블명                   | API 설명                                    |
 | -------------------------- | ------------------------------------------- |
 | KRX_IDX_KRX_DD_TRD         | KRX_지수_KRX 시리즈 일별시세정보            |
 | KRX_IDX_KOSPI_DD_TRD       | KRX_지수_KOSPI 시리즈 일별시세정보          |
 | KRX_IDX_KOSDAQ_DD_TRD      | KRX_지수_KOSDAQ 시리즈 일별시세정보         |
 | KRX_IDX_BON_DD_TRD         | KRX_지수_채권지수 시세정보                  |
 | KRX_IDX_DRVPROD_DD_TRD     | KRX_지수_파생상품지수 시세정보              |
 | KRX_STO_STK_BYDD_TRD       | KRX_주식_유가증권 일별매매정보              |
 | KRX_STO_KSQ_BYDD_TRD       | KRX_주식_코스닥 일별매매정보                |
 | KRX_STO_KNX_BYDD_TRD       | KRX_주식_코넥스 일별매매정보                |
 | KRX_STO_SW_BYDD_TRD        | KRX_주식_신주인수권증권 일별매매정보        |
 | KRX_STO_SR_BYDD_TRD        | KRX_주식_신주인수권증서 일별매매정보        |
 | KRX_STO_STK_ISU_BASE_INFO  | KRX_주식_유가증권 종목기본정보              |
 | KRX_STO_KSQ_ISU_BASE_INFO  | KRX_주식_코스닥 종목기본정보                |
 | KRX_STO_KNX_ISU_BASE_INFO  | KRX_주식_코넥스 종목기본정보                |
 | KRX_ETP_ETF_BYDD_TRD       | KRX_증권상품_ETF 일별매매정보               |
 | KRX_ETP_ETN_BYDD_TRD       | KRX_증권상품_ETN 일별매매정보               |
 | KRX_ETP_ELW_BYDD_TRD       | KRX_증권상품_ELW 일별매매정보               |
 | KRX_BON_KTS_BYDD_TRD       | KRX_채권_국채전문유통시장 일별매매정보      |
 | KRX_BON_BND_BYDD_TRD       | KRX_채권_일반채권시장 일별매매정보          |
 | KRX_BON_SMB_BYDD_TRD       | KRX_채권_소액채권시장 일별매매정보          |
 | KRX_DRV_FUT_BYDD_TRD       | KRX_파생상품_선물 일별매매정보 (주식선물外) |
 | KRX_DRV_EQSFU_STK_BYDD_TRD | KRX_파생상품_주식선물(유가) 일별매매정보    |
 | KRX_DRV_EQKFU_KSQ_BYDD_TRD | KRX_파생상품_주식선물(코스닥) 일별매매정보  |
 | KRX_DRV_OPT_BYDD_TRD       | KRX_파생상품_옵션 일별매매정보 (주식옵션外) |
 | KRX_DRV_EQSOP_BYDD_TRD     | KRX_파생상품_주식옵션(유가) 일별매매정보    |
 | KRX_DRV_EQKOP_BYDD_TRD     | KRX_파생상품_주식옵션(코스닥) 일별매매정보  |
 | KRX_GEN_OIL_BYDD_TRD       | KRX_일반상품_석유시장 일별매매정보          |
 | KRX_GEN_GOLD_BYDD_TRD      | KRX_일반상품_금시장 일별매매정보            |
 | KRX_GEN_ETS_BYDD_TRD       | KRX_일반상품_배출권 시장 일별매매정보       |
 | KRX_ESG_SRI_BOND_INFO      | KRX_ESG_사회책임투자채권 정보               |


### 기타 OPEN 데이터
- 공공데이터 API : https://www.data.go.kr
- DART(전자공시) OPEN API : https://opendart.fss.or.kr
- 한국수출입은행 OPEN API : https://www.koreaexim.go.kr/ir/HPHKIR019M01
- Massive.com(미국 주가정보) OPEN API : https://massive.com/docs/rest/stocks/aggregates/daily-market-summary

 | 테이블명                      | 테이블 설명                |
 | ----------------------------- | -------------------------- |
 | KRX_SCRAPE_12025_업종분류현황 |                            |
 | DART_LIST                     | DART_공시검색              |
 | KR_EXIM_EXCHANGE              | 수출입_현재환율            |
 | MASSIVE_TICKER_TYPE           | Massive_티커 타입 정보     |
 | MASSIVE_TICKERS_INFO          | Massive_미국 종목 티커정보 |
 | MASSIVE_DAILY_MARKET          | Massive_미국 일별 시세정보 |
 <!-- | KRX_SCRAPE_12001_전종목시세   |                                      |
 | KRX_SCRAPE_12023_외국인보유량 |                                      |
 | K---------------------------T | 수----------------------------------리 |
 | binance_crypto_price_info     | 거래소 기준 전 종목 선물 가격 데이터 |
 | CORPCODE                      | DART_고유번호                        |
 | KR_DATA_HOLIDEINFO            | 공공_특일(국경일) 정보               |
 | KR_DATA_RESTDEINFO            | 공공_특일(공휴일) 정보               |
 | KR_DATA_ANNIVERSARYINFO       | 공공_특일(기념일) 정보               |
 | KR_DATA_DIVIINFO              | 공공_주식배당정보                    | -->


## DM (Data Mart) 스키마
`dm` 스키마 테이블들은 `ods` 를 이용하여 분석된 결과물을 저장한다.  

 <!-- |   종류   | 테이블명             | 테이블 설명             |
 | :------: | -------------------- | ----------------------- |
 | T------e | c------------------r | 보---------------------산 |
 | Function | fn_bucket_data       | 화면 조회용 테이블 함수 |
 | Function | fn_stock_screener    | 화면 조회용 테이블 함수 |
 | Function | fn_etf_etn_screener  | 화면 조회용 테이블 함수 | -->
