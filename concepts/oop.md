# What Is Wrong with OOP

Some things in this may be obvious or beating a dead horse but they should be mentioned because obvious things can turn
out to be wrong and if you don't know why something is wrong then it'll be more difficult to fix.

Programming by default is a field where almost everything you are building is new. In other words you don't know how
something is going to be built until it is built. This makes every premtive decision you make is a liability. That being
said, we all have to make a premtive decision to some degree so what's the best way to do this? The awnser in my
experiance is to build only what is needed to complete the task. This acomplishes a few things, but first and foremost
it illiminates code and concepts that you may want to preimtively create that will later just be something you have to
keep in mind or refactor.

This illuminates our core problem with OOP: inheritance. Inheritance is flawed in concept and by proxy design because it causes you to build
extra code and keep in mind unnessisary concepts. If your class is a Cat inheriting a Animal you
must now make sure that the cat does everything the animal does. This means that you're building code and concepts
because of the animal and not because of the task you are trying to acomplish. This, however, doesn't mean that the design is completely unuseable.
If I'm building a zoo, and I want every animal to have a form of locamotion so that they can all be used by certain
features in a program then inheritance becomes much more useful. Now if I put a locamotion method on my class and force
everyone who inherits the class to implement it, it can now be used consitantly across the program based on that inheritance.
A real world example of this is Flutter. While everything is a Widge is a borderline meme and the team is probably more on board with the idea of inheritance, the Widge class provides a standard for
dev tools and context that must be used throughout the app creating a fantastic experiance for developers.

Even if you follow this ideal; however, there is a danger here. If inheritance goes too deep then the flexibility of
the program becomes compramised because we now must keep in mind the 7 classes up the inheritance tree. Having this in
a language is bad and damages the community, but if you follow best practices, it's not your problem. Unfortunately that's the
best I can do for you if I want to make a superset of JS.

The best way to alivate deeply nested inheritance is by injecting method and property requirements into a class. Rust
does this very well with their traits and implementations.

```
// structs are the better form of classes as they represent data instead of concepts and are used throughout functional
// programming.
struct Cat {
  name: String,
  fur_color: String,
  legs: int,
}

trait Locamotion {
  fn speed(&self) -> int;
}

trait Color {
  fn color(self) -> String;
}

impl Locamotion for Cat {
  fn speed(self) -> int {
    return self.legs * 20;
  }
}

impl Color for Cat {
  fn color(self) -> String {
    return self.color;
  }
}

// This is close to valid rust so that people who don't write rust can understand it. I apoligize to rustations brains.
// Arrows represent return types.
```

Another benifit this highlights is that you are now creating less wordy dependances because instead of being a sub type
of Animal which would have to being named MotionOfObject or ColorOfObject, we're now a set of standards that moves and colors the struct.

Abstract classes can also do this to a degree; however, it still opens the floor to problems with deeply nested
inheritance, concepts driving design as oposed to design driving concepts, and excessive wordiness.

For DevScript unlike rust properties on traits will probably be allowed

## The Beifit of Using a Class or Structure Over a Function

A lot of times when I'm programming, I sit back and think to myself this class is just a glorified function. While this
can lead to some problems, it can also be a good thing if done right. Lets say I'm designing a program that calculates different
data points for a car, and I have an engine class. Let's also say in that engine class I'm calculating horse power.

```
class Engine {
  constructor(cylinders, cylinderRadius, cylinderHight, injectionRate) {
    this.cylinders = cylinders,
    this.cylinderRadius = cylinderRadius,
    this.cylinderHight = cylinderHight,
    this.injectionRate = injectionRate,
  }

  get cylinderVolume() {
    // calculations
  }

  get hoursePower() {
    // calculations
  }
}
``` 
This is now essentially a glorified function in order to get hoursepower, but as my program grows I decided that I need to calculate the weight of the car and the space I need for the hood. This class now leaves me with a few options.
The first is that I can put the calculations for the weight of the engine in a place that you'd expect it to be,
next to the engine data. The second is that I can grab the cylinderVolume to help guess what my space is under the hood
even if I don't have all the parts to guess the actual size of the engine. 

```
class Engine {
  constructor(cylinders, cylinderRadius, cylinderHight, injectionRate) {
    this.cylinders = cylinders,
    this.cylinderRadius = cylinderRadius,
    this.cylinderHight = cylinderHight,
    this.injectionRate = injectionRate,
  }

  get cylinderVolume() {
    // calculations
  }

  get hoursePower() {
    // calculations
  }

  get engineWight() {
    // calculations
  }
}

class Hood {
  constructor() {
    // stuff
  }

  get spaceNeeded(engine) {
    // calculations with engine.cylinderVolume
  }
}
```

Now my engine weight is in a predictable spot and I don't have to worry about the calculations for cylinderVolume to be in multiple spots in my program.

This doesn't mean you should always use classes or that this is always the solution for this particular problem, but understanding what benifits they can bring over functions is very useful.

## What Should Class Decloration Look Like

Dart does class declaration best, classes must remain in this language if we want it to be a predictable superset of
JS, and theoretically those classes can be easily and predictably compiled into JS. Dart's class structure also removes
the need for seperate type declarations and condenses a lot of code. I won't get into it here because it's already very
well documented on their website, and there really isn't anything more I can add other than that there may be comprimises
with allowing for multiple functions to use the same name.  
https://dart.dev/language#classes
