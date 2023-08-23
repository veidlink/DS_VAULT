# 📚 References 
- Tags : [[RNN - Recurrent Neural Network]] [[CV]] #NLP
- Links:  [Deep Learning School](https://youtu.be/G4vT5cvJSxY)

# ❓ Questions
- В лекции про Align Attention?

# 🔗 Related material

# Seq2Seq - машинный перевод

#### <mark style="background: #FF5582A6;">Идея Attention</mark> 
![a](22.png)

При переводе человек несколько раз смотрит на изначальное предложение, потому что забывает. Также забывает RNN (BiLSTM отчасти лучше). Поэтому создали Attention.  Архитектура принимает каждое слово и смотрит насколько декодеру оно важно для перевода следующего слова.
- $< eos >$ - end of sequence
-  $< bos >$ - beginning of sequence
Ванильным - энкодер, синим - декодер.
#### <mark style="background: #FF5582A6;">Подробнее о структуре</mark> 

![b](23.png)
- $h_{et}$ -hidden state энкодера
- $h_{dt}$ - hidden state декодера
Оба идут на вход Attention function, на выходах применятся softmax, получаем вероятности - насколько важно это слово для перевода первого (на данном фото, а так следующего).
![c](24.png)
Получаем вектор контекста $c$, отправляем его с токеном $< bos >$ (чтобы декодер предсказал первое слово таргета) в декодер вместе с hidden state.

В этом черном кружке может быть много видов механизмов attention.
![d](26.png)
Content-base attention использует косинус чтобы оценить схожесть векторов. Dot-product использует скалярное произведение чтобы оценить схожесть векторов. По сути одно и то же, но другая запись.

Структура encoder-decoder с исп. attention выглядит иначе. Теперь каждый выход имеет context вектор из себя и всех предыдущих hidden states.
![e](27.png)