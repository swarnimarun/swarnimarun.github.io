---
title: Functionalism, the boon or curse?
date: "2020-03-14T22:12:03.284Z"
description: ""
---

This is my first post on my absolutely not new blog :P<br/>
How exciting!

I'm sure I'll write a lot more interesting things in the future.

But for now let's start with a short and simple post with some examples from languages ranging from typed to untyped, from functional to not-at-all functional.

First, let me make it clear that I will not be concluding which is a better language or going into details about them but rather to look at some very beginner examples of code such as writing fizzbuzz, to a simple parser for regex(finite automata).

For this part 1 we will only be doing FizzBuzz programs.

### JavaScript
As you may have guessed, easily one the most popular and most polarising languages in the programming community but it's not a language without it's merits.

```js
// some naive code
let a = parseInt(prompt("input a"));
let b = parseInt(prompt("input b"));

for (let x = a; x < b; x++) {
    let v = ""
    if (x % 3 == 0) 
        v = "fizz"
    if (x % 5 == 0) 
        v += "buzz"
    if (v)
        console.log(v);
}
```

<br/>
Let's make it a little more functional + js-esque

```js
// coerce into int
const getInt = x => parseInt(prompt(x))
let a = getInt("input a")
let b = getInt("input a")
// exploit array keys function
// which needs to be destructed as it returns an iter
[...Array(b-a).keys()] // we need ranges, or better alternative
    .map( x => x + a) // results in an end exlusive range
    .map( x => (x % 3 ? "" : "fizz") + (x % 5 ? "" : "buzz"))
    .filter(x => x) // wish js had a default identity function
    .forEach(console.log)
```
<br/>
So first one is a typical imperative code without any kinds of magic or hidden language features being used while second one is a tad bit more complex with use of coercion, destructoring,<br/>
Does the second one really look soo much better???<br/>
Not really...<br/>
So does it perform sooo much better????<br/>
Not really...<br/>

So was there any use? Again not really....<br/>
So what then, ofc this is cherry picked example where functional programming doesn't shine?????

Well let's first take a look at some more code from other languages.

### Python

Naive/imperative python code,
```py
def main():
  a = input()
  b = input()
  c = range(a, b)
  arr = []
  for x in c:
    if x % 15 == 0:
      arr.append("fizzbuzz")
    if x % 3 == 0:
      arr.append("fizz")
    if x % 5 == 0:
      arr.append("buzz")
  print(arr)
```
<br/>
Functionally inclined python code,

```py
def main():
    a = input()
    b = input()
    c = range(a, b)
    d = list(filter(lambda x: x, # we really need that id function
            map(lambda x: 
                if x % 15:
                    "fizzbuzz"
                else if x % 3:
                    "fizz"
                else if x % 5:
                    "buzz"
                , c)))
    print(d)
```

### Go
Yes go, the opinionated beast.

```go
package main
import "fmt"

func main() {
    var a int
    fmt.Scan(&a)
    // I know I should error check but...mehhh...
    var b int
    fmt.Scan(&b)
    v := make([]string, 0);
    for i := a; i < b; i++ {
        if i%15 == 0 {
            v = append(v, "FizzBuzz");
        } else if i%3 == 0 { // no truthy falsy
            v = append(v, "Fizz");
        } else if i%5 == 0 {
            v = append(v, "Buzz");
        }
    }
    fmt.Println(v);
    // not sure how to make it more functional
    // feel free to share ideas.
}
```

### Rust
I know it's not the most idiomatic code snippet but let's bear with it,
```rust
use std::io;

fn get_int() -> i32 {
    let mut st = String::new();    
    io::stdin().read_line(&mut st).expect("input failed");
    st.trim().parse::<i32>().expect("parse to int failed")
}

fn main() {
    let a = get_int();
    let b = get_int();
    let v = Vec::new();
    for i in (a..b) {
        if i%15 == 0 {
            v.push("fizzbuzz")
        } else if i%3 == 0 { // no truthy falsy
            v.push("fizz")
        } else if i%5 == 0 {
            v.push("buzz")
        }
    }
    println!("{:?}", v);
}
```
<br/>
Going functional,

```rust
use std::io;

fn get_int() -> i32 {
    let mut st = String::new();    
    io::stdin().read_line(&mut st).expect("input failed");
    st.trim().parse::<i32>().expect("parse to int failed")
}

fn main() {
    let a = get_int();
    let b = get_int();
    let v: Vec<_> = (a..b)
        .map(|x| {
            (if x % 3 == 0 { "fizz" } else { "" }).to_owned()
                + (if x % 5 == 0 { "buzz" } else { "" })
        })
        .filter(|x| !x.is_empty()) // can't do truthy falsy here :P
        .collect();
    println!("{:?}", v);
}
```
<br/>
Let's pattern match a little,

```rust
use std::io;

fn get_int() -> i32 {
    let mut st = String::new();    
    io::stdin().read_line(&mut st).expect("input failed");
    st.trim().parse::<i32>().expect("parse to int failed")
}

fn main() {
    let a = get_int();
    let b = get_int();
    let v: Vec<_> = (a..b)
        .map(|x| {
            match (x % 3, x % 5) {
                (0, 0) => "fizzbuzz",
                (0, _) => "fizz",
                (_, 0) => "buzz",
                _ => ""
            } // I know pattern matching rocks
        })
        .filter(|x| !x.is_empty())
        .collect();
    println!("{:?}", v);
}
```
Alright this might be a little new for some folks, but pattern matching sure is amazing. :P

We can clearly tell that the second snippet is much more clean and readable. So I would say yes it does make a difference.

### Haskell

I know I am not good at Haskell :P

```haskell
-- this was the best I could as of writing this article
-- feel to suggest better methods
fizzbuzz x = case (x `rem` 3, x `rem` 5) of
        (0,0) -> "fizzbuzz"
        (0,_) -> "fizz"
        (_,0) -> "buzz"
        _     -> ""

main = do
      st <- getLine
      let x = (read st :: Int)
      vt <- getLine
      let y = (read vt :: Int)
      let z = filter (\x -> length(x) > 0) $ fmap fizzbuzz [x..y]
      putStrLn $ show $ z
```

## Conclusion
I am not sure how I should put this but there are some clear differences that can be seen here, but which one is more clear surely depends on who you ask. 

Want to add code for you favourite langauge? Or suggest improvements go ahead and send a PR for this file on 
[my-blog](https://github.com/swarnimarun/swarnimarun.github.io)