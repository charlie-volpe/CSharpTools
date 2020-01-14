# JSON

## Dependencies
- C# 7.1+

## Why another JSON implementation?
I don't enjoy using the DataContracts implementation for JSON in C#. I wanted a JSON implementation
in C# that felt a  bit more like the python json implementation. I made sure to implement the classes
with indexers and implicit casting, which I believe, does the job.

## Usage
There are examples in the code but I will include a small section here:
```c#
// String can be read from file but for this example, I am just showing the full string.
string people = "[{\"name\": \"Smith\"}, {\"name\": \"Doe\"}]";

JSON json0 = new JSON(people); // Can deserialize on construction
JSONObject firstPerson = json0[0]; // Uses implicit cast from JSONElement to JSONObject

JSON json1 = new JSON();
json1.Deserialize(people); // Can deserialize later on as well
JSONObject secondPerson = json1[1]; // Could have just as easily been json0[1]

Console.WriteLine("Full: " + json0.Serialize());
// Full: [{"name":"Smith"},{"name":"Doe"}]
Console.WriteLine("First person: " + firstPerson.Serialize());
// First person: {"name":"Smith"}
Console.WriteLine("First person's name: " + firstPerson["name"]); // Uses implicit cast from JSONElement to string
// First person's name: Smith

JSONArray arrays = JSONElement.Deserialize("[[10.0, 1.5, 2.3],[0.0,3.2]]");
JSONArray randomArray = arrays[0];
// To get a double value in Console.WriteLine cast it to double from JSONElement
Console.WriteLine("Some Double: " + (double)randomArray[1]); // Some Double: 1.5
// If you don't it will try to cast it as a string and will return null
Console.WriteLine("Some Double: " + randomArray[1]); // Some Double: 
// This is true, as well, of other types

Console.WriteLine("Second person: " + secondPerson.Serialize());
// Second person: {"name":"Doe"}
Console.WriteLine("Second person's name: " + secondPerson["name"]);
// Second person's name: Doe

File.WriteAllText("people.json", json0.Serialize());
```

## Potential Next Steps
### Prettified JSON
Currently this only serializes as a Minified JSON string; in an update it could potentially also be Serialized
to a prettified version with variable tabs as spaces. As there are tools that do that do that work already,
I decided not to write that into the initial version so that I could release it sooner.

## Conclusion
I will be using this in my projects from here on, instead of the DataContracts implementation that comes
with C#'s System libraries. Hopefully you find it useful in your projects as well.
