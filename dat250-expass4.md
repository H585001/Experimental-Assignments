# Experimental Assignment 4

## Issues
I encountered a couple problems with the Java program. I struggled to get the ID added to the post requests. For some reason it didnt seem like it worked in the constructor as imagined.
Since i have 4 oblig this week i couldnt finish by friday, but it is fixed now!

## Rest API for TODO Items
### Get Requests
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
