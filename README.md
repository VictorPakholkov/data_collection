# Модуль 2. Практическое задание

## Данные и общая идея

Для выполнения этого практического задания я решил обратиться к текстовым данным с kaggle, представленным в (почти) классическом IMDB Top250 Reviews.

Он доступен здесь: https://www.kaggle.com/datasets/aturret/imdb-top250-reviews

Однако, размечать сантимент на бинарной шкале (положительно-отрицательно, как на rotten tomatoes) имеет довольно мало смысла для такого типа данных, потому что отзывы на фильмы сопровождаются оценкой, которая и без того выражает должный сантимент. 
Кроме того, будем честны, в top250 reviews встречаются *почти исключительно*, если не *исключительно положительные отзывы*, поэтому если разметить все позитивной категорией точность вссе равно будет довольно высока.
Поэтому я решил подойти к задаче для разметчиков с немного другой стороны.

Положительные отзывы не являются неизбежно аппелирующими к одним и тем же чувствам. Кто-то ставит высокую оценку потому что фильм вызывает чувство ностальгии и тоски по детству, кто-то пытается подойти максимально объективно и отмечает влияние на жанр или на кино в целом, кто-то просто вдохновляется фильмом. 
Я решил предположить, что размеченные данные могут потенциально пригодится для классификатора подобного сантимента, не просто устанавливающего благоприятное отношение рецензента к ленте, но и выделяющего причину этого благоприятного отношения.

Таким образом, я решил выделить 5 категорий (осей), которые люди могут упомянать в своих отзывах: classic, inspiring, deep, revolutionary, nostalgic. 
Более подробное описание каждой категории - в ТЗ для разметки.
Кроме того, есть отдельная категория negative на тот случай, если отзыв все же окажется отрицательным (все может быть).

Данные, взятые с kaggle были отчищены (оставлены только осмысленные для задачи колонки - "movie_title", "review_title", "review_rating", "review_text") а также значительно сокращены. В первоначальных данных было 335686 отзывов и не один из моих знакомых ни за что не взялся бы за такую работу забесплатно. Поэтому я решил сократить датасет по принципу один фильм - один отзыв. Всего получилось 250 отзывов (код для препроцессинга доступен в 'IMDB preporcessing.ipynb' в этой ветке).

**UPD:** *250 отзывов так же оказалось слишком много, оба разметчика начали жаловаться, отзывы все таки не однострочные, а на пару абзацев как минимум. Поэтому было принято решение сократить количество отзывов для разметки до 50 (45 для разметчиков при 5 заполненных мной для примера).*


## ТЗ для разметки датасета

Вам необходимо разметить отзывы на кино, выделяя характеристики картины, связанные с положительными впечатлениями зрителей. 
Отзывы должны быть почти исключительно положительные, так как они взяты с IMDB Top250 Reviews, соответственно они оставлены на фильмы с очень высокими оценками.

В каждой строчке содержится один отзыв на один фильм, наряду с заголовком отзыва, который вы так же можете использовать и рейтингом (присуствует не всегда).
Вам необходимо заполнить колонки: F-L для первого разметчика и M-S для второго.
Первые пять колонок, которые вам нужно разметить отражают спектр определенных положительных характеристик, которые могут быть замечены в отзыве человека на фильм: classic, inspiring, deep, revolutionary, nostalgic. 

Вы должны поставить '1' или '0' в зависимости от того, присутствуют ли указания на эти характеристики в отзыве. Вы должны заполнить все колонки, причем в каждой строке может встречаться больше одной '1' (кроме note_1 и note_2 если в этом нет никакой необходимости). 
Если же отзыв оказался негативным, то необходимо поставить '1' в колонку negative_1 или negative_2 соответственно и заполнить все остальные поля нулями.
В случае же, если отзыв не негативный, но ни одной из предложенных характеристик в отзыве не встретилось, то необходимо оставить пометку в note_1 или note_2, записав несколько ключевых слов (через запятую, на английском), которыми автор характеризует фильм в данном отзыве. 
Так же в поле note_1 или note_2 можно оставлять и любые другие замечания и сомнения разметчика, но в случае если это не набор ключевых слов требуется обрамить их обычными скобками '()'.


