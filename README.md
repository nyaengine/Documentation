<p align="left">
  <img width="100" alt="Nya Engine logo" src="docs/NyaEngine.jpg">
</p>

# Nya Engine Documentation

**Nya Engine** is a community-driven 2D game engine built with [LÖVE2D](https://love2d.org/), designed to be lightweight, easy to use, and *kawaii* 🌸. Nya Engine includes an integrated IDE, visual scripting, Lua coding, object and scene management, UI customization, and more — all to empower game developers to create amazing interactive 2D games quickly and easily.

## Table of Contents

- [Examples](#examples)
- [Syntax](#syntax)

## Examples

Nya Engine uses the default LÖVE syntax and some additional custom libraries.

- # ButtonLibrary
It's a library for easy creation of buttons.

To create a button use ButtonLibrary:new(x, y, width, height, text, function, image(optional))

for example: 

```lua
    function love.load()
      Button = ButtonLibrary:new(0, 100, 500, 100, "Test", function()
        print("test")
    end)
```

You can also change the background transparency by using this code:

```lua
    Button:IsVisibleBG(false) -- true or false
```

or 

``` lua
    Button:SetTransparency(1) -- transparency value
```

If you want to change the button position while the game is running you can do:

```lua
    function love.draw()
        Button:setPosition(x, y)
    end
```

This is the whole example for creating buttons:

```lua
    local ButtonPressed = false

    function love.load()
      Button = ButtonLibrary:new(0, 100, 500, 100, "Test", function()
        ButtonPressed = not ButtonPressed
    end)

    function love.update(dt)
        local mouseX, mouseY = love.mouse.getPosition()

        Button:update(mouseX, mouseY)
    end

    function love.draw()
        Button:draw()

        if ButtonPressed == true then
            Button:setPosition(100, 100)
        else
            Button:setPosition(0, 100)
        end
    end

    function love.mousepressed(x, y, button, istouch, presses)
        Button:mousepressed(x, y, button)
    end
```

This code makes it so when the button is pressed then it changes the position.

- # ObjectLibrary

This library is responsible for all the objects in the game. 
To create an Object use:
```lua 
    local Object = ObjectLibrary:new(150, 100, 50, 50) -- x, y, width, height, imagePath
```

the ObjectLibrary has a Force syntax which allows you to move the object.

```lua
    local Object = ObjectLibrary:new(150, 100, 50, 50) -- x, y, width, height, imagePath

    function love.update(dt)
        if love.keyboard.isDown("w") then
            Object:applyForce(100, 0) -- moves the object's x position by 100
        end
    end

    function love.draw()
        Object:draw()
    end
```

the ObjectLibrary also has built-in physics.

```lua
    local Object = ObjectLibrary:new(150, 100, 50, 50) -- x, y, width, height, imagePath

    function love.update(dt)
        Object:update(dt)

        if love.keyboard.isDown("w") then
            Object:applyForce(100, 0) -- moves the object's x position by 100
        end
    end

    function love.draw()
        Object:draw()
    end
```

you can make the objects be clickable and you can add collisions to objects.

```lua
    local Object = ObjectLibrary:new(150, 100, 50, 50) -- x, y, width, height, imagePath
    local Floor = ObjectLibrary:new(300, 100, 100, 20) -- Floor to test the collision

    function love.load()
        Floor.gravity = 0 -- disable the gravity for the floor
    end

    function love.update(dt)
        -- enables object physics
        Object:update(dt)

        if love.keyboard.isDown("w") then
            Object:applyForce(100, 0) -- moves the object's x position by 100
        end
    end

    function love.draw()
        Object:draw()

        Object:resolveCollision(Floor) -- Check if the Object is colliding with the floor

        -- If Object is colliding, print text
        if Object:checkCollision(Floor) then
            print("Object is colliding with the floor")
        end
    end

    -- check if object is pressed
    function love.mousepressed(x, y, button, istouch, presses)
        if Object:isClicked(x, y) then
            print("Object Pressed")
        end
    end
```

## Syntax
- [ObjectLibrary](#objectlibrary)
- # ButtonLibrary
- # love
- # function
- # print
- # for
