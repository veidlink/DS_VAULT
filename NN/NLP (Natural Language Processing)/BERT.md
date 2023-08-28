## 📚 References 
- Tags :  [[Transformers]]
- Links: 

## ❓ Questions
- 

## 🔗 Related material

# Bidirectional Encoder Representation from Transformers
Это энкодер из трансформера. В задачах ниже работает так:
![a](imgs/39.png)
### Где применяется
1. SQuAD - найти в определенном контексте ответ на заданный вопрос
2. NER - распознование именнованных сущностей. ![NER](https://www.shaip.com/wp-content/uploads/2022/02/Blog_Named-Entity-Recognition-%E2%80%93-The-Concept-Types-Applications.jpg)
3. Multi NLI (Natural Language Inference) - могут ли рядом друг с другом стоять два предложения по смыслу. Еще ответит на такой вопрос: 
 
 *<center> 'Этот текст о квантовых компьютерах?' <center> Квантовый компьютер (в отличие от обычного) оперирует не битами, а кубитами".*

4. Классификация текста и т.д

### Как обучается Bert
- **Mask Language Modeling**. 80% времени учится предсказывать следующий элемент в последовательности (Я кушал [MASK]  - Я кушал рыбу). 
- 10% не даем заучить удобные последовательности для минимизации $Loss$ (pred = "Я кушал рыбу", target = "Я гулял рыбу")
- 10% треним как автоэнкодер.