**Пояснения к категориям:**

*classic -* любые указания на то, что фильм занимает положение классической киноенты в истории кино, как прямые, так и непрямые. Оценка фильма как одного из лучших в своем жанре, чего-то высшей категории своего вида, достойного подражания, большое достижение в истории кино, образцовая лента своего времени/жанра.

Примеры:

"The over-used term "classic movie" really comes into its own here!"

"One of Hitchcock's greatest masterpieces, "Rear Window" is a deep and entertaining classic with many strengths, and a little bit of everything"

"This is the film that put the science in "science fiction"..."


*inspiring -* любое указание на то, что фильм вызывает мощную эмоциональную или ментальную симуляцию, наполняет храбростью и силой для свершений, вдохновляет, дарует моральные и духовные впечатления.

Примеры:

"Usual man's-best-friend story, spiced with an intriguing yet inspiring detail..."

""On the Waterfront" is one of the great American films, not only because it bravely spreads a strong light on the violation of justice, but because it is a powerful piece of cinema, which push forward a classic study of man's responsibility to his fellow man... "


*deep -* любое указание на то, что фильм имеет глубокий смысл, поднимает важные, философские темы, дает пищу для размышления, затрагивает вечные/классичиские истины

Примеры:

"Kubrick also presents the viewer with a lot of food for thought about what it means to be human, and where the human race is going..."

"A Deep & Entertaining Classic"

"The story of corruption in politics and the greatness of the men who resist it is timeless and would not be lost on the politicians in Washington today."


*revolutionary -* любые указания на то, что фильм стал чем-то новым/откровением в своем жанре/в свое время, перезапустил индустрию/жанр, стал основоположником направления/течения, был первым в своем роде

Примеры:

"The revolutionary methods of Kurosawa are still effective and on-par with the cinema of today..."

"Yet Reservoir Dogs is still extraordinarily fresh and vibrant, raising the bar for crime movies in the modern era."


*nostalgic -* любые указания на то, что фильм воспринимается положительно из-за чувства ностальгии, из-за положительных эмоций, вызванных в детстве/раньше, теплый чувств, связанных с возрастом фильма и просмотром в былые времена

Примеры:

"It seems i maybe in the minority for my feelings towards this film, but im not sugar coating my opinion like it seems a few people are doing due to nostalgia."

"There's humor, there's action, there's nostalgia, there's the perfect capture of being a child..."


В данных мною размечено пять первых фильмов, для образца, на который можно ориентироваться. (Сами неразмеченные данные доступны в этой ветке в файле 'data_for_markup.csv') 

Разметку предполагается проводить с помощью excel/google sheets.

## Проверка на адекватность и метрика согласованности

Основным валидатором будет метрика согласованности - в разметке участвуют два разметчика. Однако я также решил добавить небольшую проверку на адекватность - разметил дополнительно пять примеров (поверх тех пяти, что были включены в датасет, отправляемый разметчикам). Это нужно, чтобы проверить, не начали ли размечики размечать данные абсолютно случайно, не вдаваясь в техническое задание. Я не требовал идеальноого совпадения моей тайной разметки с оной от разметчиков, но если вообще никаких пересечений бы не было, то тогда я бы поставил под сомнение качество работы. 

Однако основным валиадтором является метрика согласованности между разметчиками. В следствие того, что колонки для раметки по сути бинарные, я выбрал Cohen's Kappa как подходящий валидатор. 
Он должен быть высчитан сначала индивидуально по фичам, а затем усреднен между всем фичами.


## Обратная связь по разметке 

Разметчики отметили, что по большей мере задание выглядело понятным для них, когда они прочитали ТЗ, однако, когда они приступили к непосредственно разметке, поначалу стали возникать трудности. 
Один из разметчиков отметил, что несмотря на неплохой уровень владения английским яыком, некоторые моменты, особенно касательно оборотов и устойчивых выражений оказались не совсем очевидны, что могло повлиять в том числе и на качество разметки.

