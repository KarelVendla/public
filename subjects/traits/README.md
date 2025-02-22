## traits

### Instructions

Imagine you are designing a new video game and you have to create food that the players can eat to gain strength.

There are two types of food for now:

- Fruit: increase the strength by 4 units per each kilogram of fruit consumed.
- Meat: has the weight in kilograms `weight_in_kg` (which is the weight of the whole piece) and the `fat_content` which corresponds to the percentage of the weight which is pure fat (the rest is considered protein) each kilogram of protein gives 4 units of `strength` and each kilogram of fat gives 9 units of `strength`.

Define the `Food` trait for `Fruit` and `Meat`. The required method `gives()` represents the energy that the food provides.

Implement the `std::fmt::Display` trait for `Player` structure in a way that when using the template `{}` inside a println! macro it will print:

- In the first line, the name of the player
- In the second line the strength, score and the money
- In the third line the weapons

### Notions

- [Traits](https://doc.rust-lang.org/book/ch10-02-traits.html)



### Expected Functions and Structures

```rust
#[derive(Debug)]
pub struct Player {
	pub name: String,
	pub strength: f64,
	pub score: i32,
	pub money: i32,
	pub weapons: Vec<String>,
}

pub struct Fruit {
	pub weight_in_kg: f64,
}

pub struct Meat {
	pub weight_in_kg: f64,
	pub fat_content: f64,
}

impl Player {
	fn eat(&mut self, food: T) {
		self.strength += food.gives();
	}
}

pub trait Food {
	fn gives(&self) -> f64;
}

impl Food for Fruit {
}

impl Food for Meat {
}
```

### Usage

Here is a program to test your functions and traits.

```rust
use traits::*;


fn main() {
	let apple = Fruit { weight_in_kg: 1.0 };

	println!("this apple gives {} units of strength", apple.gives());

	let steak = Meat {
		weight_in_kg: 1.0,
		fat_content: 1.0,
	};

	let mut player1 = Player {
		name: String::from("player1"),
		strength: 1.0,
		score: 0,
		money: 0,
		weapons: vec![String::from("knife")],
	};
	println!("Before eating {:?}", player1);
	player1.eat(apple);
	println!("After eating an apple\n{}", player1);
	player1.eat(steak);
	println!("After eating a steak\n{}", player1);
}

```

And its output:

```console
$ cargo run
this apple gives 4 units of strength
Before eating Player { name: "player1", strength: 1.0, score: 0, money: 0, weapons: ["knife"] }
After eating an apple
player1
Strength: 5, Score: 0, Money: 0
Weapons: ["knife"]
After eating a steak
player1
Strength: 14, Score: 0, Money: 0
Weapons: ["knife"]
$
```
