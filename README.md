# prjctr-node-test-task
Привет! Если ты находишься здесь - значит ты хочешь узнать больше о Node.js, присоединясь к обучению в Projector. Для этого осталось лишь пару шагов, и один из них - это тестовое задание по JS. Оно надо для того, чтобы обучение было максимально качественным для всех - для тебя, для других студентов и для преподавателя. Ведь если ты не будешь знать основ JS - тебе будет очень трудно. Задания не сложные, выполнение их при должном уровне сноровки занимает не больше 1 часа. Удачи!

## Задание №1
Реализовать функцию `groupBy` на чистом JS, которая будет группировать массив по определённой функции, переданной вторым аргументом:
```
const groupBy = (array, func) => {
   ...
}

console.log(groupBy([3.6, 3.7, 6.4, 8.9], Math.floor)) // { '3': [3.6, 3.7], '6': [6.4], '8': [8.9] }
```
## Задание №2
Реализовать функцию `invert` на чистом JS, которая будет менять ключи и значения объектов местами:
```
const invert = (obj) => {
   ...
}

console.log(invert({ 'a': 'some', 'b': 'object', 'c': 1 })) // { 'some': 'a', 'object': 'b', '1': 'c' }
```
## Задание №3
Реализовать функцию `checkParentheses` на чистом JS, которая проверяет на синтаксическую верность последовательность скобок ( (), {} и [] ). Функция возвразает `false`, если переданная строка содержит неправильную последовательность:
```
const checkParentheses = (str) => {
   ...
}

console.log(checkParentheses('--()--')) // true
console.log(checkParentheses('-a]--[')) // false
console.log(checkParentheses('dsa{vsfs{ad')) // false
console.log(checkParentheses('j78(g5b]uyg')) // false
console.log(checkParentheses(',m{i987y}hj')) // true
console.log(checkParentheses('dsa[3ed---:]::')) // true
```
## Задание №4
Дан объект, эмулирующий в самом примитивном виде слой работы с данными:
```
const database = {
    getUser: (id, callback) => {
        const users = [{
            id: 1,
            name: 'Robert',
        }, {
            id: 2,
            name: 'John'
        }];
        
        const user = users.find((user) => user.id === id);
        if (!user) {
            callback(`User with id=${id} not found`);
        } else {
            callback(null, user);
        }
    },
    getUsersBook: (userId, callback) => {
        const usersBooks = {
            1: [],
            2: [1, 2],
        };

        const userBook = usersBooks[userId];
        if (!userBook) {
            callback(`Set of books related to userId=${userId} not found`);
        } else {
            callback(null, userBook);
        }
    },
    buyBook: (id, callback) => {
        const books = [{
            id: 1,
            name: 'Art of war'
        }, {
            id: 2,
            name: 'Hunger games'
        }, {
            id: 3,
            name: '1984'
        }];

        const book = books.find((book) => book.id === id);
        if (!book) {
            callback(`Book with id=${id} not found`);
        } else {
            callback(null, true);
        }
    },
};
```
Необходимо с помощью Promises (async/await) отрефакторить функцию ниже, чтобы избежать большого количества уровней вложенности, а также чтобы повысить читаемость:
```
const buyBookForUser = (bookId, userId, callback) => {
    database.getUser(userId, (err, user) => {
        if (err) {
            callback(err);
        } else {
            database.getUsersBook(userId, (err, userBooks) => {
                if (err) {
                    callback(err);
                } else {
                    if (userBooks.includes(bookId)) {
                        callback(`User already has book with id=${bookId}`);
                    } else {
                        database.buyBook(bookId, (err) => {
                            if (err) {
                                callback(err);
                            } else {
                                callback(null, 'Success');
                            }
                        });
                    }
                }
            })
        }
    })
}
```
Вот код тестов, применимый для текущей реализации:
```
buyBookForUser(1,1, (err, message) => {
    console.log(err) // null
    console.log(message) // 'Success'
})

buyBookForUser(1,2, (err, message) => {
    console.log(err) // 'User already has book with id=1'
    console.log(message) // undefined
})

buyBookForUser(3,2, (err, message) => {
    console.log(err) // null
    console.log(message) // 'Success'
})

buyBookForUser(5,2, (err, message) => {
    console.log(err) // 'Book with id=5 not found'
    console.log(message) // undefined
})

buyBookForUser(1,3, (err, message) => {
    console.log(err) // 'User with id=3 not found'
    console.log(message) // undefined
})
```
Отрефакторенный код должен возвращать те же результаты, но может иметь другой вид.

Результатом выполнения данного тестового должен быть открытый репозиторий с минимум 4 файлами (одно задание - один файл).
А ссылку на свой репозиторий добавь сюда:
https://form.typeform.com/to/habPJsGo
