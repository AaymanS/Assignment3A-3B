-----------------------------------------------------------------------------------------
--
-- Created by: Aayman Shameem 
-- Created on: Mar 04 2018
--
-- This code will calculate the cost of the pizza and the tax(HST)
-----------------------------------------------------------------------------------------
display.setDefault ( "background", 0.10, 0, 0.90)

local HST = 1.13

-- display for input text field
local pizzaSizeInputDisplay = display.newText( "Size of pizza(1 or 2):", display.contentCenterX - 100, display.contentCenterY - 120, native.systemFont, 30 )
-- input text field
local pizzaSizeInputTextField = native.newTextField( display.contentCenterX + 120, display.contentCenterY - 120, 150, 30)
pizzaSizeInputTextField.id = "The size of the pizza"


-- displaying the cost of large pizza
local largePizzaDisplay = display.newText( "1. Large: $6.00 ", display.contentCenterX - 120, display.contentCenterY - 90, native.systemFont, 20 )
largePizzaDisplay.id = "large size cost"

-- displaying the cost of extra large pizza
local extraLargePizzaDisplay = display.newText( "2. Extra Large: $10.00 ", display.contentCenterX - 139, display.contentCenterY - 70, native.systemFont, 20 )
extraLargePizzaDisplay.id = "extra large cost"



-- # of toppings
local toppingInputDisplay = display.newText( "Number of toppings:", display.contentCenterX - 100, display.contentCenterY - 30, native.systemFont, 30)
-- input text field for # of toppings
local toppingInputTextField = native.newTextField(display.contentCenterX + 130, display.contentCenterY - 30, 150, 30)
toppingInputTextField.id = "the number of toppings"


-- displaying the cost of one topping
local oneToppingDisplay = display.newText( "One topping: $1.00 ", display.contentCenterX - 120, display.contentCenterY, native.systemFont, 20 )
oneToppingDisplay.id = "cost of one topping"

-- displaying the cost of two toppings
local twoToppingDisplay = display.newText( "Two toppings: $1.75 ", display.contentCenterX - 124, display.contentCenterY + 20 , native.systemFont, 20 )
twoToppingDisplay.id = "cost of two toppings"

-- displaying the cost of three toppings
local threeToppingDisplay = display.newText( "Three toppings: $2.50 ", display.contentCenterX - 132, display.contentCenterY + 40, native.systemFont, 20 )
threeToppingDisplay.id = "cost of three toppings"

-- displaying the cost of four toppings
local fourToppingDisplay = display.newText( "Four Toppings: $3.35 ", display.contentCenterX - 128, display.contentCenterY + 60, native.systemFont, 20 )
fourToppingDisplay.id = "cost of four toppings"


-- button
local calculateButton = display.newImageRect( "./assets/sprites/enterButton.png", 150, 75 )
calculateButton.x = display.contentCenterX + 100
calculateButton.y = display.contentCenterY + 40 
calculateButton.id = "calculate button"

local finalPrice = display.newText( "Final Price with tax: $ ", display.contentCenterX - 100, display.contentCenterY + 120, native.systemFont, 30)

-- making sure the variables are numbers
local sizeCost = 0 
local toppingCost = 0


-- this function will calculate the price of the pizza with 
local function Button ( event ) 

	-- clears the previous price after pressing button 
	local clear1 = display.newRect(display.contentCenterX + 100, display.contentCenterY + 110, 100, 60)
 	clear1: setFillColor(0.1, 0, 0.9)

 	local clear2 = display.newRect(display.contentCenterX + 100, display.contentCenterY + 105, 100, 60)
 	clear2 : setFillColor(0.1, 0, 0.9)

 	local pizzaSize = tonumber(pizzaSizeInputTextField.text)
 	if pizzaSize == nil then
 		local errorMessage1 = display.newText( "ERROR, SIZE MUST BE 1 OR 2", display.contentCenterX + 100, display.contentCenterY + 100, native.systemFont, 20 )
 		
 		return false
 	elseif pizzaSize ~= 1  and pizzaSize ~= 2  then
 		local errorMessage1 = display.newText( "ERROR, SIZE MUST BE 1 OR 2", display.contentCenterX + 100, display.contentCenterY + 100, native.systemFont, 20  )
 		return false
 	end

	if pizzaSize == 1 then
		sizeCost = 6
	elseif pizzaSize == 2 then
		sizeCost = 10
	end

	local numberOfToppings = tonumber(toppingInputTextField.text)
 	if numberOfToppings == nil then
 		local errorMessage2 = display.newText( "ERROR, # OF TOPPINGS MUST BE BETWEEN 1 TO 4", display.contentCenterX + 10, display.contentCenterY + 100, native.systemFont, 20 )
 		return false
 	end
 	-- this checks for values between 1 and 4
 	if 1 > numberOfToppings or numberOfToppings > 4 then 
 		local errorMessage2 = display.newText( "ERROR, # OF TOPPINGS MUST BE BETWEEN 1 TO 4", display.contentCenterX + 110, display.contentCenterY + 110, native.systemFont, 20)
 		return false
 	end

 	if numberOfToppings == nil then
 		toppingCost = 0
 		local clear3 = display.newRect(display.contentCenterX, display.contentCenterY + 110, 100, 60)
 		clear3 : setFillColor(0.1, 0, 0.9)
 		local errorMessage2 = display.newText( "ERROR, # OF TOPPINGS MUST BE BETWEEN 1 TO 4", display.contentCenterX , display.contentCenterY + 110, native.systemFont, 20)
		end

	if numberOfToppings == 1 then
		toppingCost = 1

		elseif numberOfToppings == 2 then
			toppingCost = 1.75

			elseif numberOfToppings == 3 then
				toppingCost = 2.50

				elseif numberOfToppings == 4 then
					toppingCost = 3.35
	end

	if pizzaSize == nil and numberOfToppings == nil then
		finalPrice = 0
	end

	-- calculation
    local finalPrice = (sizeCost + toppingCost) * HST

    -- displaying calc with correct format
 	local finalPriceDisplay = display.newText( string.format( "%6.2f", finalPrice ), display.contentCenterX + 100, display.contentCenterY + 120, native.systemFont, 30 )


end

calculateButton:addEventListener( "touch", Button )
