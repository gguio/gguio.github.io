# Задачи по ООП на Python: основы



---

## Тема 1: Основы класса и магия `self`
**Цель:** Понять, что `self` — это способ объекта «обратиться к самому себе», чтобы запоминать свое состояние и изменять его. В этой теме мы **не используем** `__init__`.

### Уровень 1: Начальный (Простые переключатели)

**Демо-задача: «Умная лампочка»**
Создай класс `SmartBulb`. Напиши метод `turn_on(self)`, который создает атрибут `self.is_on = True`, и метод `turn_off(self)`, который делает `self.is_on = False`.

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

**Практика 1: «Кликер»**
Создай класс `Clicker`. Метод `start(self)` задает `self.score = 0`. Метод `click(self)` увеличивает `self.score` на 1.

<details>
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

**Практика 2: «Кот-тамагочи»**
Создай класс `Cat`. Метод `wake_up(self)` делает `self.is_hungry = True`. Метод `feed(self)` меняет `self.is_hungry` на `False`.

<details>
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

**Практика 3: «Музыкальный плеер»**
Создай класс `Player`. Метод `play(self)` задает `self.status = "playing"`, а `pause(self)` задает `self.status = "paused"`.

<details>
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

### Уровень 2: Средний (Взаимодействие атрибутов)

**Демо-задача: «Космический корабль»**
Класс `Spaceship`. Метод `refuel(self, amount)` добавляет топливо в `self.fuel` (изначально нужно задать 0). Метод `fly(self, distance)` тратит топливо (1 ед. на 10 км) и увеличивает `self.mileage`.

<details>
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

**Практика 1: «Копилка»**
Класс `PiggyBank`. Метод `set_empty(self)` делает `self.coins = 0`. Метод `add_coin(self, value)` добавляет монеты. Метод `break_bank(self)` возвращает все монеты и обнуляет счетчик.

<details>
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

**Практика 2: «Здоровье персонажа»**
Класс `Hero`. Метод `spawn(self)` дает `self.hp = 100`. Метод `take_damage(self, damage)` уменьшает ХП, а `heal(self, amount)` — увеличивает.

<details>
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

**Практика 3: «Кондиционер»**
Класс `AirConditioner`. Метод `turn_on(self)` задает `self.temp = 22`. Методы `warmer(self)` и `cooler(self)` меняют температуру на 1 градус.

<details>
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

### Уровень 3: Достаточный (Логика внутри методов)

**Демо-задача: «Кофемашина»**
Класс `CoffeeMachine`. Метод `fill(self, water, beans)` пополняет запасы. Метод `make_coffee(self)` проверяет: нужно 200 мл воды и 20 г зерен. Если хватает — варит кофе, если нет — выдает ошибку. Перед использованием вызови `setup()` для создания пустых запасов.

<details>
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

**Практика 1: «Продвинутый тамагочи»**
Доработай класс `Hero` (назовем его `AdvancedCat`). Вызови `spawn()`. ХП не может быть больше 100. Если при методе `take_damage` ХП падает ниже 0, кот падает в обморок (создается `self.is_fainted = True`).

<details>
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

**Практика 2: «Принтер»**
Класс `Printer`. Создай `setup(self, paper, ink)`. Метод `print_page(self, text)` считает символы в тексте (`len(text)`). Каждый символ тратит 1 ед. краски, печать — 1 лист бумаги. Добавь проверки ресурсов.

<details>
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

**Практика 3: «Снайперская винтовка»**
Класс `SniperRifle`. Метод `reload(self)` дает 5 патронов (`self.ammo = 5`). Метод `shoot(self)` проверяет патроны: если есть — стреляет ("Бах!") и тратит патрон, если нет — пишет "Щелк!".

<details>
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
**Цель:** Научиться задавать начальные характеристики объекта в момент его «рождения».

### Уровень 1: Начальный 

**Демо-задача: «Паспорт игрока»**
Класс `PlayerProfile`. В `__init__(self, nickname, level)` задаются имя и уровень. Создай объект: `player1 = PlayerProfile("Ninja", 10)`.

<details>
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

**Практика 1: «Автомобиль»**
Класс `Car`. При создании (`__init__`) принимает `brand` и `color`. Атрибут `speed` всегда равен 0 по умолчанию.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
        self.speed = 0
