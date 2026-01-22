# Fullstack

 
## 4 МОДУЛЬ - Разработка клиент серверного приложения 

Клиент  frontend 
Сервер  backend

В конце вся разработка на Reakt - функция которая возвращает разметку ииииууу
                                     
                                    
 Backend Сервер - это сервер + сервеное приложение + бизнес логика (сценарии обработки клиентских запросов)
в основном все будет со стрелочной функцией

### Технологический стек разработки
_______________
P.E.R.N  + ORM sequelize

Postgres

Express

React

Node.js

________________
## Node.Js
Платформа для языка js позволяющая ему работать вне браузера 

### Основная особенность Ассинхронность и Событийно-ориентировання архитектура.
Основные параметры 

Неблокирующий ввод-вывод (когда серверу нужно выполнить операцию ввода вывода, например прочитать файл с диска или запрос в бд оно не ждет ее завершения 

Вместо этого выполняет другой код, как только операция завершается, вызывается функция обработчик Call back.

Однопоточность с циклом событий - Ivent Loop

Цикл событий - механизм который постоянно прореверяет завершшились ли какие то ассинхронные операции

Ассинхронные операции - операция которая выполнится когда нибудь

### N.P.M - менеджер пакетов

Позволяет установить и использовать открытые библиотеки и инструменты

_________________



# Этапы разработки проекта на Node.js

#### 1 Подготовка и инициализация
1.1 Создание директорий проекта ( папки клиент и сервер)

1.2 Инициализация 

1.3 Установка необходимых зависимостей (модулей  npm Install express)

#### 2 Создание hhtp сервера через express 

2.1 Импорт фреймворка express и определение порта на котором сертвер будет принимать входящие подключения 

2.2 Создание портов и переменных окружения

2.3 Создение файла конфигурации базы данных

2.4 Настройка промежуточного ПО (Middle Ware)

#### 3 Описание моделей данных ( с помощью sequelize )

Работа с таблицами  БД как с JS обьектами

#### 4 Создание маршрутов (Routes) и API Endpoints 



HTML 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="./style.css">
    <title>Document</title>
</head>
<body>
    <table>
        <thead>
            <tr>
                <td>
                    ID
                </td>
                <td>
                    name
                </td>
                <td>
                    age
                </td>
            </tr>
        </thead>
        <tbody id = 'tbody'>
            
        </tbody>
    </table>
    <script src="./script.js"></script>
</body>
</html>

js 
const dataset = [
    { id: 1, name: 'Ivanov', age: 30 },
    { id: 2, name: 'Petrov', age: 24 },
    { id: 3, name: 'Sidorov', age: 10 }
]

const table = (data) => {
const tbody = document.getElementById('tbody')

data.forEach(element => {
tbody.innerHTML =`
 <tr><td> ${element.id} </td>

 <td> ${element.name} </td>
 
<td> ${element.age} </td></tr>`
})

}
table(dataset)



Данное решение не оптимальное потому что количество атрибутов получается фиксированное нашей html разметкой 

Самое главное - в коде есть уязвимость : переддача данных через Inner создает XSS уязвимость

Поетому рассмотрим другие варианты :
2 Исключим XSS уязвимость 

const dataset = [
    { id: 1, name: "Ivanov", age: 30},
    { id: 2, name: "Petrov", age: 24},
    { id: 3, name: "Sidorov", age: 10},
]

const table = (data) => {
    const tbody = document.getElementById("tbody")
    data.forEach( element => {
        const tr = tbody.insertRow()
        const cellId = tr.insertCell()
        cellId.textContent = element.id
        const cellName = tr.insertCell()
        cellName.textContent = element.name
        const cellAge = tr.insertCell()
        cellAge.textContent = element.age})




}

table(dataset)



отрисовать полностью динамическую таблицу и что бы заголовки учитыались и что бы строки и ячейки таблицы создавались  по количеству чего то там в обьекте 

перебор ключей обьектов Object.keys(data[0])
