# Experimental Assignment 3: MongoDB
## Experiment 1: CRUD Operations
These tasks were conducted in powershell, as running mongo.exe did not support any copy and paste actions. 

### 1. Inserting and showing data
![image](https://user-images.githubusercontent.com/54100104/191807080-c60e7813-0db5-4eed-a408-5821d2cb6b62.png)

### 2. Querying Data
#### 2.1 Inserting data
![image](https://user-images.githubusercontent.com/54100104/191809158-3485b467-5191-4a11-b212-f364ba1df6bb.png)
#### 2.2 Finding all items in inventory with status = A, or B
Achieved using following command:
```
db.inventory.find( { status: { $in: [ "A", "D" ] } } )
```
![image](https://user-images.githubusercontent.com/54100104/191809475-b3560d6f-2532-446d-91a3-bcb0a9731d7f.png)


