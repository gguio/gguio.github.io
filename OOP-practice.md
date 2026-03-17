# Задачи по ООП на Python: основы

---

## Тема 1: Основы класса и магия `self`
**Цель:** Понять, что `self` — это способ объекта «обратиться к самому себе», чтобы запоминать свое состояние и изменять его. В этой теме мы **не используем** `__init__`.

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

*(Далее по аналогии добавлены разделители и исправлены пустые строки)*

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

*(Остальные темы оформляются в том же стиле)*
