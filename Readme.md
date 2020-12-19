# 앙상블 감성분석 모델

##### 본 감성분석 모델은 고려대학교 디지털금융공학과 DFE610 디지털금융공학을 위한 자연어처리기술 수업의 과제를 수행하기 위해 개발한 모델이다.<br/>

본 감성분석 모델은 한국어 영화 리뷰, 영어 대화 데이터를 기반으로 최신의 딥러닝(Deep Learning) 모델을 학습 시킨 후 각 모델의 결과를 앙상블(Ensemble) 하였을 때, 개별 모델 보다 예측 데이터의 성능이 개선될 수 있는지에 대한 연구 자료이다.

**■ 1. 한국어 앙상블 감성분석 모델**

##### **한국어 감성분석 모델은 앙상블 감정분석 대상 모델로 본 과정 수업 실습자료인 'Transformer를 이용한 감정분석 모델', 'CNN을 이용한 감정분석 모델' 과 '네이버 영화리뷰 감정분석 with Hugging Face BERT' 모델을 실습자료로 제공된 소스와 오픈소스를 참고하여 구성하였다.** <br/>

### 참고자료 및 소스 출처

##### 모델의 오픈소스 참고 출처

1. **Transformer를 이용한 감정분석 모델** : https://github.com/Parkchanjun/KU-NLP-2020-1/Transformer를 이용한 감정분석_한국어.jpynb 

2. **CNN을 이용한 감정분석 모델** : https://github.com/Parkchanjun/KU-NLP-2020-1/CNN_Sentiment_Analysis.jpynb

3. **BERT를 이용한 감성분석 모델 : 네이버 영화리뷰 감정분석 with Hugging Face BERT**,  https://colab.research.google.com/drive/13AMh8N9tEIw5rmxgc1fQfS8581mWegxj

#### 앙상블 모델의 구성

**본 앙상블 모델은 첨부 소스코드의 순차적 실행을 통해 예측 결과를 반환한다.**

**본 앙상블 모델은 아래 3가지 모델의 예측결과를 하드보팅(Hard Voting)한 결과를 최종 모델의 아웃풋으로 산출하며, 최종 모델의 최종 예측 결과는 ensamble_submission 인스턴스에 저장되며,  'ensamble prediction.csv'로 저장할 수 있다.**

1. **개별 모델**
   - Transformer을 이용한 감정분석 모델 , CNN을 이용한 감정분석 모델, BERT(bert-base-multilingual-cased)

2. **데이터 셋**

   - 학습, 테스트 데이터 : [Web] https://github.com/e9t/nsmc.git

   - Kaggle Competition 테스트 데이터 : [API] korean-sa-competition-dfe610

3. **전처리**
- Transformer, CNN : 감정분석 대상 문장을 Konlpy의 Okt를 이용하여 형태소 분석 결과를 토크나이저로 입력
  
- BERT 감정분석 모델 : BERT 토크나이져에서 감정분석 대상 문장 토큰처리
  
4. **모델 학습**

   - 모델 학습은 반드시 순차적으로 실행해야 한다. (비고 : 1 모델 학습 → 1 모델 예측결과 저장)

   - 모델 학습은 NSMC 학습 데이터를 활용한다.

5. **개별 모델 예측 결과 저장**

   - 모델 학습 후 각 모델의 테스트 데이터에 대한 예측 결과를 순차적으로 각 모델의 x_predict 인스턴스에 저장 될 수 있도록 실행해야 한다.
- Transformer를 이용한 감정분석 모델, BERT 감정분석 모델은 모델의 예측 결과를 Argmax한 결과를 Predict 인스턴스에 저장한다.
   - CNN을 이용한 감정분석 모델은 모델의 예측 결과가 > 0.5 면 1, 이외의 경우 0으로 Predict 인스턴스에 저장한다.
- 모든 개별 모델의 예측 결과를 csv 파일로 저장 할 수 있다.
   - Sentiment_analysis_Korean_KSB_origianal.jpynb는 학습데이터의 테스트 데이터로 성능을 평가한다.
- Sentiment_analysis_Korean_KSB_kaggle.jpynb는 Kaggle korean-sa-competition 테스트 데이터를 통해 앙상블 감성분석 예측 결과를 생성한다.
  
6. **개별 모델 예측 결과 생성 및 하드보팅 실행**

   - 개별 모델의 예측 결과를 Hard Voting 하여 최종 앙상블 모델의 예측 결과를 산출한다.

   - Hard Voting은 개별모델의 예측 결과를 SUM하여 >=2인 경우 예측결과를 1로, 이외 경우 0으로 최종 아웃풋을 산출한다.

7. **앙상블 모델 아웃풋과 CSV 파일 저장**

   - 앙상블 모델의 최종 예측 결과는 ensamble_submission 인스턴스에 저장된다.

   - 예측 결과는 ensamble prediction.csv로 저장할 수 있다.

