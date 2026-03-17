# Задачи по ООП на Python: основы

---

## Тема 1: Основы класса и магия `self`
**Цель:** Понять, что `self` — это способ объекта «обратиться к самому себе», чтобы запоминать свое состояние и изменять его. 

**Что такое класс?**
Представь, что класс — это чертеж или рецепт (например, чертеж автомобиля). А объект — это реальная машина, построенная по этому чертежу. Мы можем создать тысячи машин по одному чертежу, и у каждой будет свой цвет или номер.

**Зачем нужен self?**
Внутри класса self — это переменная, которая указывает на конкретный объект, с которым мы сейчас работаем.

Через self.название мы создаем «память» объекта (атрибуты).

Без self переменная будет видна только внутри одного метода и сразу «забудется».

**Пример:** Если у нас есть 10 роботов, и мы говорим self.battery = 100, то заряд 100 появится именно у того робота, которого мы сейчас настраиваем, а не у всех сразу.

### Уровень 1: Начальный (Простые переключатели)

**1. Демо-задача: «Умная лампочка»** Создай класс `SmartBulb`. Напиши метод `turn_on(self)`, который создает атрибут `self.is_on = True`, и метод `turn_off(self)`, который делает `self.is_on = False`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class SmartBulb:
    def turn_on(self):
        self.is_on = True
        print("Лампочка включена!")
        
    def turn_off(self):
        self.is_on = False
        print("Лампочка выключена!")

# Проверка:
bulb = SmartBulb()
bulb.turn_on()
bulb.turn_off()
```

</details>

---

**2. Практика: «Кликер»** Создай класс `Clicker`. Метод `start(self)` задает `self.score = 0`. Метод `click(self)` увеличивает `self.score` на 1.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Clicker:
    def start(self):
        self.score = 0
        
    def click(self):
        self.score += 1
        print(f"Клик! Счет: {self.score}")
```

</details>

---

**3. Практика: «Кот-тамагочи»** Создай класс `Cat`. Метод `wake_up(self)` делает `self.is_hungry = True`. Метод `feed(self)` меняет `self.is_hungry` на `False`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Cat:
    def wake_up(self):
        self.is_hungry = True
        print("Кот проснулся и хочет есть!")
        
    def feed(self):
        self.is_hungry = False
        print("Кот сыт и доволен.")
```

</details>

---

**4. Практика: «Музыкальный плеер»** Создай класс `Player`. Метод `play(self)` задает `self.status = "playing"`, а `pause(self)` задает `self.status = "paused"`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Player:
    def play(self):
        self.status = "playing"
        print("Музыка играет 🎵")
        
    def pause(self):
        self.status = "paused"
        print("Пауза ⏸️")
```

</details>

---

### Уровень 2: Средний (Взаимодействие атрибутов)

**1. Демо-задача: «Космический корабль»** Класс `Spaceship`. Метод `refuel(self, amount)` добавляет топливо в `self.fuel` (изначально нужно задать 0). Метод `fly(self, distance)` тратит топливо (1 ед. на 10 км) и увеличивает `self.mileage`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Spaceship:
    def build(self):
        self.fuel = 0
        self.mileage = 0
        
    def refuel(self, amount):
        self.fuel += amount
        print(f"Заправлено на {amount}. Всего топлива: {self.fuel}")
        
    def fly(self, distance):
        fuel_needed = distance / 10
        if self.fuel >= fuel_needed:
            self.fuel -= fuel_needed
            self.mileage += distance
            print(f"Пролетели {distance} км. Пробег: {self.mileage}")
        else:
            print("Не хватает топлива для полета!")
```

</details>

---

**2. Практика: «Копилка»** Класс `PiggyBank`. Метод `set_empty(self)` делает `self.coins = 0`. Метод `add_coin(self, value)` добавляет монеты. Метод `break_bank(self)` возвращает все монеты и обнуляет счетчик.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class PiggyBank:
    def set_empty(self):
        self.coins = 0
        
    def add_coin(self, value):
        self.coins += value
        
    def break_bank(self):
        total = self.coins
        self.coins = 0
        print(f"Копилка разбита! Вы достали {total} монет.")
        return total
```

