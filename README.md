# Комментарий к первому домашнему заданию. Вариант 2. 
1. Было выбрано несколько экспрессивов: "жаль", "печально", "сожаление" (в составе "к сожалению"). Все они имеют явную эмоциональную окраску (в нашем случае — это выражание сожаления и грусти), что является основной целью экпрессива как речевого акта. На этом этаме преполагалось, что регресионная модель будет представлять собой стабильно убывающий график, поскольку с высокой долей вероятности эти экпрессивы употребляются в негативном контексте, вряд ли нейтральном или положительном. Нужно также отметить, что экспрессивы отбирались с учетом встречаемости в датасете. 

2. Была построена модель, которая производит предобработку текстов корпуса и строит регрессионную модель. В качестве основного корпуса был выбран размеченный по тональности (positive, neutral, negative; это примерно одинаковые по количеству текстов группы) очищенный корпус отзывов на сайте "Кинопоиск" (за него большое спасибо автору вот этой работы https://habr.com/ru/post/467081/). 

3. Этап предобработки корпуса выполнен с помощью морфологического анализатора pymorphy 2 и включает в себя: отбор только размеченных по тональности текстов, разбиения строки на отдельные элелемнты, приведение форм слов к единой.  

4. Далее по формуле из работы Constant et al. 2009 был вычислен логит, значения которого на графиках отложены на оси _y_. На оси _x_ — значения от -1 до 1, где -1 — негативное, 0,5 — нейтральное, 1 — положительное. 

5. И, наконец, было построено графическое представление регрессионной модели для каждого экспрессива: 

**Для экспрессива "жаль"**

<img width="415" alt="Снимок экрана 2021-10-19 в 17 54 35" src="https://user-images.githubusercontent.com/35366929/137936066-e4364315-32c4-4597-b720-579987d3bdfe.png">

**Для экспрессива "печально"**

<img width="397" alt="Снимок экрана 2021-10-19 в 17 55 59" src="https://user-images.githubusercontent.com/35366929/137936338-69992085-7894-4ec2-9db4-c70715ddf376.png">

**Для экспрессива "сожаление"**

<img width="396" alt="Снимок экрана 2021-10-19 в 17 56 29" src="https://user-images.githubusercontent.com/35366929/137936461-187f6f53-0e4a-4a54-b730-24d44d1a33ac.png">

Здесь мы видим перевернутые J-образные профили. Довольно неожиданно, что в двух случаях из трех нейтральность "перевешивает" негативность контекста, в котором употребляются выбранные экпрессивы. Можно предположить, что поскольку перед нами корпус отзывов на фильмы, в текстах возможен контекст сопереживания (например, "жаль героя"). Подобный контекст не обязательно делает отзыв негативным, а потому выбранные экпрессивы имеют скорее нейтральную, нежели негативную окрашенность. 
Чтобы проверить, верно ли это предположение, был выбран еще один русскоязычный датасет, но на этот раз состоящий из новостной хроники. То есть язык этого корпуса, 
в отличие от отзывов с "Кинопоиска", довольно формальный. Также, он примерно в три раза больше и содержит около 10 000 размеченных текстов. Этот датасет лежит здесь, — https://www.kaggle.com/c/sentiment-analysis-in-russian/data 

Сама модель (кроме тонкостей, связанных с тем, что здесь немного другой формат корпуса) никак не меняется. Соответственно, регрессионные модели для тех же экспрессивов, но в других, более формальных контекстах выглядят следующим образом: 

**Для экспрессива "жаль"**

<img width="415" alt="Снимок экрана 2021-10-19 в 18 22 18" src="https://user-images.githubusercontent.com/35366929/137941556-1e0d28b2-ada2-49bd-bc1e-369611d9b548.png">

**Для экспрессива "печально"**

<img width="408" alt="Снимок экрана 2021-10-19 в 18 22 42" src="https://user-images.githubusercontent.com/35366929/137941620-4e0f62ac-3bc8-4c5c-8388-244d293204f3.png">

**Для экспрессива "сожаление"**

<img width="399" alt="Снимок экрана 2021-10-19 в 18 23 10" src="https://user-images.githubusercontent.com/35366929/137941727-a9723a47-2bf4-472f-a33f-4570b56da2ae.png">

Мы видим, что получившиеся профили выбранных экпрессивов совпадают с предположенными в первом пункте: они отчетливо негативно окрашены, не особенно нейтральны и совсем не положительны. 
Эта особенность и представляет собой интересный случай, возникший в процессе анализа регрессионных моделей разных экпрессивов в корпусе отзывов "Кинопоиска". Именно из-за неочевидности получившихся профилей, был выбран дополнительный корпус для сравнения. 
P.S. Сделнные выводы, разумеется, отстаются на уровне предположений.