8. 실행환경

   - 본 소스는 구글 Colab에서 작성됨 
- 본 소스의 실행을 위해서는 Colab Pro 환경이 필요(GPU 메모리 필요)
   - ① 실행 후 ② 순차 실행 → 종료 후 ③ 실행 (실행순번 표기)
   - BERT 모델 저장 후 업로드 시에도 메모리 문제 발생 가능함(재실행 권장)



**■ 2. 영어 앙상블 감성분석 모델**

**영어 감정분석 모델은ELECTRA 모델과 '네이버 영화리뷰 감정분석 with Hugging Face BERT' 모델을 오픈소스를 참고하여 구성하였다.**

### 참고자료 및 소스 출처

##### 모델의 오픈소스 참고 출처

1. ELECTRA를 이용한 감정분석 모델 : https://github.com/jiwonny/nlp_emotion_classification 

2. BERT를 이용한 감성분석 모델 : 네이버 영화리뷰 감정분석 with Hugging Face BERT, https://colab.research.google.com/drive/13AMh8N9tEIw5rmxgc1fQfS8581mWegxj


#### 앙상블 모델의 구성

본 모델은 ELECTRA, BERT의 아웃풋을 Soft Voting하여 최종 아웃풋을 산출한다.

**본 앙상블 모델은 아래 2가지 모델의 예측결과를 소프트 보팅(Soft Voting)한 결과를 최종 모델의 아웃풋으로 산출하며, 최종 모델의 최종 예측 결과는 ensemble_out 인스턴스에 저장되며,  'ensemble_submission.csv'로 저장할 수 있다.**

1. **개별 모델**
   - ELECTRA(electra-large-generator) , BERT (bert-base-multilingual-cased)

2. **데이터 셋**

   - 학습, 테스트 데이터 : [Web] http://doraemon.iis.sinica.edu.tw/emotionlines/

   - Kaggle Competition 테스트 데이터 : [API] english-sa-competition-dfe610

3. **전처리**

- Nltk 라이브러리를 통해 stopword 등 불용어 제거 후 [CLS], [SEP]로 분리하여 ELECTRA, Bert 토크나이져로 입력


4. **모델 학습**
   - 모델 학습은 순차적으로 실행해야 한다. (비고 : 1 모델 학습 → 1 모델 예측결과 저장)

   - 모델 학습은 데이터 셋 출처의 미국 영화 드라마 Friends 학습 데이터를 활용한다.

5. **개별 모델 예측 결과 저장**

   - 모델 학습 후 각 모델의 테스트 데이터에 대한 예측 결과를 순차적으로 각 모델의 x_predict, x_predict_score 인스턴스에 저장 될 수 있도록 실행해야 한다.
   - 테스트는 Kaggle korean-sa-competition 테스트 데이터를 활용한다.(변경 가능)
   - 모든 개별 모델의 예측 결과를 csv 파일로 저장 할 수 있다.
   - Sentiment_analysis_English_KSB_origianal.jpynb는 학습데이터의 테스트 데이터로 성능을 평가한다.
   - Sentiment_analysis_English_KSB_kaggle.jpynb는 Kaggle english-sa-competition 테스트 데이터를 통해 앙상블 감성분석 예측 결과를 생성한다.

6. **개별 모델 예측 결과 생성 및 하드보팅 실행**

   - 개별 모델의 예측 결과를 Soft Voting 하여 최종 앙상블 모델의 예측 결과를 산출한다.
   - Soft Voting은 개별모델의 예측 결과를 합산하고, 합산한 결과를 모델 수로 나눈 평균 데이터를 인덱스 별로 Argmax하여 앙상블 감성분석 예측 결과로 생성한다.

7. **앙상블 모델 아웃풋과 CSV 파일 저장**

   - 앙상블 모델의 최종 예측 결과는 ensemble_out 인스턴스에 저장된다.

   - 예측 결과는 ensemble_submission.csv로 저장할 수 있다.

8. 실행환경

   - 본 소스는 구글 Colab에서 작성됨 
   - 본 소스의 실행을 위해서는 Colab Pro 환경이 필요(GPU 메모리 필요)
   - ① 실행 후 ② 순차 실행 → 종료 후 ③ 실행 (실행순번 표기)
   - BERT 모델 저장 후 업로드 시에도 메모리 문제 발생 가능함(재실행 권장)

  @ ELECTRA를 이용한 감정분석 모델 : https://github.com/jiwonny/nlp_emotion_classification



  @ 네이버 영화리뷰 감정분석 with Hugging Face BERT : https://colab.research.google.com/drive/13AMh8N9tEIw5rmxgc1fQfS8581mWegxj



***☞ Kaggle 리더보드 업로드 시 index 칼럼명을 'Id'로 입력하여 저장 후 제출함\****



