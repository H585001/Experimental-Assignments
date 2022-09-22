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

### 3. Updating documents
The following commands updates the size.uom field, and status
```
db.inventory.updateMany(
   { "qty": { $lt: 50 } },
   {
     $set: { "size.uom": "in", status: "P" },
     $currentDate: { lastModified: true }
   }
)
```
By showing all items, we see that all items with qty < 50 have size.oum = in
![image](https://user-images.githubusercontent.com/54100104/191811185-fe302832-b74b-4286-b661-7452ad56ac16.png)

### 4. Deleting documents
The following command deletes all items with status = A
```
db.inventory.deleteMany({ status : "A" })
```
We get returned amount of items deleted
![image](https://user-images.githubusercontent.com/54100104/191811521-906be6b9-b159-4db2-8a5d-1e60ccd6f7d4.png)

When inspecting we see that there are no more items with status = A
![image](https://user-images.githubusercontent.com/54100104/191811801-b0b73d0b-3b17-4594-90d3-5f013b9203ac.png)

### 5. Bulk-write operations
Writing the following command results in multiple operations being executed.
![image](https://user-images.githubusercontent.com/54100104/191813635-0ff67513-de61-481a-b6c4-ab8528466503.png)   
Since the optional order variable is not set to false, the operations are executed in order.   
The result is the following:   
![image](https://user-images.githubusercontent.com/54100104/191813980-c6635133-df35-4b8f-a036-c0f433de535c.png)

## Experiment 2: Aggregation


