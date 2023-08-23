# 📚 References 
- Tags : [[RNN - Recurrent Neural Network]] [[Word2Vec]]  [[NLP (Natural language processing)]]
- Links: [Презентация](https://github.com/Elbrus-DataScience/ds-phase-2/blob/master/slides/LSTM.pdf)

# ❓ Questions
- 

# 🔗 Related material
- [Habr](https://habr.com/ru/companies/wunderfund/articles/331310/)
- [Biderectional LSTM](https://paperswithcode.com/method/bilstm)
# LSTM (Long-short-term memory)

Как ясно из названия, эта архитектура решает проблему забывания контекста. Это достигается добавлением потока $C$ (cell state) к $h$, которое забывает что было в самом начале.
![a](15.png)
![b](16.png)

Для сравнения структура обычной RNN и LSTM.
Поэтапно разберу LSTM.
### <center> $f_{t}$ <center>

Т.н. forget gate. Сигмоида выдает 0/1. 0 значит забыть, 1 - запомнить. Идет в  Cell state.
![ft](17.png)
### <center>$i_{t}$, $C_{t}$<center>

Еще два полносвязных слоя, ищущие какие-то закономерности и добавляющие сложность модели.

![itct](18.png)
### <center>Cell state<center>

1. Результат Forget gate по-элементно умножается на Cell state. -> Нужное забыть забывается, нужное запомнить запоминается.
2. Cell state + $i_{t} * C_{t}$

<mark style="background: #FF5582A6;">Контекст в LSTM не забывается благодаря тому, что на потоке Cell state нет ни одной функции активации -> производные не падают в ужасающих темпах.
</mark>
![cell state](19.png)
### <center>$h_{t}$ на выходы<center>

Новый fc-слой анализирует, что происходит на текущий момент. Активированный тангенсом Cell state хранит память о старом.
-> Анализируем новое, учитывая старое, отправляем дальше.

![ht](20.png)

### Общая схема LSTM
![scheme](21.png)