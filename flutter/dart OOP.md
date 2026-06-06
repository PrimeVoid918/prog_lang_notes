## Classes
```dart

// methods public by default
class Person {
	String name;
	
	// Private Fields
	int _age = 0;
	
	// constructor
	// this.name = name
	Person(this.name) {
		// this block is optional but can be used 
	};
	
	// named constructor
	Person({required this.name})
	// usage
	final person = Person(name: "sample");
	
	void greet() {
		print("Hello $name");
	}
	
	// setter and getter
	set name(String value) {
		_name = value;
	}
	String get name(){
		return _name;
	}
}

// Inheritance
class Employee extends Person {
	Employee(super.name);
	
	@override
	void greet() {
		print("employee greet");
	}
	
	// dart anotations
	@override
	@immutable
	@pragma
	@Deprecated
}
// or 
class Employee extends Person {
	Employee(String name) : super(name);
}

// implements forces FULL reimplementation even inherited methods must be rewritten
class Car implements Vehicle {
	@override
	void start() {}
		
	@override
	void stop() {}
}

// Abstract Classes
abstract class Animal {
	void sound();
}

class Dog extends Animal {
	@override
	void sound() {
		print("Bark");
	}
}
```

## Mixins
``` dart 
// uses "with" keyword upon usage

mixin Flyable {
	void fly() {
		print("Flying");
	}
}

// Usage
class Bird with Flyable {}
```

## Class Modifiers
``` dart 
// final class
// Cannot be extended.
final class Animal {}

// sealed class
// This is similar to discriminated unions in TS.
sealed class AuthState {}
// Usage
class Loading extends AuthState {}
class Success extends AuthState {}
class Error extends AuthState {}
// VERY important for:
// - Bloc
// - Riverpod
// - reducers
// - state machines
```