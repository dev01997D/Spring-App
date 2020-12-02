# Spring-App

## Method 
```
public class DemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}

	@GetMapping("/hello")
	public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
		return String.format("Hello %s!", name);
	}
}
```
### Output using curl request
```
curl http://localhost:8080/hellocontroller/home
Hello World!!
curl http://localhost:8080/hellocontroller -w "\n"
Hello World!!
```
## Method
```
@RestController
@RequestMapping("/hellocontroller")
public class HelloWorldController {
	@RequestMapping(value = { "", "/", "/home" })
	public String sayHello() {
		return "Hello World!!";
	}

	@RequestMapping(value = { "/query" }, method = RequestMethod.GET)
	public String sayHello(@RequestParam(value = "fName") String fName, @RequestParam(value = "lName") String lName) {
		return "Hello " + fName + " " + lName + "!!";
	}
	
	@GetMapping("/param/{name}")
	public String sayHelloParam(@PathVariable String name) {
		return "Hello " + name + "!";
	}
}
```
### Output
```
curl -X GET "http://localhost:8080/hellocontroller/query/?name=Dev" -w "\n"
Hello Dev!!
```
```
curl -X GET "http://localhost:8080/hellocontroller/query/?fName=Devnandan&lName=Kumar" -w "\n"
Hello Devnandan Kumar!!
```

```
curl -X GET "http://localhost:8080/hellocontroller/param/Devnandan" -w "\n"
Hello Devnandan!
```