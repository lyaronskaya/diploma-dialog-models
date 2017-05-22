# Эксперименты

## Модели

Дискриминатор:

1. LSTM + Attention
2. Input: (batch_size, 2 * emb_size, question_len, answer_len) -> BatchNorm + Conv(3, 3) + MaxPool(2, 2) + Conv(3, 3) + MaxPool(2, 2) 

3. 1 + InfoApproximation (не обучается к сожалению, потому что очень много параметров)
4. 2 + InfoApproximation

## Обучение дискриминатора

Adversarial Success на выборке из 3200 предложений (ROC-AUC)

| Model | AdvSucc |
|-------|---------|
|1.     | 0.699   | долго обучается 
|2.     | 0.977   |
|4.     | 0.989   |


## Дообучение генератора

|  Model  | Perplexity |
|---------|------------|
|Baseline | ~7         |
|1.       | ~7         |
|2.       | ~13        |
|4.       | ~7         |


В 2. перплексия очень большая, но ответы адекватные и в [Generative Deep Neural Networks for Dialogue](https://arxiv.org/abs/1611.06216) подтверждают, что это типичная ситуация с перплексией.

## Evaluation

Примеры ответов дискриминатора 1 на сгенерированные ответы:

Вектор внимания

<img src='https://s9.postimg.org/n8ogtuwq7/2017-05-22_19.01.03.png' 
alt='attention visualization' 
title='attention' width=700  />


|  Reward  | Phrase 
|----------|-------
| 0.646619 | my name is dr . biber .
| 0.386294 | bye - bye , precious . 
| 0.280729 | my children , mr . jefferson says you already made a sex doll the school nurse gollum has _UNK_ it
| 0.535254 | trent boyett !
| 0.325994 | very well .


Рандомные контексты и сгенерированные ответы:

## Эксперименты с information maximization

<img src='https://s22.postimg.org/qkggvwsoh/2017-05-22_18.33.18.png' 
alt='InfoGAN losses' 
title='InfoGAN losses' width=600 />

## Количество правильных ответов на вопрос "What is your name ?"

1.
| Угаданные имена | Ответ 
|-----------------|-------
|'president'      | "it ' s the president of wall - mart . at south park elementary . the second was a hit"|
|'scott'          | "my name . . . called scott , but my dad isn ' t even legal anymore ?"|

2.
(Плохо)

|Угаданные имена| Ответ
|---------------|-------
|'m'            | "ooo stan marsh . a what are his name kyle gints ? i ' m sure as soon as filmore"
|'man'          | 'hi fellas . i wanna go home . y - you gotta come meet the white man . get your' 
|'timmy'        | 'boooo ! ! show us what senator spears ? ! fudge said , timmy timmy timmy russell fan flying disciprine'
|'kenny'        | '# and daddy my fat ugly little woman ! whoa whoa whoa whoa , whoa h . . . kenny'
|'pip'          | "eugh . uhuh , i ' m pip kids from my future ' s voice box salesman , travis harrisons"

4.
|Угаданные имена | Ответ                                                                               | Прим.
|----------------|-------------------------------------------------------------------------------------|------
|'m'             | "my name is _UNK_ , and i ' m harry potter . i ' m the little boy . but"            | -
|'kyle'          | 'kyle .'                                                                            | Ок
|'snooki'        | 'snooki .'                                                                          | Ок
|'kenny'         |'( a question as am , and is perhaps mr . havisham , but , his holiness , eric kenny'| -

 