```
</details>

**Практика 2: «Собака»**
Класс `Dog`. Принимает `name` и `breed`. Выведи их на экран при создании, вызвав внутри `__init__` метод `bark(self)`.

<details>
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

**Практика 3: «Ноутбук»**
Класс `Laptop`. В `__init__` задается `model`, а заряд батареи `self.battery` автоматически устанавливается на 100.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class Laptop:
    def __init__(self, model):
        self.model = model
        self.battery = 100
```
</details>

### Уровень 2: Средний (Коллекции по умолчанию)

**Демо-задача: «Игровой инвентарь»**
Класс `Inventory`. В `__init__(self, capacity)` задается вместимость и создается пустой список `self.items = []`. Напиши `add_item(self, item)`.

<details>
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

**Практика 1: «Магазин»**
Класс `Shop`. В `__init__` задается название магазина и создается пустой словарь `self.products` (ключ - товар, значение - цена).

<details>
<summary>💡 Посмотреть решение</summary>

```python
class Shop:
    def __init__(self, name):
        self.name = name
        self.products = {}
        
    def add_product(self, product_name, price):
        self.products[product_name] = price
```
</details>

**Практика 2: «Чат-комната»**
Класс `ChatRoom`. При создании задается `room_name`, пустой список `self.users` и пустой список `self.messages`.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class ChatRoom:
    def __init__(self, room_name):
        self.room_name = room_name
        self.users = []
        self.messages = []
```
</details>

**Практика 3: «Робот-пылесос»**
Класс `RobotVacuum`. Принимает `model`. Имеет атрибуты по умолчанию: `self.trash_collected = 0` и `self.is_cleaning = False`.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class RobotVacuum:
    def __init__(self, model):
        self.model = model
        self.trash_collected = 0
        self.is_cleaning = False
```
</details>

### Уровень 3: Достаточный (Валидация при создании)

**Демо-задача: «Регистрация на сервере»**
Класс `ServerAccount`. В `__init__(self, username, age)`. Если `age < 13`, атрибуту `self.is_restricted` присваивается `True`, иначе `False`.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class ServerAccount:
    def __init__(self, username, age):
        self.username = username
        self.age = age
        if self.age < 13:
            self.is_restricted = True
        else:
            self.is_restricted = False
```
</details>

**Практика 1: «Генератор паролей»**
Класс `PasswordManager`. В `__init__` принимает пароль. Если пароль короче 8 символов, заменяет его на `"qwerty1234"` и выводит предупреждение.

<details>
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

**Практика 2: «Боевой маг»**
Класс `Mage`. Принимает `element`. Если это не "огонь", "вода" или "земля", по умолчанию ставится "обычная магия".

<details>
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

**Практика 3: «Бронирование билета»**
Класс `Ticket`. Принимает `place_number`. Если номер меньше 1 или больше 50, пишет ошибку и ставит место 0. Иначе сохраняет номер.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class Ticket:
    def __init__(self, place_number):
        if 1 <= place_number <= 50:
            self.place_number = place_number
        else:
            print("Ошибка: такого места не существует.")
            self.place_number = 0
```
</details>

---

## Тема 3: Секретные материалы — Public, Private, Protected
**Цель:** Изучить инкапсуляцию. Скрываем важные данные от взлома.

### Уровень 1: Начальный 

**Демо-задача: «Сейф»**
Класс `Safe`. В `__init__` создается приватный атрибут `self.__code = "1234"`. Напиши публичный метод `open_safe(self, try_code)`, который сравнивает коды.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class Safe:
    def __init__(self):
        self.__code = "1234"
        
    def open_safe(self, try_code):
        if try_code == self.__code:
            print("Сейф открыт!")
        else:
            print("Неверный пароль!")
```
</details>

**Практика 1: «Дневник с секретом»**
Класс `SecretDiary`. Текст хранится в `self.__text` (задай при создании). Прочитать его можно только через метод `read(self, password)`.

<details>
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
            return "Доступ запрещен!"
```
</details>

**Практика 2: «Пин-код телефона»**
Класс `Phone`. Приватный `self.__pin`. Публичный `unlock(self, pin)` возвращает `True`, если пин совпал, и `False`, если нет.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class Phone:
    def __init__(self, pin):
        self.__pin = pin
        
    def unlock(self, pin):
        return pin == self.__pin
```
</details>

**Практика 3: «Шпионский жучок»**
Класс `BugDevice`. Частота `self.__frequency` задается в `__init__`. Изменить ее нельзя, можно получить через `get_frequency(self)`.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class BugDevice:
    def __init__(self, frequency):
        self.__frequency = frequency
        
    def get_frequency(self):
        return self.__frequency
```
</details>

