# 생성형 AI 기반 제주 맛집 추천 서비스

<p align="center">
  <img src="image/main.png" width="720" />
</p>

제주 지역 장소 데이터를 바탕으로, 사용자 질문에 맞는 **추천 결과와 추천 이유**를 생성하는 **LLM-RAG 기반 맛집 추천 서비스**입니다.

인기 장소를 반복 추천하는 방식에서 벗어나,  
**연령대·시간대·현지인 비율**을 반영해 추천 기준을 다시 설계했습니다.

## Overview

이 프로젝트는 다음 요소를 중심으로 구성했습니다.

- **HOT / COOL / COLD** 플레이스 기준 정의
- 제주 지역 장소 데이터 정리
- **BM25 + Embedding + FAISS** 기반 검색 구조 구성
- **Streamlit** 기반 웹 프로토타입 구현

자세한 설명은 [`docs/PROJECT.md`](docs/PROJECT.md)에서 확인할 수 있습니다.

## Service Flow

1. 사용자 질문 입력  
2. 질문 조건과 맥락 반영  
3. 관련 장소 정보 검색  
4. 추천 결과와 이유 생성  
5. 웹 인터페이스에서 출력  

## Place Definition

<p align="center">
  <img src="image/place.png" width="720" />
</p>

- **HOT Place**: 이미 많이 알려진 인기 장소
- **COOL Place**: 덜 알려졌지만 추천 가치가 있는 장소
- **COLD Place**: 현재 추천 우선순위가 낮은 장소

질문 조건에 따라 서로 다른 성격의 장소를 제시할 수 있도록 이 기준을 활용했습니다.

## RAG pipeline

추천 구조는 RAG 기반으로 구성했으며 주요 요소는 다음과 같습니다.

- **BM25**: 장소 데이터에서 검색에 필요한 핵심 키워드 추출
- **Embedding**: 검색 가능한 벡터 형태로 변환
- **FAISS**: 질문과 관련된 장소 정보를 빠르게 검색
- **LLM**: 검색 결과를 바탕으로 최종 추천 응답 생성

즉, 키워드 기반 검색과 벡터 검색을 함께 사용하고,  
검색 결과를 바탕으로 LLM이 최종 추천 문장을 생성하는 흐름입니다.

## Setup

### 1. Environment Configuration

Python 3.8 이상 환경을 권장합니다.

```bash
pip install -r requirements.txt
```

### 2. Prepare Data

이 프로젝트에 사용한 데이터는 공모전 주최 측에서 제공한 비공개 데이터입니다.  

### 3. Run the Code

#### (1) 임베딩 생성 및 저장

```bash
python run/embeddings.py
```

#### (2) 데이터 전처리

```bash
python run/chunking.py
python run/sentences.py
```

#### (3) 웹 애플리케이션 실행

```bash
streamlit run run/alphastorm_app.py
```

## Repository structure

```bash
.
├── docs/
│   └── PROJECT.md
├── image/
│   ├── main.png
│   └── place.png
├── run/
│   ├── alphastorm_app.py
│   ├── sentences.py
│   ├── chunking.py
│   └── embeddings.py
```

### Folder guide

#### `docs/`
프로젝트 설명 문서를 정리한 폴더입니다.

- `PROJECT.md`  
  프로젝트 목적, 구조, 주요 작업 정리

#### `image/`
프로젝트 관련 이미지를 저장하는 폴더입니다.

- `main.png`  
  메인 화면 이미지
- `place.png`  
  HOT / COOL / COLD 플레이스 구분 이미지

#### `run/`
실행 코드와 전처리 스크립트를 모아둔 폴더입니다.

- `embeddings.py`  
  임베딩 생성 및 저장
- `chunking.py`  
  데이터 chunk 단위 전처리
- `sentences.py`  
  문장 단위 데이터 정리
- `alphastorm_app.py`  
  Streamlit 기반 웹 애플리케이션 실행 파일

## Award

이 프로젝트는 2024 Bigcontest 생성형 AI 분야 수상 프로젝트를 바탕으로 정리한 저장소입니다.