</details>

---

**3. Практика: «Здоровье персонажа»** Класс `Hero`. Метод `spawn(self)` дает `self.hp = 100`. Метод `take_damage(self, damage)` уменьшает ХП, а `heal(self, amount)` — увеличивает.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Hero:
    def spawn(self):
        self.hp = 100
        
    def take_damage(self, damage):
        self.hp -= damage
        print(f"Получен урон {damage}! Осталось HP: {self.hp}")
        
    def heal(self, amount):
        self.hp += amount
        print(f"Вылечено {amount} HP! Текущее HP: {self.hp}")
```

</details>

---

**4. Практика: «Кондиционер»** Класс `AirConditioner`. Метод `turn_on(self)` задает `self.temp = 22`. Методы `warmer(self)` и `cooler(self)` меняют температуру на 1 градус.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class AirConditioner:
    def turn_on(self):
        self.temp = 22
        
    def warmer(self):
        self.temp += 1
        print(f"Температура повышена: {self.temp}°C")
        
    def cooler(self):
        self.temp -= 1
        print(f"Температура понижена: {self.temp}°C")
```

</details>

---

### Уровень 3: Достаточный (Логика внутри методов)

**1. Демо-задача: «Кофемашина»** Класс `CoffeeMachine`. Метод `fill(self, water, beans)` пополняет запасы. Метод `make_coffee(self)` проверяет ресурсы (200 мл воды, 20 г зерен).

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class CoffeeMachine:
    def setup(self):
        self.water = 0
        self.beans = 0
        
    def fill(self, water, beans):
        self.water += water
        self.beans += beans
        
    def make_coffee(self):
        if self.water >= 200 and self.beans >= 20:
            self.water -= 200
            self.beans -= 20
            print("Ваш кофе готов! ☕")
        else:
            print("Ошибка: недостаточно воды или зерен!")
```

</details>

---

**2. Практика: «Продвинутый тамагочи»** Доработай класс `Hero`. ХП не может быть больше 100. Если при методе `take_damage` ХП падает ниже 0, кот падает в обморок (`self.is_fainted = True`).

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class AdvancedCat:
    def spawn(self):
        self.hp = 100
        self.is_fainted = False
        
    def heal(self, amount):
        self.hp += amount
        if self.hp > 100:
            self.hp = 100
            
    def take_damage(self, damage):
        self.hp -= damage
        if self.hp <= 0:
            self.hp = 0
            self.is_fainted = True
            print("Кот упал в обморок! 😵")
```

</details>

---

**3. Практика: «Принтер»** Класс `Printer`. Создай `setup(self, paper, ink)`. Метод `print_page(self, text)` считает символы. Каждый символ тратит 1 ед. краски, печать — 1 лист бумаги.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Printer:
    def setup(self, paper, ink):
        self.paper = paper
        self.ink = ink
        
    def print_page(self, text):
        ink_needed = len(text)
        if self.paper >= 1 and self.ink >= ink_needed:
            self.paper -= 1
            self.ink -= ink_needed
            print(f"Печать: {text}")
        else:
            print("Нет бумаги или краски!")
```

</details>

---

**4. Практика: «Снайперская винтовка»** Класс `SniperRifle`. Метод `reload(self)` дает 5 патронов. Метод `shoot(self)` проверяет патроны: если есть — стреляет ("Бах!"), если нет — "Щелк!".

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class SniperRifle:
    def reload(self):
        self.ammo = 5
        print("Винтовка заряжена!")
        
    def shoot(self):
        if hasattr(self, 'ammo') and self.ammo > 0:
            self.ammo -= 1
            print("Бах! 🎯")
        else:
            print("Щелк! Нужна перезарядка.")
```

</details>

---

## Тема 2: Магия создания — метод `__init__`

**Что такое __init__?**
Это специальный метод (конструктор), который Python запускает автоматически в тот самый момент, когда вы создаете объект (пишете robot = Robot()).

**Зачем он нужен?**

1. Настройка при рождении: Чтобы не вызывать методы setup() или build() вручную, мы передаем все важные данные сразу.

