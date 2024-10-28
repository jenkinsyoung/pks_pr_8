# Практическая работа № 8 (Программирование корпоративных систем)

выполнила: **Полошкова Анастасия Юрьевна**

группа: **ЭФБО-01-22**


## Описание и этапы выполнения работы

В данной работе необходимо было реализовать взаимодействие клиента (приложения) с сервером на Go через REST API. Осуществить хранение данных на локальном сервере, а также управление ими используя методы GET, POST, PUT, DELETE.

1) Написала обработчики запросов в файле **main.go** ветка ***backend***

В данной работе я использовала хранение двух структур: **Product** (информация о товаре) и **Item** (элемент корзины).

```
// Product представляет продукт
type Product struct {
	ID          int
	ImageURL    string
	Title       string
	Description string
	Rules       string
	Price       int
	Age         int
	Gamers      string
	Time        string
	Indicator   int
	IsFavorite  bool
}

// Item представляет элемент корзины
type Item struct {
	ID      int
	Counter int
}
```

Изначально корзина пуста. Содержимое каталога игр хранится в коде программы, без подключения БД

Запросы:
- "http://127.0.0.1:8080/products"  // Получить все продукты
-	"http://127.0.0.1:8080/products/create" // Создать продукт
-	"http://127.0.0.1:8080/products/" // Получить продукт по ID
-	"http://127.0.0.1:8080/products/delete/" // Удалить продукт
-	"http://127.0.0.1:8080/products/update/" // Обновление статуса избранного
-	"http://127.0.0.1:8080/basket"  // Получить все элементы корзины
-	"http://127.0.0.1:8080/basket/" // Проверить есть ли товар в корзине
-	"http://127.0.0.1:8080/basket/add" // Добавить продукт в корзину или обновить количество
-	"http://127.0.0.1:8080/basket/increase" // Увеличить количество товара
-	"http://127.0.0.1:8080/basket/decrease" // Уменьшить количество товара
-	"http://127.0.0.1:8080/basket/remove" // Удалить товар из корзины

Однако при подключению с эмулятора необходимо заменить ```127.0.0.1``` на ```10.0.2.2```

2) Создала новый проект Flutter. Добавила библиотеку для работы с REST API (файл **pubspec.yaml**)

```
dependencies:
  dio: ^5.7.0
```
3) Для получения данных через API был создан файл **server-api.dart** в папке ***lib/server-api/***
4) Продолжила работу над проектом с 6-ой практической, получая данные через API

- Главный экран: каталог настольных игр в две колонки. В дизайне карточек добавлена тень и теперь описание обрезается, чтобы текст не выходил за рамки карточки и чтобы описание могло быть намного длиннее.
  
<img src='https://github.com/user-attachments/assets/38a23984-6166-456f-bf17-672e05750776' width=300 />

<img src='https://github.com/user-attachments/assets/fe0767c8-5847-4c3a-81fa-19bb5c365ef2' width=300 />

- Экран избранное: товары фильтруются из основного списка по сотоянию ***isFavorite***. Состояние обновляется как с карточки товара, так и с экрана информации о товаре через метод PUT
  
<img src='https://github.com/user-attachments/assets/d671d051-7d4c-4824-bbc4-544c3ba392aa' width=300 />

<img src='https://github.com/user-attachments/assets/79a4e371-93fe-466f-a418-723588d14031' width=300 />

<img src='https://github.com/user-attachments/assets/f605348b-d8b8-482e-991d-78d9020730b8' width=300 />

- Экран корзины: добавление товаров через карточку товара или через экран информации о товаре. Если товара еще нет в корзине, то он добавляется, в противном случае счетчик товара увеличивается на 1. Удаление товара из корзины происходит свайпом вправо или влево (обработка запроса DELETE по ID товара)
  
<img src='https://github.com/user-attachments/assets/341a5062-7970-4488-bee1-e35943270df1' width=300 />

<img src='https://github.com/user-attachments/assets/c83c5821-b78a-4135-bd62-20959bef1920' width=300 />

- Экран профиля остался без изменений. Данные остаются только на клиентской части с возможностью их редактирования
  
<img src='https://github.com/user-attachments/assets/0b10f130-7821-44ab-b14e-ac56aca6ce09' width=300 />

<img src='https://github.com/user-attachments/assets/2893cd58-f311-46ca-a0c5-602c9e65a58c' width=300 />

- Экран добавления товара отправляет запрос POST на сервер
  
<img src='https://github.com/user-attachments/assets/f15ce095-b9b9-46b2-ba2d-a6b29b7e624e' width=300 />

<img src='https://github.com/user-attachments/assets/875598a5-bb89-44e6-8301-b9d1f53bc232' width=300 />

- Через экран информации о товаре можно удалить товар из каталога (обработка запроса DELETE по ID товара)

<img src='https://github.com/user-attachments/assets/9274951f-29cf-4b75-9d40-d35565143e44' width=300 />

<img src='https://github.com/user-attachments/assets/a6b63158-0985-4b67-b253-869b23aebfcf' width=300 />

