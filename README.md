# JS_6

Javascript

Модуль 6 - Домашнее задание

/* 
  Сеть фастфудов предлагает несколько видов гамбургеров. 
  
  База гамбургера может быть большой или маленькой (обязательно):
	- маленькая (+30 денег, +50 калорий)
	- большая (+50 денег, +100 калорий)
	
  Гамбургер может быть с одной из нескольких видов начинок (обязательно):
	- сыром (+15 денег, +20 калорий)
	- салатом (+20 денег, +5 калорий)
	- мясом (+35 денег, +15 калорий)
	
  Дополнительно, гамбургер можно: 
	- посыпать приправой (+10 денег, +0 калорий) 
	- полить соусом (+15 денег, +5 калорий)
  Типы начинок и размеры надо сделать константами. Никаких магических строк 
  и чисел быть не должно.
  Напишите скрипт, расчитывающий стоимость и калорийность гамбургера. 
  Используте ООП подход, создайте класс Hamburger, константы, методы 
  для выбора опций и рассчета нужных величин. 
  Класс Hamburger, получает на вход информацию о гамбургере, а на выходе 
  дает информацию о каллориях и цене. Никакого взаимодействия с пользователем 
  и внешним миром класс делать не должен - все нужные данные ему передают явно
  в виде аргументов при создании экземпляра. 
  Написанный класс должен соответствовать следующему jsDoc описанию функции-конструктора.
  Вам необходимо написать используя синтаксис ES6 class. То есть класс должен содержать 
  указанные методы, которые принимают и возвращают данные указанного типа.
*/

/*
* Класс, объекты которого описывают параметры гамбургера. 
* @constructor
* @param {String} size - Размер
* @param {String} stuffing - Начинка
*/

function Hamburger({ size, stuffing }) { ... } 

/* Размеры, виды начинок и добавок добавить как статические свойства класса */
Hamburger.SIZE_SMALL = 'SIZE_SMALL';
Hamburger.SIZE_LARGE = ...

Hamburger.SIZES = {
  [Hamburger.SIZE_SMALL]: {
    price: 30,
    calories: 50,
  },
};

Hamburger.STUFFING_CHEESE = 'STUFFING_CHEESE';
Hamburger.STUFFING_SALAD = ...
Hamburger.STUFFING_MEAT = ...

Hamburger.STUFFINGS = {
  [Hamburger.STUFFING_CHEESE]: {
    price: 15,
    calories: 20,
  },
};
					
Hamburger.TOPPING_SPICE = 'TOPPING_SPICE';
Hamburger.TOPPING_SAUCE = ...

Hamburger.TOPPINGS = {
  [Hamburger.TOPPING_SPICE]: {
    price: 10,
    calories: 0,
  },
};

/*
* Добавить topping к гамбургеру. Можно добавить несколько
* topping, при условии, что они разные.
* @param {String} topping - Тип добавки
*/

Hamburger.prototype.addTopping = function (topping) { ... }

/*
 * Убрать topping, при условии, что она ранее была добавлена
 * @param {String} topping - Тип добавки
 */
 
Hamburger.prototype.removeTopping = function (topping) { ... }

/*
 * Получить список toppings
 * @return {Array} - Массив добавленных topping, содержит значения констант Hamburger.TOPPING_*
 */
 
Hamburger.prototype.getToppings = function () { ... }

/*
 * Узнать размер гамбургера
 * @return {String} - размер гамбургера
 */
 
Hamburger.prototype.getSize = function () { ... }

/*
 * Узнать начинку гамбургера
 * @return {String} - начинка гамбургера
 */
 
Hamburger.prototype.getStuffing = function () { ... }

/*
 * Узнать цену гамбургера
 * @return {Number} - Цена в деньгах
 */
 
Hamburger.prototype.calculatePrice = function () { ... }

/*
 * Узнать калорийность
 * @return {Number} - Калорийность в калориях
 */
 
Hamburger.prototype.calculateCalories = function () { ... }

/* 
  Переданную информацию о параметрах гамбургера 
  класс хранит внутри в своих полях. Вот как может 
  выглядеть использование этого класса:
*/

// Маленький гамбургер с начинкой из сыра
const hamburger = new Hamburger({ 
  size: Hamburger.SIZE_SMALL, 
  stuffing: Hamburger.STUFFING_CHEESE
});

// Добавка из приправы
hamburger.addTopping(Hamburger.TOPPING_SPICE);

// Спросим сколько там калорий
console.log("Calories: ", hamburger.calculateCalories());

// Сколько стоит?
console.log("Price: ", hamburger.calculatePrice());

// Я тут передумал и решил добавить еще соус
hamburger.addTopping(Hamburger.TOPPING_SAUCE);

// А сколько теперь стоит? 
console.log("Price with sauce: ", hamburger.calculatePrice());

// Проверить, большой ли гамбургер? 
console.log("Is hamburger large: ", hamburger.getSize() === Hamburger.SIZE_LARGE); // -> false

// Убрать добавку
hamburger.removeTopping(Hamburger.TOPPING_SPICE);
						     
// Смотрим сколько добавок
console.log("Hamburger has %d toppings", hamburger.getToppings().length); // 1

/*
  Обратите внимание на такие моменты:
    - класс не взаимодействует с внешним миром. Это не его дело, этим занимается 
    	другой код, а класс живет в изоляции от мира
	
    - обязательные параметры (размер и начинка) мы передаем через конструктор, 
    	чтобы нельзя было создать объект, не указав их
	
    - необязательные (добавка) добавляем через методы
    
    - имена методов начинаются с глагола и имеют вид «сделайЧтоТо»: calculateCalories(), addTopping()
    
    - типы начинок обозначены "константами" с понятными именами (на самом деле просто 
    	свойствами, написанным заглавными буквами, которые мы договорились считать "константами")
	
    - объект создается через конструктор - функцию, которая задает начальные значения полей. 
      	Имя конструктора пишется с большой буквы и обычно является существительным: new Hamburger(...)
    
    - в свойствах объекта гамбургера логично хранить исходные данные (размер, тип начинки), 
      	а не вычисленные из них (цена, число калорий и т.д.). Рассчитывать цену и калории 
	логично в тот момент, когда это потребуется, а не заранее.
*/