2. Обязательные данные: Если робот не может существовать без серийного номера, мы требуем его в __init__.

3. Значения по умолчанию: Мы можем сразу установить уровень здоровья в 100 или пустой список инвентаря.

**Важно:** __init__ всегда пишется с двумя нижними подчеркиваниями с каждой стороны. Это знак того, что метод «магический».

### Уровень 1: Начальный 

**1. Демо-задача: «Паспорт игрока»** Класс `PlayerProfile`. В `__init__(self, nickname, level)` задаются имя и уровень.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class PlayerProfile:
    def __init__(self, nickname, level):
        self.nickname = nickname
        self.level = level
        print(f"Создан игрок {self.nickname} ({self.level} уровень)")

player1 = PlayerProfile("Ninja", 10)
```

</details>

---

**2. Практика: «Автомобиль»** Класс `Car`. При создании (`__init__`) принимает `brand` и `color`. Скорость всегда 0 по умолчанию.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
        self.speed = 0
```

</details>

---

**3. Практика: «Собака»** Класс `Dog`. Принимает `name` и `breed`. Вызови внутри `__init__` метод `bark(self)`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed
        self.bark()
        
    def bark(self):
        print(f"Гав! Я {self.name}, порода: {self.breed}")
```

</details>

---

**4. Практика: «Ноутбук»** Класс `Laptop`. В `__init__` задается `model`, заряд батареи автоматически становится 100.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Laptop:
    def __init__(self, model):
        self.model = model
        self.battery = 100
```

</details>

---

### Тема 2: Уровень 2: Средний (Коллекции по умолчанию)

**5. Демо-задача: «Игровой инвентарь»** Класс `Inventory`. В `__init__(self, capacity)` задается вместимость и создается пустой список `self.items = []`. Напиши метод `add_item(self, item)`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Inventory:
    def __init__(self, capacity):
        self.capacity = capacity
        self.items = []
        
    def add_item(self, item):
        if len(self.items) < self.capacity:
            self.items.append(item)
            print(f"Предмет {item} добавлен!")
        else:
            print("Инвентарь полон!")
```

</details>

---

**6. Практика: «Магазин»** Класс `Shop`. В `__init__` задается название магазина и создается пустой словарь `self.products` (где ключ — товар, а значение — цена).

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Shop:
    def __init__(self, name):
        self.name = name
        self.products = {}
        
    def add_product(self, product_name, price):
        self.products[product_name] = price
        print(f"Товар {product_name} теперь в продаже за {price}.")
```

</details>

---

**7. Практика: «Чат-комната»** Класс `ChatRoom`. При создании задается `room_name`, пустой список `self.users` и пустой список `self.messages`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class ChatRoom:
    def __init__(self, room_name):
        self.room_name = room_name
        self.users = []
        self.messages = []
```

</details>

---

**8. Практика: «Робот-пылесос»** Класс `RobotVacuum`. Принимает `model`. Имеет атрибуты по умолчанию: `self.trash_collected = 0` и `self.is_cleaning = False`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class RobotVacuum:
    def __init__(self, model):
        self.model = model
        self.trash_collected = 0
        self.is_cleaning = False
```

</details>

---

### Тема 2: Уровень 3: Достаточный (Валидация при создании)

**9. Демо-задача: «Регистрация»** Класс `ServerAccount`. В `__init__(self, username, age)`. Если `age < 13`, атрибуту `self.is_restricted` присваивается `True`, иначе `False`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class ServerAccount:
    def __init__(self, username, age):
        self.username = username
        self.age = age
        if self.age < 13:
            self.is_restricted = True
            print("Аккаунт создан с ограничениями (детский).")
        else:
            self.is_restricted = False
            print("Полный доступ разрешен.")
```

</details>

---

**10. Практика: «Генератор паролей»** Класс `PasswordManager`. В `__init__` принимает пароль. Если пароль короче 8 символов, заменяет его на `"qwerty1234"`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class PasswordManager:
    def __init__(self, password):
        if len(password) < 8:
            print("Пароль слишком короткий! Установлен стандартный.")
            self.password = "qwerty1234"
        else:
            self.password = password
```

