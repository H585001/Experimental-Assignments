# Experimental Assignment 4

## Link to Repository
https://github.com/H585001/dat250-sparkjava-counter

## Issues
I encountered a couple problems with the Java program. I struggled to get the ID added to the post requests. I did not realize that Gson did not use the constructors.
Since i have 4 oblig this week i couldnt finish by friday, but it is fixed now!

## Rest API for TODO Items
### GET Mappings
```java
get("/todos", (req, res) -> {
			if (todos.size() == 1)
				return new Gson().toJson(todos.get(0));
			else return new Gson().toJson(todos);
			});
		
get("/todos/:id", (req, res) -> {
	try {
		Long id = Long.parseLong(req.params(":id"));

		for (int i = 0; i < todos.size(); i++) {
			if (todos.get(i).getId() == id) {
				return new Gson().toJson(todos.get(i));
			}
		}
		return String.format("Todo with the id \"%s\" not found!", req.params(":id"));
				
	} catch (NumberFormatException e) {
		return String.format("The id \"%s\" is not a number!", req.params(":id"));
	}
});
```
### POST Mapping
```java
post("/todos", (req, res) -> {
	Todo todo = new Gson().fromJson(req.body(), Todo.class);
	todo.setId(Long.valueOf(todos.size()));
	todos.add(todo);
	return todo.toJson();
});
```
### PUT Mapping
```java
put("/todos/:id", (req, res) -> {

	try {
		Long id = Long.parseLong(req.params(":id"));

		for (int i = 0; i < todos.size(); i++) {
			if (todos.get(i).getId() == id) {
				Todo todo = new Gson().fromJson(req.body(), Todo.class);
				todo.setId(id);
				todos.set(i, todo);
				return todos.get(i).toJson();					}
			}
		}
		return null;
		} catch (NumberFormatException e) {
			return String.format("The id \"%s\" is not a number!", req.params(":id"));
		}
	});
```
### DELETE Mapping
```java
delete("/todos/:id", (req, res) -> {
	try {
		Long id = Long.parseLong(req.params(":id"));
		for (int i = 0; i < todos.size(); i++) {
			if (todos.get(i).getId() == id) {
				todos.remove(i);
				return true;
			}
		}
		return String.format("Todo with the id \"%s\" not found!", req.params(":id"));
		} catch (NumberFormatException e) {
			return String.format("The id \"%s\" is not a number!", req.params(":id"));
		}
	});
```
