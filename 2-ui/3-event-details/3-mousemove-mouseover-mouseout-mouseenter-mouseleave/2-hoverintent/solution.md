Будем замерять скорость движения курсора. 

Для этого можно запустить `setInterval`, который каждые 100мс (или другой интервал) будет сравнивать текущие координаты курсора с предыдущими и, если расстояние пройдено маленькое, считаем, что посетитель "навёл указатель на элемент", вызвать `options.over`. 

В браузере нет способа "просто получить" текущие координаты. Это может сделать обработчик события, в данном случае `mousemove`. Поэтому нужно будет поставить обработчик на `mousemove` и при каждом движении запоминать текущие координаты, чтобы `setInterval` мог раз в 100мс сравнивать их.

Можно обойтись и без `setInterval` -- сравнивать координаты при каждом срабатывании `mousemove`. Если передвинулись на маленькое расстояние с последнего `mousemove` -- это "наведение на элемент", а на большое -- игнорируем. Вариант с `setInterval` теоретически надёжнее, но на практике и один `mousemove` работает.

Чтобы наш код не срабатывал чересчур часто, мы будем начинать анализ координат при заходе на элемент, а заканчивать -- при выходе с него. 

Если выход осуществлён, и при этом на элементе зафиксировано "состояние наведения", то нужно вызвать соответствующий обработчик `options.out`.

Чтобы точно отловить момент входа и выхода, без учёта подэлементов (во избежание мигания), можно использовать `mouseenter/mouseleave`. 

В решении, предложенном ниже, однако, используется `mouseover/mouseout`, так как это позволит легко "прикрутить" к такому объекту делегирование, если потребуется. А, чтобы не было лишних срабатываний, лишние переходы отфильтровываются.