</details>

---

**11. Практика: «Боевой маг»** Класс `Mage`. Принимает `element`. Если это не "огонь", "вода" или "земля", по умолчанию ставится "обычная магия".

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Mage:
    def __init__(self, element):
        valid_elements = ["огонь", "вода", "земля"]
        if element in valid_elements:
            self.element = element
        else:
            self.element = "обычная магия"
```

</details>

---

**12. Практика: «Бронирование билета»** Класс `Ticket`. Принимает `place_number`. Если номер меньше 1 или больше 50, ставит место 0 и пишет ошибку.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Ticket:
    def __init__(self, place_number):
        if 1 <= place_number <= 50:
            self.place_number = place_number
        else:
            print("Ошибка: места с таким номером нет.")
            self.place_number = 0
```

</details>

---

## Тема 3: Секретные материалы — Public, Private, Protected
**Цель:** Изучить инкапсуляцию. Скрываем важные данные от прямого изменения, чтобы никто «не сломал» логику объекта.

**Что такое инкапсуляция?**
Это объединение данных и методов для работы с ними в одну «капсулу» (класс) и ограничение доступа к важным деталям.

**Зачем скрывать данные?**
Представь телевизор. У тебя есть кнопки (публичные методы), но ты не должен лазить внутри с паяльником (приватные атрибуты), иначе ты его сломаешь. В коде так же: мы скрываем данные, чтобы их нельзя было случайно испортить.

**Три уровня доступа в Python:**

Публичные (name): доступны всем. Можно читать и менять как угодно.

Защищенные (_name): начинаются с одного _. Это предупреждение для других программистов: «Пожалуйста, не меняй это напрямую, это для внутреннего использования».

Приватные (__name): начинаются с двух __. Python «прячет» их. Если попытаться обратиться к ним напрямую, программа выдаст ошибку. Доступ к ним обычно дают только через специальные методы (геттеры и сеттеры).

### Тема 3: Уровень 1: Начальный (Приватные атрибуты)

**1. Демо-задача: «Сейф»** Класс `Safe`. В `__init__` создается приватный атрибут `self.__code = "1234"`. Напиши метод `open_safe(self, try_code)`, который сравнивает коды.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Safe:
    def __init__(self):
        self.__code = "1234" # Приватный атрибут
        
    def open_safe(self, try_code):
        if try_code == self.__code:
            print("Сейф открыт! 💰")
        else:
            print("Неверный код!")
```

</details>

---

**2. Практика: «Дневник с секретом»** Класс `SecretDiary`. Текст хранится в `self.__text`. Прочитать его можно только через метод `read(self, password)`, если пароль верный.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class SecretDiary:
    def __init__(self, text, password):
        self.__text = text
        self.__password = password
        
    def read(self, password):
        if password == self.__password:
            return self.__text
        else:
            return "Доступ запрещен! ❌"
```

</details>

---

**3. Практика: «Пин-код телефона»** Класс `Phone`. Приватный `self.__pin`. Публичный метод `unlock(self, pin)` возвращает `True`, если пин совпал, и `False`, если нет.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Phone:
    def __init__(self, pin):
        self.__pin = pin
        
    def unlock(self, pin):
        return pin == self.__pin
```

</details>

---

**4. Практика: «Шпионский жучок»** Класс `BugDevice`. Частота `self.__frequency` задается в `__init__`. Создай метод `get_frequency(self)`, чтобы узнать её (но менять нельзя!).

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class BugDevice:
    def __init__(self, frequency):
        self.__frequency = frequency
        
    def get_frequency(self):
        return self.__frequency
```

</details>

---

### Тема 3: Уровень 2: Средний (Защищенные и внутренние методы)

**5. Демо-задача: «Роутер»** Класс `Router`. Публичный `model`, защищенный `_ip_address` и приватный `__admin_password`. Метод `connect` проверяет пароль перед выдачей IP.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Router:
    def __init__(self, model, ip_address, password):
        self.model = model
        self._ip_address = ip_address
        self.__admin_password = password
        
    def connect(self, password):
        if password == self.__admin_password:
            return f"Успех! IP адрес: {self._ip_address}"
        return "Ошибка: неверный пароль администратора."