### Уровень 2: Средний (Внутренние методы)

**Демо-задача: «Сетевой роутер»**
Класс `Router`. Public `model`, protected `_ip_address` и private `__admin_password`. Создай `connect(self, password)`, проверяющий пароль перед выдачей IP.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class Router:
    def __init__(self, model, ip_address, password):
        self.model = model
        self._ip_address = ip_address
        self.__admin_password = password
        
    def connect(self, password):
        if password == self.__admin_password:
            return f"Подключено! IP: {self._ip_address}"
        return "Неверный пароль сети."
```
</details>

**Практика 1: «Криптокошелек»**
Класс `CryptoWallet`. Баланс public, ключ `__private_key`. Напиши защищенный метод `_sign_transaction()`, используемый только внутри `send_money(self)`.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class CryptoWallet:
    def __init__(self, balance, private_key):
        self.balance = balance
        self.__private_key = private_key
        
    def _sign_transaction(self):
        return f"Подписано ключом {self.__private_key[-4:]}" # имитация подписи
        
    def send_money(self, amount):
        if self.balance >= amount:
            signature = self._sign_transaction()
            self.balance -= amount
            print(f"Перевод успешен. {signature}")
```
</details>

**Практика 2: «Мотор автомобиля»**
Класс `Engine`. Публичный `start()`. Внутри он вызывает приватный `__inject_fuel()`, который пользователь не должен запускать вручную.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class Engine:
    def __inject_fuel(self):
        print("Впрыск топлива произведен...")
        
    def start(self):
        self.__inject_fuel()
        print("Двигатель запущен! Врум-врум!")
```
</details>

**Практика 3: «Банкомат»**
Класс `ATM`. Приватный `__total_money`. Публичный `withdraw(self, amount)`, который выдает деньги, только если внутри хватает купюр.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class ATM:
    def __init__(self, total_money):
        self.__total_money = total_money
        
    def withdraw(self, amount):
        if amount <= self.__total_money:
            self.__total_money -= amount
            print(f"Выдано: {amount}")
        else:
            print("В банкомате недостаточно средств!")
```
</details>

### Уровень 3: Достаточный (Безопасный доступ)

**Демо-задача: «Игровой аккаунт»**
Класс `GameAccount`. Приватный `__level` (изначально 1). Методы `get_level(self)` и `add_xp(self, xp)`. Уровень нельзя изменить напрямую, он растет (на 1 за каждые 100 XP), если вызван `add_xp`.

<details>
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
        # Если накопилось 100 опыта, повышаем уровень
        while self.__xp >= 100:
            self.__xp -= 100
            self.__level += 1
            print(f"Новый уровень! Теперь вы {self.__level} уровня.")
```
</details>

**Практика 1: «Ядерный реактор»**
Класс `Reactor`. Приватная `__temperature` (изначально 0). Методы `get_temp()` и `increase_power(amount)`. Если `__temperature` > 1000, вызывается `__emergency_shutdown()`.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class Reactor:
    def __init__(self):
        self.__temperature = 0
        
    def get_temp(self):
        return self.__temperature
        
    def __emergency_shutdown(self):
        self.__temperature = 0
        print("ВНИМАНИЕ! Аварийная остановка реактора!")
        
    def increase_power(self, amount):
        self.__temperature += amount
        if self.__temperature > 1000:
            self.__emergency_shutdown()
```
</details>

**Практика 2: «Банковский счет»**
Класс `BankAccount`. Приватный `__balance`. Метод `deposit(self, amount)` кладет деньги (> 0). `withdraw(self, amount)` — снимает (если сумма меньше баланса).

<details>
<summary>💡 Посмотреть решение</summary>

```python
class BankAccount:
    def __init__(self):
        self.__balance = 0
        
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            
    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
            return amount
        return "Ошибка операции."
```
</details>

**Практика 3: «Температурный датчик»**
Класс `Sensor`. Приватный `__celsius`. Публичные методы: `set_temperature(self, value)` не принимает ниже -273, и `get_fahrenheit(self)` возвращает в Фаренгейтах `(C * 9/5) + 32`.

<details>
<summary>💡 Посмотреть решение</summary>

```python
class Sensor:
    def __init__(self):
        self.__celsius = 0
        
    def set_temperature(self, value):
        if value >= -273:
            self.__celsius = value
        else:
            print("Ошибка: температура ниже абсолютного нуля!")
            
    def get_fahrenheit(self):
        return (self.__celsius * 9/5) + 32
```
</details>
