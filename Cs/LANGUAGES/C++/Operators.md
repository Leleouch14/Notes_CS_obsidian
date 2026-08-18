Increment: increases the value of variable by 1 
`counter = 10;`
`counter++;` now the value of the counter is 11

1. position of *++* defines when the increment function will take place 
	`cout << counter;`----> 10
	`result = counter++;` 10
	`cout << result;`---->10
	`cout<< counter;` ----> 11
		result = counter---> counter++ ---> counter+1
	----------------------------
	`cout << counter;` ----> 10
	`result = ++counter;`
	`cout << result;` -----> 11
	`cout << counter;` ---> 11
		here result = counter +1 -----> counter = counter + 1
	
	*++* before the variable will be added to the new variable and *++* after the variable will not be added to the new variable 

Never use two increment statements in same line

---
