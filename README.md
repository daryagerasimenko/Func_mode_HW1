# Вариант 2. Комментарий к заданию.  
# Введение

Было выбрано несколько экспрессивов: "жаль", "печально" и "сожаление" (поскольку встречается в составе выражения "к сожалению"). Все они имеют явную эмоциональную окрашенность (в нашем случае — это выражение сожаления и грусти), что является основной целью экспрессива как речевого акта. На этом этапе предполагалось, что регрессионная модель будет представлять собой почти равномерно убывающий график, поскольку предположительно эти экспрессивы употребляются именно в негативном контексте. Пример, на основании которого делается это предположение, может быть следующим. В исследовании "The pragmatics of expressive content: Evidence from large corpora" был построен график для англоязычного экспрессива "superb", который в некотором роде по смыслу можно противопоставить русскоязычному "печально" или "жаль": 

<img width="499" alt="Снимок экрана 2021-10-19 в 19 09 00" src="https://user-images.githubusercontent.com/35366929/137949866-63eace1e-58f6-4e65-8175-a022714504a9.png">

Мы видим, что график монотонно возрастает. От выбранных русскоязычных экспрессивов ожидался такой же монотонный график, но убывающий. 
Однако в результате графики регрессионных моделей выбранных экспрессивов имели совершенно иной профиль. В связи с этим возникла гипотеза, что такие характеристики корпуса "Кинопоиска" как неформальность речи, яркая эмоциональная окрашенность, вызванная тем, что тексты датасета — реакция на фильмы, и т.п. могут влиять на вид графика регрессионной модели. Поэтому дополнительно был выбран другой русскоязычный корпус — новостная хроника. Он примерно в три раза больше датасета "Кинопоиска" и содержит около 10 000 размеченных текстов. Для сравнения на основе той же модели были построены дополнительные графики регрессионных моделей уже по данным второго корпуса. Он лежит в репозитории, а также тут — https://www.kaggle.com/c/sentiment-analysis-in-russian/data 

# Этапы работы 

1. Была произведена предобработка корпуса текстов и построены графики регрессионных моделей. В качестве основного был выбран корпус, состоящий из текстов отзывов на сайте "Кинопоиск", размеченный для решения задачи определения тональности (negative, neutral, positive). В корпусе примерно одинаковое количество текстов каждого класса. За корпус благодарность автору вот этой статьи: https://habr.com/ru/post/467081/.

2. Этап предобработки корпуса включает в себя разбиение текстов на отдельные слова и приведение их к нормальной форме с помощью морфологического анализатора pymorphy2.  

4. Далее по формуле из работы "The pragmatics of expressive content: Evidence from large corpora" были вычислены значения log-odds, которые на получившихся графиках отложены на оси y. На оси x — значения от -1 до 1, где -1 — соответствует негативной тональности текста, 0,5 — нейтральной, а 1 — положительной. 

5. И наконец, были построены графики регрессионных моделей для каждого экспрессива. 

# Графики регрессионных моделей 
## Корпус "Кинопоиска"

### Экспрессив "жаль"

<img width="415" alt="Снимок экрана 2021-10-19 в 17 54 35" src="https://user-images.githubusercontent.com/35366929/137936066-e4364315-32c4-4597-b720-579987d3bdfe.png">

e.g. 

_...И отдельно — сцена её гибели — снова великолепно и безумно её жаль._

_Жаль, что к ним не присоединился Шон из Токио._

_Мне жаль человека, который не видел вырезаную версию._

_Откровенно жаль, к примеру, когда он разговаривает с отцом о четырех добродетелях._


### Экспрессив "печально"

<img width="397" alt="Снимок экрана 2021-10-19 в 17 55 59" src="https://user-images.githubusercontent.com/35366929/137936338-69992085-7894-4ec2-9db4-c70715ddf376.png">

e.g. 

_Весь это фильм с максимально трагическим сюжетом отражает, как ни печально, самую актуальную проблему современного общества._

_Никто уже не собирается возвращаться к истокам, что очень и очень печально._


### Экспрессив "сожаление"

<img width="396" alt="Снимок экрана 2021-10-19 в 17 56 29" src="https://user-images.githubusercontent.com/35366929/137936461-187f6f53-0e4a-4a54-b730-24d44d1a33ac.png">

e.g. 

_Я не критик и не профи — просто любитель хорошего и качественнего кино, которого, к сожалению, очень мало._

_Тёмный рыцарь я не смотрел, к сожалению, хотя я и люблю актёра Хита Леджера._

_Если ты не можешь изменить этот мир, единственный выход — это смерть, к сожалению, но это действительно так._

## Новостной корпус 

### Экспрессив "жаль"

<img width="415" alt="Снимок экрана 2021-10-19 в 18 22 18" src="https://user-images.githubusercontent.com/35366929/137941556-1e0d28b2-ada2-49bd-bc1e-369611d9b548.png">

e.g. 

_Очень жаль, что ваш банк так работает._

_Жаль, что мы не увидим запуск настоящей ракеты._

### Экспрессив "печально"

<img width="408" alt="Снимок экрана 2021-10-19 в 18 22 42" src="https://user-images.githubusercontent.com/35366929/137941620-4e0f62ac-3bc8-4c5c-8388-244d293204f3.png">

e.g. 

_Печально, если могучий ствол государственности облюбовали разные жучки-короеды…_

_Как бы печально это ни звучало, нужно принять, что моя спортивная карьера уже закончена._

_О печальном положении казахстанского авторынка мы говорили уже не раз._


### Экспрессив "сожаление"

<img width="399" alt="Снимок экрана 2021-10-19 в 18 23 10" src="https://user-images.githubusercontent.com/35366929/137941727-a9723a47-2bf4-472f-a33f-4570b56da2ae.png">

e.g.

_...К сожалению, 8 партнеров с нами уже не работают._

_К сожалению, как показали недавние события, Нацбанк оказался не в состоянии обеспечить соответствующей защиты и требуемой прозрачности._

_Но, к сожалению, некоторые не справляются с симптомами звездной болезни._

# Выводы

На графиках регрессионных моделей к экспрессивам из корпуса "Кинопоиск" мы видим перевернутые J-образные профили. Довольно неожиданно, что в двух случаях из трех нейтральность "перевешивает" негативность контекста, в котором употребляются выбранные экспрессивы. Как уже было сказано, можно предположить, что поскольку перед нами корпус отзывов на фильмы, в текстах возможен контекст сопереживания (например, "жаль героя"). Подобный контекст не обязательно делает отзыв негативным, а потому выбранные экспрессивы имеют также и нейтральную окрашенность.

На графиках регрессионных моделей к экспрессивам из корпуса новостной хроники мы видим, что их профили совпадают с предположенными изначально: они отчетливо негативно окрашены, а графики монотонно убывают. Можно предположить, что в новостном стиле изложения набор экспрессивов более предсказуем и используется в крайне предсказуемых контекстах. В отзывах к фильмам же все иначе: экспрессивы там менее предсказуемы и могут использоваться в более широком ряде контекстов. Эта особенность представляет собой интересный случай, неожиданно возникший в процессе анализа профилей разных экспрессивов в корпусе отзывов "Кинопоиска". 
