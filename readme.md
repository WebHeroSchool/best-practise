---
Всем привет это лучшие практики написания javascript кода, которые применяются во всем мире! Используй их и будь счастлив!

---

# h1 Лучшие практики написания javascript кода

## Используйте меньше глобальных переменных, объектов, функций:
Плохой код:

    let stop_word = 'flugenheinmen'
    while(true) {
	if(stop_word === 'flugenheinmen')
	  break;
    }

Хороший код:
    
    while(true) {
    let stop_word = 'flugenheinmen'
	if(stop_word == 'flugenheinmen')
	  break;
    }

Пояснение: старайтесь по возможности минимизировать количество глобальных переменных, объектов, функций. Так как они могут быть легко переписаны из другого места программы, 
в результате чего возникнет трудно уловимая ошибка.

## Объявляйте локальные переменные с ключевыми словами var или let:
Плохой код:

    while(true) {
    stop_word = 'flugenheinmen'
	if(stop_word == 'flugenheinmen')
	  break;
    }

Хороший код:

    while(true) {
    let stop_word = 'flugenheinmen'
	if(stop_word == 'flugenheinmen')
	  break;
    }

Пояснение: всегда объявляйте локальные переменные с ключевым словом var или let. При объявлении локальной переменной без ключевого слова, переменная становится глобальной.

## Декларируйте переменные сверху:
Плохой код:

    let firstName = "John";
    let lastName = "Doe";
    let price = 19.90;
    let discount = 0.10;
    let fullPrice = price * 100 / discount;

Хороший код:

    var firstName, lastName, price, discount, fullPrice;

    firstName = "John";
    lastName = "Doe";
    price = 19.90;
    discount = 0.10;
    fullPrice = price * 100 / discount;

Пояснение: объявляйте свои переменные сверху это сделает ваш код лучше. Сделает его более чистым и читабельным. Организация единого места со всеми переменными упростит их поиск и повысит общую читаемость кода. Будет легче избегать не объявленных локальных переменных, которые станут глобальными. Снизит вероятность переопределения переменной.

## Инициализируйте переменные при объявлении:
Плохой код:

    let firstName, lastName, price, discount, fullPrice, myArray, myObject;

Хороший код:

    let firstName = "",
    lastName = "",
    price = 0,
    discount = 0,
    fullPrice = 0,
    myArray = [],
    myObject = {};

Пояснение: старайтесь всегда присваивать переменным значения при их объявлении. Это сделает код чище и читабельнее. Обеспечит единное место со всеми переменными, что упростит работу с ними. Позволит избежать не инициализируемых переменных.

## Всегда объявляйте number, boolean или string данные как примитивные переменные, а не как объекты:
Плохой код:

    var x = new String("John");
    var y = new String("John");
    (x == y)

Хороший код:

    var x = "John";
    var y = "John";
    (x == y)

Пояснение: объявляйте числа, строки и логические значения как примитивы, а не как объекты. Объявление их как объектов снизит скорость исполнения скрипта и вызовет ряд нежелательных эффектов, как в примере выше нельзя сравнивать объекты через "==".

## Не используйте new Object() и ему подобные:
Плохой код:

    var x1 = new Object();
    var x2 = new String();
    var x3 = new Number();
    var x4 = new Boolean();
    var x5 = new Array();
    var x6 = new RegExp();
    var x7 = new Function(); 

Хороший код:

    var x1 = {};
    var x2 = "";
    var x3 = 0;
    var x4 = false;
    var x5 = [];
    var x6 = /()/;
    var x7 = function(){};

Пояснение: использование new Object() и ему подобных замедлит вашу программу и может привести к неожиданным эффектам.

## Будьте аккуратны с автоматическим приведением типов	:
Плохой код:

    var x = 5 - "x";     // x.valueOf() is NaN, typeof x is a number

Хороший код:

    var x = 5 + 7;       // x.valueOf() is 12,  typeof x is a number
    var x = 5 + "7";     // x.valueOf() is 57,  typeof x is a string
    var x = "5" + 7;     // x.valueOf() is 57,  typeof x is a string
    var x = 5 - 7;       // x.valueOf() is -2,  typeof x is a number
    var x = 5 - "7";     // x.valueOf() is -2,  typeof x is a number
    var x = "5" - 7;     // x.valueOf() is -2,  typeof x is a number

Пояснение: переменные в javascript могут быть разного типа и при совместных оперецаиях, их типы приводятся к какому-то одному типу. При таких преоьразованиях
могут возникать неожиданные результаты, при использовании несовместимых операций, например при использовании оператора "минус" на строке, а не числе.

## Используйте === для сравнения, вместо "==":
Плохой код:

    0 == "";        // true
    1 == "1";       // true
    1 == true;      // true

Хороший код:

    0 === "";       // false
    1 === "1";      // false
    1 === true;     // false

Пояснение: оператор "==" всегда приводит сравниваемые переменные к одному типу, оператор "===" сравнивает переменные с текущими типами, которые у них в данный момент.

## Используйте значения по умолчанию для переменных:
Плохой код:

    function myFunction(x, y) {
      console.log(y + x);
    }

Хороший код:

    function myFunction(x, y) {
      if (y === undefined) {
        y = 0;
      }
    if (x === undefined) {
        x = 0;
      }
      console.log(y + x);
    }

Пояснение: если параметр, испольуемый в вашей программе не задан по умолчанию, старайтесь предусмотреть ему значение по умолчанию. Это уменьшит вероятность ошибок и неожиданных результатов.

## Всегда заканчивайте ваши операторы switch значением по умолчанию:
Плохой код:

    switch (new Date().getDay()) {
  case 0:
    day = "Sunday";
    break;
  case 1:
    day = "Monday";
    break;
  case 2:
    day = "Tuesday";
    break;
  case 3:
    day = "Wednesday";
    break;
  case 4:
    day = "Thursday";
    break;
  case 5:
    day = "Friday";
    break;
  case 6:
    day = "Saturday";
    break;
}


Хороший код:

   switch (new Date().getDay()) {
  case 0:
    day = "Sunday";
    break;
  case 1:
    day = "Monday";
    break;
  case 2:
    day = "Tuesday";
    break;
  case 3:
    day = "Wednesday";
    break;
  case 4:
    day = "Thursday";
    break;
  case 5:
    day = "Friday";
    break;
  case 6:
    day = "Saturday";
    break;
  default:
    day = "Unknown";
}

Пояснение: всегда добавляйте в конце оператора switch значение по умолчанию, даже если думаете, что оно вам не понадобится. Это снизит количество ошибок и не ожиданных эффектов в программе.
