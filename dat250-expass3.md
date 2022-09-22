# Experimental Assignment 3: MongoDB

## Validation of installation package
![image](https://user-images.githubusercontent.com/54100104/191832606-7cf506b7-eead-4283-8c30-629fdc39a8fd.png)

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

---
## Experiment 2: Aggregation

### 2.1 Return the Total Price Per Customer
Before Map-Reduce
![image](https://user-images.githubusercontent.com/54100104/191822989-1dc6cba7-6fba-4e1e-bc4e-02d1a47ce402.png)
After Map-Reduce
![image](https://user-images.githubusercontent.com/54100104/191822707-fcc22cd8-e3dd-4c70-85b8-55b4fcec7916.png)

### 2.2 Calculate Order and Total Quantity with Average Quantity Per Item
After Map-Reduce
![image](https://user-images.githubusercontent.com/54100104/191823485-86bb1f7b-ef25-4903-8d70-a25493f74848.png)

### 2.3 Custom Operation: Order dates by total sales
Map Function:
```js
var mapFunctionSalesByDate = function() {
   emit(this.ord_date, this.price);
};
```
Reduce Function:
```js
var reduceFunctionSalesByDate = function(date, price) {
   return Array.sum(price);
};
```
Perform Map-Reduce on all documents
```js
db.orders.mapReduce(
   mapFunctionSalesByDate,
   reduceFunctionSalesByDate,
   { out: "map_reduce_custom" }
)
```
Query Results
```
db.map_reduce_custom.find().sort( { value: -1 } )
```
Final Result:   
![image](https://user-images.githubusercontent.com/54100104/191828924-3222bd72-7cfd-45c1-bc14-05d39caeaed6.png)

The operation above could be very useful for analytics purposes to see days with high sales values. Perhaps an employee deserves a raise, or does he deserve the boot?
