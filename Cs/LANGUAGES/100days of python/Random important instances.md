
# How will you make a code loop?
`real = "y"
`while real == "y":
`print("hello")
`real = input("do you wish to continue? y/n")`
Now here the variable *real* will decide if our code will continue or not
in the start we assign a **true** value to it 
but then later on in the last step we ask the user again to confirm.
if the user assigns a **false** value then the code will stop else continue 

```  
while True:
    # --- Your main program goes here ---
    print("Running the program...")
    
    # --- The exit check ---
    choice = input("Run again? (y/n): ").strip().lower()
    
    if choice != 'y':
        print("Exiting.")
        break  # This instantly kills the while loop
```
now this will work to loop through a code multiple times instead of my method, which defines a variable in the start!

---
## To end a function/code early, like an exception
We can use *return* key to end the function.
as *return* key tells the code its the end of function thus bypassing any other lines of code
hence we can use it to catch exceptions


---
# blackjack
first i get 2 number from the list and a current score of mine 
then computer gets 2 number out of which 1 is displayed
	if my score is < 21 
		ask for another card(number from list)
		add that to my score 
	if my score is = 21 
		i win alr
	continue pulling till i make 21 or go overit 
	continue giving computer cards till either i go over 21 or stop pulling cards
	when i stop pulling cards 
	compare my value and computer value 
		whoever is closest to 21 without going over it wins 
		if its draw then restart the game
4 ending 
i win
i lose 
blackjack
draw