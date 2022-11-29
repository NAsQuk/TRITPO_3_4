
# Содержание
1 [Введение](#intro)  
1.1 [Назначение](#appointment)  
2   [USE CASE](#business_requirements)  
2.1 [ADMIN](#initial_data)  
2.1.1 [Добавление нового банка](#business_opportunities)  
2.1.2 [Редактирование значений валют и/или данных банка](#project_boundary)  
2.1.3 [Вход в систему](#analogues)  
2.2 [USER](#user_requirements)  
2.2.1 [Выбор отделения банка на карте](#software_interfaces)  
2.2.2 [Добавление виджета](#user_interface)  
2.2.3 [Смена основного банка(валюты)](#user_specifications)  
3 [МОДЕЛЬ ПРЕДМЕТНОЙ ОБЛАСТИ](#user_classes)  
3.1 [Глоссарий](#user_logon_to_the_application)  
3.2 [Взаимодействие компонентов](#setting_up_the_profile_of_the_active_user)  
3.3 [Диаграмма классов](#download_news)  
3.4 [Пользовательский сценарий](#view_information_about_an_individual_newsletter)  
3.5 [Состояния системы](#active_user_change)  
3.6 [Физическая структура системы](#add_new_user)  
3.7 [Функциональные требования](#restrictions_and_exclusions)  

<a name="intro"/>

# 1 Введение

<a name="appointment"/>

## 1.1 Назначение
Документ разработан для однозначной трактовки требований между разработчиком и заказчиком. Необходимо разработать мобильное приложение с простым функционалом и актуальной информацией о ценах на валюты. Необходимо, чтобы приложение имело главную страницу, с основными данными по ценам на покупку/продажу валют, выбор банка, выбор валюты, в которой выводятся цены на главной странице( первоначальная валюта - Белорусский рубль). Вторая страница - разворот с картой выбранного пользователем города, на карте меткой (круг, точка(по выбору заказчика)) обозначены отделения выбранного банка или же отделения всех доступных приложению банков(или только один, или все). На данной странице необходимо реализовать поиск необходимого города и выбор необходимого банка. Для работы приложения требуется стабильное Интернет соединение, а так же подключенная геолокация( не является обязательной функцией, необходима для просмотра ближайших отделений банка).   
В этом документе описаны функциональные и нефункциональные требования к мобильному приложению «Watch & buy» для Android, IOS. 
Этот документ предназначен для команды, которая будет реализовывать и проверять корректность работы приложения. 

<a name="business_requirements"/>

# 2 USE CASE

Далее будут преставлениы возможные ситуации, которые могут возникать при использовании приложения, как со стороны администратора, так и со стороны пользователя. 

<a name="initial_data"/>

## 2.1 ADMIN

<a name="business_opportunities"/>

### 2.1.1 Добавление нового банка

Поток событий для прецедента «Добавление нового банка»
Основной поток:
1. Вариант использования начинается, когда администратор заходит на
страницу для просмотра карт
2. Администратор посылает запрос на добавление нового банка - выполняется альтернативный поток А1.
3. Если введенный администратором банк уже существует в системе приложения - выполняется поток ошибки E1.
4. Администратор проверяет корректность добавления банка путем проверки его отображения на карте и просмотра информации о банке.
6. Система ищет в базе данных информацию о запрашиваемом банке, если нужный банк не найден - выполняется поток ошибки Е2.
7. Система выдает администратору информацию о банке.
8. Вариант использования завершается 

Альтернативный поток А1:
1. Система выдает администратору новую страницу для ввода
необходимой информации
2. Администратор вводит необходимую информацию
3. Новый банк добавляется в базу и становится доступным для просмотра на карте, но не отображается в приложении до завершения администартором цикла добавления
4. Вариант использования завершается

Альтернативный поток E1:
1. Система ищет в базе данных информацию о нужном банке
2. Система выдает сообщение об ошибке если вводимый банк уже существует в системе.
3. Поток ошибки завершается.

<a name="project_boundary"/>

### 2.1.2 Редактирование значений валют и/или данных банка

Поток событий для прецедента «Редактирование значений валют и/или данных банка»
Основной поток:
1. Вариант использования начинается, когда администратор заходит на
страницу нужного банка
2. Администратор посылает запрос на редактирование банка - выполняется альтернативный поток А1.
3.Администратор проверяет корректность добавления банка (или валюты ).
4. Система выдает администратору информацию о нужном банке/валюте.
5. Вариант использования завершается
 
Альтернативный поток А1:
1. Система ищет в базе данных информацию о нужном банке/валюте, если нужного
банка/вылюты нет, выполняется поток ошибки Е2.
2. Система выдает администратору страницу для редактирования
необходимой информации
3. Администратор вводит необходимую информацию
4. Отредактированный фильм сохраняется в базе данных, но не отображается
в приложении
5. Вариант использования завершается


<a name="analogues"/>

### 2.1.3 Вход в систему

Поток событий для прецедента «Вход в систему»
Основной поток:
1. Вариант использования начинается, когда администратор входит в систему
2. Система запрашивает у администратора учетные данные
3. Администратор вводит свои учетные данные
4. Система подтверждает введенные администратором учетные данные, если
данные не подтверждаются, выполняется альтернативный поток А1 
5. Вариант использования завершается

Альтернативный поток А1:
1. Система просит ввести данные еще 3 раза, если попытки истекают,
выполняется альтернативный поток А11
2. Вариант использования завершается

Альтернативный поток А11:
1. Система блокирует вход администратора
2. Вариант использования завершается 

<a name="user_requirements"/>

## 2.2 USER

<a name="software_interfaces"/>

### 2.2.1 Выбор отделения банка на карте

Поток событий для прецедента «Выбор отделения банка на карте»
Основной поток:
1. Вариант использования начинается, когда пользователь открывает приложение и заходит на страницу с просмотром карт
2. Пользователь вводит имя банка: банк найден - поток А1, такого банка нет - поток А2.
3. Администратор вводит свои учетные данные
4. Система подтверждает введенные администратором учетные данные, если
данные не подтверждаются, выполняется альтернативный поток А1 
5. Вариант использования завершается

Альтернативный поток А1:
1. Отображение банка на катре и вывод всей информации о найденном банке.
2. Вариант использования завершается

Альтернативный поток А11:
1. Сообщение об ошибке поиска, такой банк не найден.
2. Вариант использования завершается 
<a name="user_interface"/>

### 2.2.2 Добавление виджета

Поток событий для прецедента «Добавление виджета»
Основной поток:
1. Вариант использования начинается, когда пользователь (не заходя в приложение или с главной страницы приложеняи) выбирет функцию добавление виджета.
2. Приложение присылает ответ на запрос: нет выбранной основной валюты - поток А1, нет выбранного банка - поток А2.
3. Появляется возможность добавления виджета: нет ошибок - поток А3, нет мета на рабочей странице - поток ошибки Е1.
4. Вариант использования завершается
 
Альтернативный поток А1:
1. Приложение запрашивает ввод валюты для отображения, введена валюта, которой не в базе - поток ошибки - Е2.
2. Вариант использования завершается

Альтернативный поток А2:
1. Приложение запрашивает ввод банка для отображения, введена валюта, которой не в базе - поток ошибки - Е2.
2. Вариант использования завершается

Альтернативный поток А3:
1. Добавление виджета на основной экран.
2. Настройка размеров.
3. Вариант использования завершается

<a name="user_specifications"/>

### 2.2.3 Смена основного банка(валюты)

Поток событий для прецедента «Смена основного банка(валюты)»
Основной поток:
1. Вариант использования начинается, когда пользователь  заходя в приложение  выбирет функцию изменить банк/валюту.
2. Приложение присылает ответ на запрос: нет выбранной основной валюты - поток А1, нет выбранного банка - поток А2.
3. Появляется возможность измените банк/валюту: нет ошибок - поток А3.
4. Вариант использования завершается
 
Альтернативный поток А1:
1. Приложение запрашивает ввод валюты, введена валюта, которой не в базе - поток ошибки - Е2.
2. Вариант использования завершается

Альтернативный поток А2:
1. Приложение запрашивает ввод банка, введена валюта, которой не в базе - поток ошибки - Е2.
2. Вариант использования завершается

Альтернативный поток А3:
1. Банк/валюта успешно изменены.
2. Вариант использования завершается

<a name="user_classes"/>

# 3 МОДЕЛЬ ПРЕДМЕТНОЙ ОБЛАСТИ





<a name="user_logon_to_the_application"/>


## 3.1 Глосарий
 Основная терминология

| ТЕРМИН | ОПРЕДЕЛЕНИЕ | 
|:---|:---|
| Валюта | Деньги в обращении конкретного государства, которые определяют стоимость товаров и услуг |
| Администратор | Человек, ответственный за корректную работу приложения, а так же добавление новых валют и новых банков на карту |
| Пользователь | Человек, который использует приложение |
| Геолокация | Средство определения реального географического местоположения электронного устройства, например радиопередатчика, сотового телефона или компьютера, подключённого к сети Интернет |
| сеть Интернет | Информационно-коммуникационная сеть и всемирная система объединённых компьютерных сетей для хранения и передачи информации |

<a name="restrictions_and_exclusions"/>

## 3.2 Взаимодействие компонентов
![](https://github.com/NAsQuk/TRITPO_3_4/blob/main/schemes/Vzaimodeystvie_komponentov.png) 

<a name="quality_attributes"/>

## 3.3 Диаграмма классов

<a name="requirements_for_ease_of_use"/>

## 3.4 Пользовательский сценарий


<a name="security_requirements"/>

## 3.5 Состояния системы


<a name="external_interfaces"/>

## 3.6 Физическая структура системы

<a name="restrictions"/>

## 3.7 Функциональные требования
