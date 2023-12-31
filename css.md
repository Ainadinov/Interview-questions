# 1. Что такое CSS? Для чего он используется?

`CSS` - каскадное таблица стилей предназначен для добавление различных стилей в HTML страницу.

# 2. Варианты добавление CSS стилей на страницу?

  -- использование инлайновых стилей 
    `<div style="color: red"></div>`
  -- использование глобальные стилей в head 
    `<style> div{color: red} </style>`
  -- использование внешного файла через ссылку
    `<link href="">`
  -- импорт внутри файлов стилей 
    `@import "style/media.css"`

# 3. Типы позиционирования в CSS?

`Static`- по умолчанию, находится основном потоке документа
`Relative` - элемент поз-ся относительно от своего текущего положения
`Absolute` - пози-ся от своего родительского элемента которое не static, ином случае от окне браузера
`Fixed`  - поз-я только отно-о окна браузера
`Sticky` - комби-т своей логики два тип поз-е:
                                            - внутри видимой области браузера видёт себя как fixed
                                            - при последуешим скроле прокручивается вместе с родителем
# 4. Блочная модель CSS?

`Блочная модель` - позволят нам узнать итоговое прастранства занимаеющего  элемента.
                ` [margin [border [padding [content] padding] border] margin]`

# 5. Что такое инлайновый стиль? Можно ли его переопределить?

`Инлайновый стиль?` - это стиль которое пременяется определенному тегую
                `<h1 style="color:red">`

# 7. Есть ли у HTML элементов свой дефолтные специфичные стили?

Каждый элемент обладает своеми наборам стилей:
                -- Список - маркеры, цифры
                -- Зоголовок - разммер, отступы, жирност.
                -- Парагроф - доп-ые маржины

# 8. Что такое селекторы и какие существует?

`Селекторы` - это часть CSS правило, которое сапщает браузеру какому элементу будеть преминятся стилей.
            -- простые - class, #id, p, *
            -- составные - комбинадция селекторов

# 9. Как читать вес селектора? Что такое специфичность  селктора?

`Специфичность` - это способ браузера которое опредеоять какие значение CSS  свойств будет премененый к элементу.
            Весы селектора: inline - 1000, id - 100, class - 10, element - 1

# 10. Разница между Reset.css и Normalize.css?

`Reset.css` - сбрасивает все дефольтные стилей
`Normalize.css` - нормализует все стилей под всем браузерам

# 11. Разница между margin и padding?

`margin` - внешный отступ элемента
`padding` - внутренный отступ элемента

# 12. Разница между display: none и  visibility: hidden?

Оба правила предназначен скрывать элемент:
`display: none ` - полнисью убераеть элемент из страницы
`visibility: hidden ` не смотря на то что элемент не виденб он не удаляется из основной потоке данных. Находится для пойсковых роботов.

# 13. Разница между адаптивным и отсывчивым дизайнем?

`Адаптивный` - есть несколько  HTML, CSS, JS файлов для разного ширины экрана
`Отзивчивый` - есть один набор файлов внутри CSS c помощью медиа запросов изменяем контент для разного ширины экрана.

# 14. Что такое делигирование событие?

`Делигирование` - это прием разработки когда вместо того чтобы вещеть кучу обработчиков однотипного происхождение на все элементы можно добавить  на общего предка.

# 15. Что такое CSS правило?

    Синтаксис: P {color: red};
              selector - выборка элементов для стилизаций
              declaration - блок объявление стилей

# 16. Разница между классом и идентификатором в CSS?

`Class` - не уникальный, для добваление стилей лучше использовать класс 
`Id` - уникальный, лучше использовать для взаймодействия с JS

# 17. Что такое CSS спрайт?

`Спрайт` - это картинка котрое объединяет несколько изображение в одно большое.

# 18. Что такое вендерные префиксы?

`Вендерные префиксы` - это приставка СSS свойств которые обеспечивает поддержку данного свойство браузерами которое оно не внедрена на постоянное основе (Can I Use)

# 19. Разница между Progressive Enhancement и Graceful Degradation?

  Обо использивается для создание клаусплатфор-х приложений
`Progressive Enhancement` - по этапное содание интерфейса от простого к сложному (Mobile -> Tablet -> Laptop)
`Graceful Degradation` - обратное философия деградирует от слажного к более простому (Соврем-й браузер -> Устар-й браузер)

# 20. Что такое псевдоэлементы?

`Псевдоэлементы` - это ключевое слова которое доб-ть на селектор и посволяеть стилизировать элемента
                  -- (first letter, last letter, first-line, before, after, selection)

# 21. Что такое схлопывание границ (margin collapsing)

`Схлопывание границ` - это механизм взоимодействия отступов по вертикально

# 22. Что такое крoссбраузерность?

`Крoссбраузерность` - это корректная адаптивная верстка сайта для правильного отображение по всем браузерами
                    Техники и подходы:
                                      -- Семантическая верстка
                                      -- использивание Reset/Normolize
                                      -- @media запросы

# 23. Что такое  CSS препроцессоры?

`Припроцессор` - это программа которое позволяет генерировать CSS из собственного уникального синтаксиса.
            Синтаксис:
                      -- проще читат
                      -- поддерживат
                      -- переиспользивать
                      -- расшират
            Фичи:
                      -- переменные
                      -- вложенность
                      -- комбинация селекторов
                      -- переисполь-е куски кода