Кроме того, оба разметчика отметили, что ТЗ, именно касательно выделяемых категорий сформулировано довольно абстрактно, и несмотря на то, что примеры позволяют примерно уловить  чем речь, разметчики предпочли бы более четкое формализованное определение категориальных понятий, а также некоторый набор keywords, позволяющий отыскивать подходящую тематику в отзывах более эффективно.


## Анализ результатов

По большей мере результаты разметки меня удовлетворили. В целом, разметчики ответственно подошли к задаче и выдали результат, который предполагался ТЗ. Тест на адекватность был пройден успешно, результаты разметки не сильно варьировались от обозначенных мной. Но есть также ряд недостатков.

Во=первых, это пользование полей пользование note_1 и note_2. Проблема отчасти в не особо подробной части ТЗ на эту тему. Разметчики не использовали эти поля иначе как при постановке нулей во все прочие поля. Мною предполагалось (хотя я не смог сформулировать это нормально в ТЗ), что эти поля будут использоваться не только в таких случаях, но и для отметки сомнений, спорных категоризаций и размышлений разметчиков (примерно как мя 5я демонстрационная разметка). 

Другой проблемой с note_1 и note_2 оказался несогласованный в ТЗ формат разметки, который разметчики оставляли, в случае если во всех других полях были нули. Первый разметчик всегда просто перечислял факторы из ревью (cast, plot, atmosphere), в то время как второй разметчик добавлял эпитеты, испольуемые автором (good cast, gripping plot, cozy atmosphere). Это делает эти поля слабо полезными для дальнейшего использования, потому что значнения в них не очень compatable. 

Возникли проблемы и с опечатками, сделанными разметчиками. Иногда встречалось двойное нажатие ('00' вместо '0', '11' вместо '1'). В таких случаях я заменял дублирующиеся цифры на одиночные, чтобы терять меньше информации из датасета. Однако встречались и более грубые и менее очевидные опечатки (например '-' и 'q'). Несмотря на то, что теоретически можно догадаться, что 'q' это скорее всего '1', а '-' это скорее всего '0' из-за близости расположения на клавиатуре, я решил удалить строки с подобными проблемами, чтобы случайно не снизить качество данных при каком-либо другом исходе. 

У первого разметчика так же есть одно пропущенное наблюдение, я решил удалить эту строку из датасета полностью.

Так же, в ходе манипуляций с датасетом через pandas, я отметил, что гораздо лучше бы было попросить размечающих вместо оставления note_1 и note_2 пустыми, заполнить их нулями или прочерками, если они не используются. Это облегчило бы чистку от NaN.


Средняя Cohen's Kappa для всех размеченных полей в датасете (кроме note_1 и note_2) равняется 0.8951310861423221. Несмотря на так себе сформулированное ТЗ, это астрономически высокий результат для подобной задачи. Вероятно сыграли роль малый объем датасета, его чиста (еще уменьшила объем) и относительная простота задания на этих данных.
Код для расчета усредненной каппы лежит в этой ветке в 'inter-rater reliability.ipynb'.


## Выводы

В целом, разметка прошла относительно успешно, однако ТЗ и сам процесс требуют серьезных доработок.

**Во-первых**, в следующий раз при разметке требуется учитывать языковой барьер и культурную специфичность. Даже люди, хорошо знающие иностранный язык не всегда могут справится с подобными задачами именно из-за культурного аспекта, нежели языкового.

**Во-вторых**, очевидным выводом предстает создание более качественного и подробного ТЗ. Добавление определенных keywords для задачи разметки текстов в целом является полезной идеей. Уточнение стандартов заполнения колонок для размечающих тоже может принести свои плоды. Ну и более подробное прописывание ожиданий, с добавлениями примеров не только категоризаций, но и заполнения note_1 и note_2 сыграло бы мне на руку и сделало эти колонки куда пригоднее для дальнейшего использования.