```

</details>

---

**6. Практика: «Криптокошелек»** Класс `CryptoWallet`. Баланс публичный, ключ `__private_key` — приватный. Метод `send_money` вызывает внутренний метод `_sign_transaction`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class CryptoWallet:
    def __init__(self, balance, private_key):
        self.balance = balance
        self.__private_key = private_key
        
    def _sign_transaction(self):
        # Внутренний метод для подписи
        return f"Транзакция подписана кодом {self.__private_key[:4]}..."
        
    def send_money(self, amount):
        if self.balance >= amount:
            print(self._sign_transaction())
            self.balance -= amount
            print("Деньги отправлены!")
```

</details>

---

**7. Практика: «Мотор автомобиля»** Класс `Engine`. Публичный метод `start()`, который внутри вызывает приватный метод `__inject_fuel()`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Engine:
    def __inject_fuel(self):
        print("Впрыск топлива...")
        
    def start(self):
        self.__inject_fuel()
        print("Двигатель запущен!")
```

</details>

---

**8. Практика: «Банкомат»** Класс `ATM`. Приватный атрибут `__total_money`. Публичный метод `withdraw(self, amount)`, выдающий деньги только при наличии средств.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class ATM:
    def __init__(self, initial_amount):
        self.__total_money = initial_amount
        
    def withdraw(self, amount):
        if amount <= self.__total_money:
            self.__total_money -= amount
            print(f"Выдано {amount}. В банкомате осталось {self.__total_money}")
        else:
            print("Ошибка: недостаточно денег в банкомате.")
```

</details>

---

### Тема 3: Уровень 3: Достаточный (Геттеры и Сеттеры вручную)

**9. Демо-задача: «Игровой уровень»** Класс `GameAccount`. Приватный `__level` (1) и `__xp` (0). Метод `add_xp(xp)` повышает уровень за каждые 100 XP. Уровень нельзя менять напрямую.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class GameAccount:
    def __init__(self):
        self.__level = 1
        self.__xp = 0
        
    def get_level(self):
        return self.__level
        
    def add_xp(self, xp):
        self.__xp += xp
        while self.__xp >= 100:
            self.__xp -= 100
            self.__level += 1
            print(f"Поздравляем! Ваш уровень повышен до {self.__level}")
```

</details>

---

**10. Практика: «Ядерный реактор»** Класс `Reactor`. Приватная `__temperature`. Метод `increase_power` греет реактор. Если температура > 1000, вызывается приватный метод `__emergency_shutdown`.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Reactor:
    def __init__(self):
        self.__temperature = 0
        
    def __emergency_shutdown(self):
        self.__temperature = 0
        print("ОПАСНОСТЬ! Аварийное охлаждение активировано!")
        
    def increase_power(self, amount):
        self.__temperature += amount
        print(f"Текущая температура: {self.__temperature}")
        if self.__temperature > 1000:
            self.__emergency_shutdown()
```

</details>

---

**11. Практика: «Банковский счет»** Класс `BankAccount`. Приватный `__balance`. Методы `deposit` и `withdraw` должны менять баланс только при положительных суммах и проверке остатка.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class BankAccount:
    def __init__(self):
        self.__balance = 0
        
    def get_balance(self):
        return self.__balance
        
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            
    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
            return amount
        print("Недостаточно средств или неверная сумма.")
```

</details>

---

**12. Практика: «Умный градусник»** Класс `Sensor`. Приватная `__celsius`. Метод `set_temp` не дает ставить ниже -273. Метод `get_fahrenheit` возвращает температуру в Фаренгейтах.

<details markdown="1">
<summary>💡 Посмотреть решение</summary>

```python
class Sensor:
    def __init__(self):
        self.__celsius = 0
        
    def set_temp(self, value):
        if value >= -273:
            self.__celsius = value
        else:
            print("Ниже абсолютного нуля нельзя!")
            
    def get_fahrenheit(self):
        return (self.__celsius * 9/5) + 32
```

</details>

---
