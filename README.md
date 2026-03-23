# jeju-place-recommendation

<p align="center">
  <img src="image/main.png" width="800" alt="Overview" />
</p>

제주 지역 음식점 데이터를 바탕으로, 사용자 질문 맥락에 맞는 추천 결과와 추천 이유를 제공하는 LLM-RAG 기반의 '생성형 AI 활용 맛집 추천 서비스' 프로젝트입니다.

## Overview
 
인기 장소만 반복 추천하는 방식의 한계를 줄이기 위해, 장소를 HOT / COOL / COLD 플레이스로 구분하고 사용자 질문에 맞는 추천 응답을 생성하도록 구성했습니다.

이 레포는 다음 작업을 중심으로 정리되어 있습니다.

- HOT / COOL / COLD 플레이스 기준 정의
- 제주 지역 장소 데이터 전처리
- BM25 기반 키워드 추출 및 임베딩 생성
- FAISS 기반 검색 구조 구성
- LLM 프롬프트 엔지니어링
- Streamlit 기반 웹 프로토타입 구현

## What this repository covers

- 제주 지역 장소 추천 서비스 기획
- 장소 데이터 구조화 및 전처리
- BM25 · FAISS 기반 RAG 파이프라인
- 사용자 질문 맥락 반영 응답 설계
- 추천 이유를 포함한 설명형 응답 구현

## Service flow

jeju-place-recommendation은 다음 흐름으로 동작합니다.

A. 사용자가 자연어로 장소 추천 질문 입력  
B. 질문과 관련된 조건 및 맥락 반영  
C. 전처리된 장소 데이터에서 관련 정보 검색  
D. 검색 결과를 바탕으로 추천 결과와 이유를 포함한 응답 생성  
E. 웹 인터페이스에서 결과 출력  

## Place definition

이 프로젝트에서는 제주 지역 장소를 다음 기준으로 구분했습니다.

- **HOT Place**: 이미 인기가 높고 많이 알려진 장소
- **COOL Place**: 상대적으로 덜 알려졌지만 추천 가치가 있는 장소
- **COLD Place**: 현재 추천 우선순위가 낮은 장소

이 구분을 바탕으로,  
단순 인기순 추천이 아니라 사용자 상황에 맞는 추천 결과를 제시하도록 구성했습니다.

## Data preprocessing

데이터는 추천에 바로 사용할 수 있도록 전처리 과정을 거쳐 정리했습니다.

주요 작업은 다음과 같습니다.

- 공모전 제공 제주 지역 데이터 정리
- 장소 관련 텍스트 전처리
- 카테고리 및 속성 정보 정리
- 추천에 필요한 컬럼 및 기준 재구성
- HOT / COOL / COLD 플레이스 기준 반영

## RAG pipeline

이 프로젝트의 추천 구조는 RAG 기반으로 구성했습니다.

주요 구성은 다음과 같습니다.

- **BM25**: 장소 데이터에서 검색에 필요한 핵심 키워드 추출
- **Embedding**: 검색 가능한 벡터 형태로 변환
- **FAISS**: 질문과 관련된 장소 정보를 빠르게 검색
- **LLM**: 검색 결과를 바탕으로 최종 추천 응답 생성

## Prompt Engineering

검색 결과를 그대로 출력하지 않고,  
추천 결과와 추천 이유가 함께 나타나도록 프롬프트를 조정했습니다.

프롬프트 설계에서 반영한 요소는 다음과 같습니다.

- 지역, 음식 종류, 분위기 등 질문 조건 반영
- 검색된 장소 정보를 기반으로 추천 결과 생성
- 추천 이유가 포함되도록 응답 형식 조정
- HOT / COOL / COLD 플레이스 구분 반영

이를 통해 장소 목록 나열보다,  
질문 조건에 맞는 설명형 추천 응답을 생성하도록 구성했습니다.

## Data and model

- 데이터: 공모전 제공 제주 지역 장소 데이터
- 전처리: 장소 텍스트 및 속성 정보 정리
- 검색 방식: BM25 + Embedding + FAISS
- 응답 방식: LLM 기반 생성
- 인터페이스: Streamlit 기반 웹 프로토타입

## Setup

### 1. Environment Configuration

Python 3.8 이상 환경을 권장합니다.

```bash
pip install -r requirements.txt
```

### 2. Prepare Data

이 프로젝트에 사용한 데이터는 공모전 주최 측에서 제공한 비공개 데이터입니다.  
본 레포에는 포함되어 있지 않으며, 별도로 준비해야 합니다.

데이터는 `./data` 경로에 위치시킨 뒤 사용합니다.

### 3. Run the Code

#### (1) 임베딩 생성 및 저장

```bash
python embeddings.py
```

#### (2) 데이터 전처리

```bash
python chunking.py
python sentences.py
```

#### (3) 웹 애플리케이션 실행

```bash
streamlit run alphastorm_app.py
```

## Repository structure

- `embeddings.py`  
  임베딩 생성 및 저장

- `chunking.py`  
  데이터 chunk 단위 전처리

- `sentences.py`  
  문장 단위 데이터 정리

- `alphastorm_app.py`  
  Streamlit 기반 웹 애플리케이션 실행 파일

- `data/`  
  장소 데이터 저장 경로

## My role

이 프로젝트에서 수행한 작업은 다음과 같습니다.

- 제주 장소 추천 문제 정의
- HOT / COOL / COLD 플레이스 기준 설계
- 데이터 전처리 및 추천 기준 정리
- BM25 · FAISS 기반 검색 구조 구성
- 프롬프트 엔지니어링을 통한 응답 보정
- Streamlit 기반 프로토타입 구현

## Result

이 프로젝트를 통해 다음 결과를 정리했습니다.

- HOT / COOL 플레이스 추천 기준 기반 서비스 프로토타입 구현
- 사용자 맥락을 반영한 추천 응답 구조 설계
- 추천 이유를 포함한 설명형 응답 구현

## Award

이 프로젝트는 2024 Bigcontest 생성형 AI 분야 수상 프로젝트를 바탕으로 정리한 저장소입니다.
