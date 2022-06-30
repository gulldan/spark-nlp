---
layout: model
title: Arabic Named Entity Recognition (from boda)
author: John Snow Labs
name: bert_ner_ANER
date: 2022-05-04
tags: [bert, ner, token_classification, ar, open_source]
task: Named Entity Recognition
language: ar
edition: Spark NLP 3.4.2
spark_version: 3.0
supported: true
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

Pretrained Named Entity Recognition model, uploaded to Hugging Face, adapted and imported into Spark NLP. `ANER` is a Arabic model orginally trained by `boda`.

## Predicted Entities

` حكومة  `, ` شخص ديني  `, ` رياضي  `, ` ترفيه  `, ` كتاب  `, ` شعب(أمة)  `, ` مطار  `, ` مؤسسة دينية  `, ` مركز سكني  `, ` فنان  `, ` غير حكومي  `, ` أراضي البناء  `, ` سماوي  `, ` أرض طبيعية  `, ` منشأة منطقة فرعية  `, ` هواء  `, ` مدينة أو ضاحية  `, ` عالم  `, ` محامي  `, ` سوفتوير(برمجيات)  `, ` أرض  `, ` منفجر  `, ` كيميائي  `, ` رياضة  `, ` رماية  `, ` طريق  `, ` ماء  `, ` تجاري  `, `   `, ` سياسي  `, ` صوت  `, ` علوم طبية  `, ` نووي  `, ` فظ  `, ` فيلم  `, ` قارة  `, ` ولاية أو مقاطعة  `, ` شخص  `, ` حاد  `, ` مهندس  `, ` مسطح مائي  `, ` عتاد  `, ` طعام  `, ` قذيفة  `, ` دواء  `, ` تعليمي  `, ` نبات  `, ` شرطة  `, ` رجل أعمال  `, ` إعلام  `, ` مجموعة  `

{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/bert_ner_ANER_ar_3.4.2_3.0_1651630311382.zip){:.button.button-orange.button-orange-trans.arr.button-icon}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python
documentAssembler = DocumentAssembler() \
    .setInputCol("text") \
    .setOutputCol("document")

sentenceDetector = SentenceDetectorDLModel.pretrained("sentence_detector_dl", "xx")\
       .setInputCols(["document"])\
       .setOutputCol("sentence")

tokenizer = Tokenizer() \
    .setInputCols("sentence") \
    .setOutputCol("token")

tokenClassifier = BertForTokenClassification.pretrained("bert_ner_ANER","ar") \
    .setInputCols(["sentence", "token"]) \
    .setOutputCol("ner")

pipeline = Pipeline(stages=[documentAssembler, sentenceDetector, tokenizer, tokenClassifier])

data = spark.createDataFrame([["أنا أحب الشرارة NLP"]]).toDF("text")

result = pipeline.fit(data).transform(data)
```
```scala
val documentAssembler = new DocumentAssembler() 
      .setInputCol("text") 
      .setOutputCol("document")

val sentenceDetector = SentenceDetectorDLModel.pretrained("sentence_detector_dl", "xx")
       .setInputCols(Array("document"))
       .setOutputCol("sentence")

val tokenizer = new Tokenizer() 
    .setInputCols(Array("sentence"))
    .setOutputCol("token")

val tokenClassifier = BertForTokenClassification.pretrained("bert_ner_ANER","ar") 
    .setInputCols(Array("sentence", "token")) 
    .setOutputCol("ner")

val pipeline = new Pipeline().setStages(Array(documentAssembler,sentenceDetector, tokenizer, tokenClassifier))

val data = Seq("أنا أحب الشرارة NLP").toDF("text")

val result = pipeline.fit(data).transform(data)
```
</div>

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|bert_ner_ANER|
|Compatibility:|Spark NLP 3.4.2+|
|License:|Open Source|
|Edition:|Official|
|Input Labels:|[document, token]|
|Output Labels:|[ner]|
|Language:|ar|
|Size:|506.0 MB|
|Case sensitive:|true|
|Max sentence length:|128|

## References

- https://huggingface.co/boda/ANER
- https://drive.google.com/file/d/1cNnKf-jS-3sjBXF2b0rkh517z9EzFFT4/view?usp=sharing
- https://fsalotaibi.kau.edu.sa/Pages-Arabic-NE-Corpora.aspx
- https://github.com/aub-mind/arabert
- https://fsalotaibi.kau.edu.sa/Pages-Arabic-NE-Corpora.aspx
- https://github.com/BodaSadalla98