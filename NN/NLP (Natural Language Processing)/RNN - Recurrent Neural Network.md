# 📚 References 
- Tags :  [[NLP (Natural language processing)]] 
- Links:  [Презентация](https://github.com/Elbrus-DataScience/ds-phase-2/blob/master/slides/RNN.pdf)

# ❓ Questions
- В каких случаях возникает проблема взрыва градиента?
- Когда использовать активацию ReLU вместо tanh?  
*Никогда, не используется из-за градиента*
- Для чего есть смысл добавлять дополнительные RNN слои? 
*Более сложные закономерности*
- Объяснить функцию init_hidden() в обучающем цикле (Зачем нам что-то кроме hidden_dim на входе?)
*В торче не нужно, все автоматически делается*

# 🔗 Related material
-  [Word2vec в картинках](https://habr.com/ru/post/446530/)
- [Чудесный мир Word Embeddings: какие они бывают и зачем нужны?](https://habr.com/ru/company/ods/blog/329410/)
- [Vanilla Recurrent Neural Network](https://calvinfeng.gitbook.io/machine-learning-notebook/supervised-learning/recurrent-neural-network/recurrent_neural_networks)
- [Определение частей речи / POS (part of speech) tagging](https://becominghuman.ai/part-of-speech-tagging-tutorial-with-the-keras-deep-learning-library-d7f93fa05537)
- [Обнаружение именованых сущностей / NER (named entity recognition)](https://habr.com/ru/company/abbyy/blog/449514/)
- [Seq2seq подход / sequence to sequence](https://habr.com/ru/post/440472/)
- [LTSM networks](https://subscription.packtpub.com/book/big_data_and_business_intelligence/9781788399906/10/ch10lvl1sec62/implementation-of-the-language-model), [Схема для LTSM на самом деле немного другая](https://elbrus-ds-cheatsheets.streamlit.app/%F0%9F%82%93_rnn)
- [Взрыв градиента в RNN](https://gblobscdn.gitbook.com/assets%2F-LIA3amopGH9NC6Rf0mA%2F-M4bJ-IWAKzglR0XHFwU%2F-M4bJ2qhkeQ1-xH49LhY%2Frnn-gradient-flow.png?alt=media)



# РЕККУРЕНТНЫЕ НЕЙРОННЫЕ СЕТИ
## Структуры нейроннных сетей

![Structure](NN/NLP%20(Natural%20Language%20Processing)/imgs/1.png)

**One-to-one [[Neural Networks]]** это, например, CNN (сверточная н.н.), которой на вход дается 1 фото, а на выход она выдает класс.

**One-to-many NN** - Image captioning. На вход изображение, на выход модель говорит, что происходит на нем. (Кот, сидит, на столе...)

**Many-to-one NN** -  по описанию генерит фото, т.е. делает обратное. Или классификация текста (добрый/злой отзыв)

**Many-to-many** ([[Seq2Seq]]) - перевод текста. Втора схема это похожая архитектура - сеть соответствующе классифицирует каждое слово в неслучайной последовательности (прилагательное, сущ, глаг...)
## Схема работы RNN 

![Scheme](NN/NLP%20(Natural%20Language%20Processing)/imgs/2.png)

$h_{n}$ - hidden state. Hidden state - это история. Чем больше hidden size, тем больше сеть помнит о прошлых словах.
$f_{w}$  - это комбинация  $h_{n-1}$ и $x_{n}$, где w - это какие-то веса (веса везде одинаковые, находятся с помощью [[Back propagation]])
Таким образом, $h_{n+1}$ это результат комбинации $x_{n}$ c $h_{n-1}$.  Этим путем все h хранят память о предыдущих комбинациях. -> RNN основан на "запоминании информации".

<center>Пример: <center>

*Если NN дана цель находить негативный отзыв, то h будет хранить в векторе неинтерпретируемые абстратные признаки (аналогично [[Feature maps]] в CNN), которые позволят предсказать негативный ли отзыв.*

<mark style="background: #FF5582A6;">**Более сложая версия сети** 
</mark>

![More complicated](NN/NLP%20(Natural%20Language%20Processing)/imgs/3.png)
Надстройка выше вычисляет общий Loss, дергая промежуточные предсказания из сети и считая их потери.

<center>Примеры: <center>

1) NN предсказывает часть речи. На $h_{1}$ она сказала "прилагательное", на $h_{2}$ - "существительное", ибо вероятность встретить пару прилагательное-существительное выше. Но на деле $x_{2}$ оказалось еще одним прилагательным, $L_{2}$ - посчитанный лосс.

2) Посимвольная генерация слова 'Hello'

![Hello!](4.png)

<mark style="background: #FF5582A6;">**Еще подробнее**</mark>

![Elaborated](5.png)

- Линейный слой для закодированного слова (embedding'a) ищет закономерности между словами последовательности поочередно.

- Линейный слой для hidden state ищет зависимость между всеми словами, хранящися в истории RNN.

<mark style="background: #FF5582A6;">**Embedding слой**</mark>

![Embedding](6.png)

Pad это то же самое, что [[Padding]] в Convolutional Layer(Filter or Kernel) в CNN. Он нужен, чтобы у всех эмбедингов была одна размерность, так дорабатывают короткие эмбэдинги, длинные - обрезают.

<mark style="background: #FF5582A6;">**Общая схема**</mark>

![Overall Scheme](7.png)


- Реккурентный слой **в целом** делает лишь последнее предсказание, остальные выдергиваются промежуточно
- В случае последнего предсказания промежуточное и выдернутое предсказания равны.

## Проблемы RNN

1. Затухание / взрыв градиента
а. Затухает когда последовательность слишком длинная и градиент становится очень маленьким пока дойдет до первых слов.
б. ***Когда взрывается?***
2. Забывается контекст
