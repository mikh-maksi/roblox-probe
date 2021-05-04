# Пробне заняття напрямок "Розробка ігор"
## При запуску RobloxStudio обиаємо шаблон "Classic Beseplate"
<img src = "img/RobloxStudio1.jpg">

## Відкривається основне робоче поле
<img src = "img/RobloxStudio2.jpg">

## Обираємо пункт Part і підпункт Block
<img src = "img/RobloxStudio3.jpg">

## Буде створено прямокутний блок 
<img src = "img/RobloxStudio4.jpg">

## В блоці меню Explorer клікнемо на плюсик 
<img src = "img/RobloxStudio5.jpg">

## І оберемо пункт Script
<img src = "img/script.jpg">

## Нажимаємо на створений елемент Script та видалимо код print("Hello world!")

<img src = "img/RobloxStudio7.jpg">

## Вставимо код та запустимо код

```lua
element = script.Parent
element.BrickColor = BrickColor.new("Dark blue")
```
<img src = "img/RobloxStudio8.jpg">

## Побачемо результат: блок після запуску стає темно синього (dark blue) кольору.

<img src = "img/RobloxStudio9.jpg">

## До блоку Part додамо ефект вогню (fire)
Для цього натиснемо "+" біля назви блоку (Part) 
<img src = "img/RobloxStudio10.jpg">

Та за допомогою пошуку знайдемо ефект вогню (fire)
<img src = "img/RobloxStudio11.jpg">

Вогонь, як властивість, з'яветься на обраному блоці
<img src = "img/RobloxStudio12.jpg">

## Додамо код, що буде динамічно змінювати ефект
```lua
local element = script.Parent

local function stopFire()
	element.Fire:Destroy()
	local spark = Instance.new("ParticleEmitter")
	spark.Parent = element
end

wait(10)
stopFire()
```
<img src = "img/RobloxStudio13.jpg">
Даний код за 10 секунд після запуску змінить ефект блоку з вогню (fire) на "випромінювач частинок" (ParticleEmitter)
<img src = "img/change_property.gif">  

## Додамо реалізацію зникнення блоку
Для цього створемо функцію destroyBlock і викличемо її через 5 секунд після зникнення ефекту "випромінювача частинок"
```lua
local element = script.Parent

local function stopFire()
	element.Fire:Destroy()
	local spark = Instance.new("ParticleEmitter")
	spark.Parent = element
end
local function destroyBlock()
	element:Destroy()
end


wait(10)
stopFire()
wait(5)
destroyBlock()
```  
<img src = "img/RobloxStudio14.jpg">
отримаємо результат: 
<img src = "img/effects.gif">

## Додамо особилвість блоку - циклічну зміну кольору.
```lua
while true do
	element.BrickColor = BrickColor.new(0.9,0.6,0.2)
	wait(3)
	element.BrickColor = BrickColor.new(0.2,0.6,0.2)
	wait(3)
end

```
<img src = "img/RobloxStudio15.jpg">
Отримаємо результат  
<img src = "img/change_color.gif">

## Додамо функціональність балів
біля пункту Workspace натиснемо "+"
<img src = "img/RobloxStudio16.jpg">  
Оберемо пункт Script
<img src = "img/RobloxStudio17.jpg">

В новоствореному блоці Script видалемо код `print("Hello world!")` (він там є за замовчуванням). І додамо код формвання балів:

```lua
local function onPlayerJoin(player)
	local leaderstats = Instance.new("Folder")
	leaderstats.Name = "leaderstats"
	leaderstats.Parent = player

	local points = Instance.new("IntValue")
	points.Name = "Points"
	points.Value = 0
	points.Parent = leaderstats

end

game.Players.PlayerAdded:Connect(onPlayerJoin)
```
<img src = "img/RobloxStudio18.jpg">
## Додамо новий блок
Оберемо кнопку Block (1) на панелі інструментів. У випадаючому списку оберемо Part (2). Буде створено новий блок (3)

<img src = "img/RobloxStudio19.jpg">
В блоці Explorer біля пункту меню Part, що відповідає створеном блоку натиснемо елемент +
<img src = "img/RobloxStudio20.jpg">
У меню, що з'явиться оберемо пункт Script

<img src = "img/RobloxStudio21.jpg">

Замість того коду, що є в цьому блоку за замовчуванням (`print("Hello world!")`) додамо код отримання балів в залежності від кольору блоку.
```lua
local pointPart = script.Parent

local blue = Color3.fromRGB(0, 0, 255)
local green = Color3.fromRGB(0, 255, 0)
local red = Color3.fromRGB(255 ,0, 0)

local smallPoints = 10
local largePoints = 50
local losePoints = 100

local Players = game:GetService("Players")

local function givePoints(player)
	local currentColor = pointPart.Color

	local playerStats = player:WaitForChild("leaderstats")
	local playerPoints = playerStats:WaitForChild("Points")

	if currentColor == blue then
		playerPoints.Value = playerPoints.Value + smallPoints
	elseif currentColor == green then
		playerPoints.Value = playerPoints.Value + largePoints
	else
		playerPoints.Value = playerPoints.Value - losePoints
	end

	pointPart:Destroy()

	local playerCharacter = player.Character
	local particle = Instance.new("ParticleEmitter")
	particle.Color = ColorSequence.new(currentColor)
	particle.Parent = playerCharacter:WaitForChild("Head")
	wait(1)
	particle:Destroy()
end

local function partTouched(otherPart)
	local player = game.Players:GetPlayerFromCharacter(otherPart.Parent)

	if player then
		givePoints(player)
	end
end

pointPart.Touched:Connect(partTouched)

while true do
	pointPart.Color = blue
	wait(4)
	pointPart.Color = green
	wait(3)
	pointPart.Color = red
	wait(2)
end
```
<img src = "img/RobloxStudio22.jpg">
Здублюйте блок (нажав на нього правою клавішею миші та обрав пункт Duplicate)
<img src = "img/RobloxStudio23.jpg">
перемістість здубльований блок 
<img src = "img/duplicate.gif">
Повторіть три рази.

## Запустіть код для отримання результату 
<img src = "img/result.gif">
