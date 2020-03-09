## Introduction: Class Inheritance
## 22.1. Introduction: Class Inheritance
* Classes can “inherit” `methods` and `class variables` from other classes.
* First, however, let’s motivate why this might be **valuable**.
* It turns out that inheritance doesn’t let you do anything that you couldn’t do without it, but it makes some things a lot more elegant. You will also find it’s useful when someone else has defined a class in a module or library, and you just want to override a few things without having to reimplement everything they’ve done.
* Consider our Tamagotchi game. Suppose we wanted to make some different kinds of pets that have the same structure as other pets, but have some different attributes or behave a little differently. For example, suppose that dog pets should show their emotional state a little differently than cats or act differently when they are hungry or when they are asked to fetch something.

* You could implement this by making an instance variable for the pet type and dispatching on that instance variable in various methods.
```python
from random import randrange

class Pet():
    boredom_decrement = 4
    hunger_decrement = 6
    boredom_threshold = 5
    hunger_threshold = 10
    sounds = ['Mrrp']
    def __init__(self, name = "Kitty", pet_type="dog"):
        self.name = name
        self.hunger = randrange(self.hunger_threshold)
        self.boredom = randrange(self.boredom_threshold)
        self.sounds = self.sounds[:]  # copy the class attribute, so that when we make changes to it, we won't affect the other Pets in the class
        self.pet_type = pet_type

    def clock_tick(self):
        self.boredom += 1
        self.hunger += 1

    def mood(self):
        if self.hunger <= self.hunger_threshold and self.boredom <= self.boredom_threshold:
            if self.pet_type == "dog": # if the pet is a dog, it will express its mood in different ways from a cat or any other type of animal
                return "happy"
            elif self.pet_type == "cat":
                return "happy, probably"
            else:
                return "HAPPY"
        elif self.hunger > self.hunger_threshold:
            if self.pet_type == "dog": # same for hunger -- dogs and cats will express their hunger a little bit differently in this version of the class definition
                return "hungry, arf"
            elif self.pet_type == "cat":
                return "hungry, meeeeow"
            else:
                return "hungry"
        else:
            return "bored"

    def __str__(self):
        state = "     I'm " + self.name + ". "
        state += " I feel " + self.mood() + ". "
        return state

    def hi(self):
        print(self.sounds[randrange(len(self.sounds))])
        self.reduce_boredom()

    def teach(self, word):
        self.sounds.append(word)
        self.reduce_boredom()

    def feed(self):
        self.reduce_hunger()

    def reduce_hunger(self):
        self.hunger = max(0, self.hunger - self.hunger_decrement)

    def reduce_boredom(self):
        self.boredom = max(0, self.boredom - self.boredom_decrement)
```

* That code is exactly the same as the code defining the Pet class that you saw in the `Tamagotchi` section, except that we’ve added a few things.
  - A new input to the constructor – the `pet_type` input parameter, which defaults to **"dog"**, and the **self.pet_type** instance variable.
  - if..elif..else in the **self.mood()** method, such that different types of pets (a dog, a cat, or any other type of animal) express their moods and their hunger in slightly different ways.
* But that’s not an elegant way to do it. It obscures the parts of being a pet that are common to all pets and it buries the unique stuff about being a dog or a cat in the middle of the mood method. What if you also wanted a dog to reduce boredom at a different rate than a cat, and you wanted a bird pet to be different still? Here, we’ve only implemented dogs, cats, and other – but you can imagine the possibilities.
* If there were lots of different types of pets, those methods would start to have long and complex if..elif..elif code clauses, which can be confusing. And you’d need that in every method where the behavior was different for different types of pets. Class inheritance will give us a more elegant way to do it.

## Inheriting Variables and Methods
```python
CURRENT_YEAR = 2020
class Person:
  def __init__init__(self, name, year_born):
    self.name = name
    self.year_born = year_born
  def getAge(self):
    return CURRENT_YEAR - self.year_born
   def __str__(self):
   return "{} ({})".format(self.name, self.getAge())

alice = Person("Alice Smith", 1990)
print(alice)


```

* Suppose you want to define a class for student:
```python
class Student:
  def __init__(self, name, year_born):
    self.name = name
    self.year_born = year_born
    self.knowledge =0
  def getAge(self):
    self.knowledge +=1
    return CURRENT_YEAR - self.year_born
  def __str__(self):
    return "{} ({})".format(self.name, self.getAge())

alice = Student("Alice Smith", 1990)
print(alice)
alice.study()
print(alice.knowledge)
```
* But there is a most easer way to do this, by using Inheriting.
* In this case, every student is a Person
* So, student should have everything a person has.
* you put the Person class inside the Student class:
```python
class Person:
  def __init__init__(self, name, year_born):
    self.name = name
    self.year_born = year_born
  def getAge(self):
    return CURRENT_YEAR - self.year_born
   def __str__(self):
   return "{} ({})".format(self.name, self.getAge())

class Student(Person):
  def __init__(self, name, year_born):
    Person.__init__(self, name, year_born)
    self.knowledge =0
  def study(self):
    self.knowledge +=1
  # def getAge(self):          ----now removed
  #   self.knowledge +=1
  #   return CURRENT_YEAR - self.year_born
  # def __str__(self):
  #   return "{} ({})".format(self.name, self.getAge())

alice = Student("Alice Smith", 1990)
print(alice)
alice.study()
print(alice.knowledge)
print(alice.getAge())
print(alice)
```
## 22.2. Inheriting Variables and Methods¶
### 22.2.1. Mechanics of Defining a Subclass

* We said that inheritance provides us a more elegant way of, for example, creating **Dog** and **Cat** types, rather than making a very complex **Pet** class. In the abstract, this is pretty intuitive: all pets have certain things, but dogs are different from cats, which are different from birds. Going a step further, a Collie dog is different from a Labrador dog, for example. Inheritance provides us with an easy and elegant way to represent these differences.
* Basically, it works by defining a new class, and using a special syntax to show what the new sub-class inherits from a super-class. So if you wanted to define a **Dog** class as a special kind of **Pet**, you would say that the **Dog** type inherits from the **Pet** type. In the definition of the inherited class, you only need to specify the methods and instance variables that are different from the parent class (the parent class, or the superclass, is what we may call the class that is inherited from. In the example we’re discussing, **Pet** would be the superclass of **Dog** or **Cat**).
* Here is an example. Say we want to define a class Cat that inherits from Pet. Assume we have the Pet class that we defined earlier.

* We want the Cat type to be exactly the same as Pet, except we want the sound cats to start out knowing “meow” instead of “mrrp”, and we want the Cat class to have its own special method called chasing_rats, which only Cat s have.

* For reference, here’s the original Tamagotchi code
```python
from random import randrange

# Here's the original Pet class
class Pet():
    boredom_decrement = 4
    hunger_decrement = 6
    boredom_threshold = 5
    hunger_threshold = 10
    sounds = ['Mrrp']
    def __init__(self, name = "Kitty"):
        self.name = name
        self.hunger = randrange(self.hunger_threshold)
        self.boredom = randrange(self.boredom_threshold)
        self.sounds = self.sounds[:]  # copy the class attribute, so that when we make changes to it, we won't affect the other Pets in the class

    def clock_tick(self):
        self.boredom += 1
        self.hunger += 1

    def mood(self):
        if self.hunger <= self.hunger_threshold and self.boredom <= self.boredom_threshold:
            return "happy"
        elif self.hunger > self.hunger_threshold:
            return "hungry"
        else:
            return "bored"

    def __str__(self):
        state = "     I'm " + self.name + ". "
        state += " I feel " + self.mood() + ". "
        # state += "Hunger %d Boredom %d Words %s" % (self.hunger, self.boredom, self.sounds)
        return state

    def hi(self):
        print(self.sounds[randrange(len(self.sounds))])
        self.reduce_boredom()

    def teach(self, word):
        self.sounds.append(word)
        self.reduce_boredom()

    def feed(self):
        self.reduce_hunger()

    def reduce_hunger(self):
        self.hunger = max(0, self.hunger - self.hunger_decrement)

    def reduce_boredom(self):
        self.boredom = max(0, self.boredom - self.boredom_decrement)

# Here's the new definition of class Cat, a subclass of Pet.
class Cat(Pet): # the class name that the new class inherits from goes in the parentheses, like so.
    sounds = ['Meow']

    def chasing_rats(self):
        return "What are you doing, Pinky? Taking over the world?!"
```
* All we need is the few extra lines at the bottom of the ActiveCode window! The elegance of inheritance allows us to specify just the differences in the new, inherited class. In that extra code, we make sure the **Cat** class inherits from the **Pet** class. We do that by putting the word Pet in parentheses, class Cat(Pet):. In the definition of the class **Cat**, we only need to define the things that are different from the ones in the **Pet** class.
* In this case, the only difference is that the class variable **sounds** starts out with the string **"Meow"** instead of the string **"mrrp"**, and there is a new method **chasing_rats**.
* We can still use all the **Pet** methods in the **Cat** class, this way. You can call the __str__ method on an instance of **Cat** to `print` an instance of **Cat**, the same way you could call it on an instance of **Pet**, and the same is true for the **hi** method – it’s the same for instances of **Cat** and **Pet**. But the chasing_rats method is special: it’s only usable on **Cat** instances, because **Cat** is a subclass of **Pet** which has that additional method.
* In the original Tamagotchi game in the last chapter, you saw code that created instances of the **Pet** class. Now let’s write a little bit of code that uses instances of the **Pet** class AND instances of the **Cat** class.

```python
p1 = Pet("Fido")
print(p1) # we've seen this stuff before!

p1.feed()
p1.hi()
print(p1)

cat1 = Cat("Fluffy")
print(cat1) # this uses the same __str__ method as the Pets do

cat1.feed() # Totally fine, because the cat class inherits from the Pet class!
cat1.hi()
print(cat1)

print(cat1.chasing_rats())

#print(p1.chasing_rats()) # This line will give us an error. The Pet class doesn't have this method!

```
* And you can continue the inheritance tree. We inherited **Cat** from **Pet**. Now say we want a subclass of **Cat** called **Cheshire**. A Cheshire cat should inherit everything from **Cat**, which means it inherits everything that **Cat** inherits from **Pet**, too. But the **Cheshire** class has its own special method, **smile**.
```python
class Cheshire(Cat): # this inherits from Cat, which inherits from Pet

    def smile(self): # this method is specific to instances of Cheshire
        print(":D :D :D")

# Let's try it with instances.
cat1 = Cat("Fluffy")
cat1.feed() # Totally fine, because the cat class inherits from the Pet class!
cat1.hi() # Uses the special Cat hello.
print(cat1)

print(cat1.chasing_rats())

new_cat = Cheshire("Pumpkin") # create a Cheshire cat instance with name "Pumpkin"
new_cat.hi() # same as Cat!
new_cat.chasing_rats() # OK, because Cheshire inherits from Cat
new_cat.smile() # Only for Cheshire instances (and any classes that you make inherit from Cheshire)

# cat1.smile() # This line would give you an error, because the Cat class does not have this method!

# None of the subclass methods can be used on the parent class, though.
p1 = Pet("Teddy")
p1.hi() # just the regular Pet hello
#p1.chasing_rats() # This will give you an error -- this method doesn't exist on instances of the Pet class.
#p1.smile() # This will give you an error, too. This method does not exist on instances of the Pet class.

```

## 22.2.2. How the interpreter looks up attributes
* So what is happening in the Python interpreter when you write programs with classes, subclasses, and instances of both parent classes and subclasses?

* ***This is how the interpreter looks up attributes***:**

  - 1. First, it checks for an instance variable or an instance method by the name it’s looking for.

  - 2. If an instance variable or method by that name is not found, it checks for a class variable. (See the previous chapter for an explanation of the difference between instance variables and class variables.)

  - 3. If no class variable is found, it looks for a class variable in the parent class.

  - 4. If no class variable is found, the interpreter looks for a class variable in THAT class’s parent (the “grandparent” class).

  - 5. This process goes on until the last ancestor is reached, at which point Python will signal an error.

* Let’s look at this with respect to some code.

* Say you write the lines:

```python
new_cat = Cheshire("Pumpkin")
print(new_cat.name)
```
* In the second line, after the instance is created, Python looks for the instance variable **name** in the new_cat instance. In this case, it exists. The name on this instance of **Cheshire** is **Pumpkin**. There you go!

* When the following lines of code are written and executed:
```python
cat1 = Cat("Sepia")
cat1.hi()
```
* The Python interpreter looks for **hi** in the instance of **Cat**. It does not find it, because there’s no statement of the form **cat1.hi = ...**. (Be careful here – if you had set an instance variable on Cat called hi it would be a bad idea, because you would not be able to use the method that it inherited anymore. We’ll see more about this later.)

* Then it looks for hi as a class variable (or method) in the class Cat, and still doesn’t find it.

* Next, it looks for a class variable **hi** on the parent class of **Cat, Pet**. It finds that – there’s a method called **hi** on the class **Pet**. Because of the **()** after **hi**, the method is invoked. All is well.

* However, for the following, it won’t go so well
```python
p1 = Pet("Teddy")
p1.chasing_rats()
```
* The Python interpreter looks for an instance variable or method called **chasing_rats** on the Pet class. It doesn’t exist. Pet has no parent classes, so Python signals an error.


## Overriding Methods
* How do we inherit?
* Assume we have a super class. And we have a sub-class. This sub-class is inherit from super-class.
* And then we have an instance of the sub-class.
* whenever python look for any method or instance variables,
* First, it is going to look the instance in the sub-class. If it doesn't , it's going to look inside the subclass for that  `instance variable or method`. If it doesn't it go to superclass.
* So, when should we inherit from superclass?
* We should inherit from only if we have `absolutely everything that the superclass has, plus more or maybe plus some small modification. `
* **Exampe**
* Let suppose we have 2 kind of book in library.
* We have paper books and we have ebooks.
* so we have one superclass for book:
```python
class Book():
  def __init__(self, title author):
    self.title = title
    self.author = author
  def __str__(self):
    return '"{}" by {}'.format(self.title, self.author)
# now create a new book
myBook = Book('The Odyssey', 'Homer')
print(myBook)

```
* Now let include the two type of books.
```python
class Book():
  def __init__(self, title author):
    self.title = title
    self.author = author
  def __str__(self):
    return '"{}" by {}'.format(self.title, self.author)
# the class for first type of Paper book.
class paperBook(Book):
  def __init__(self, title, author, numPages):
    Book.__init__(self, title, author)
    self.numPages = numPages
# the class for first type of ebook.
class EBook(Book):
  def __init__(self, title, author, size):
    Book.__init__(self, title, author)
    self.size = size
# now create a new book
mypaperBook = paperBook('The Odyssey', 'Homer', 500)
print(mypaperBook)
print(mypaperBook.numPages)


myEBook = EBook('The Odyssey', 'Homer', 2)
print(myEBook)
print(myEBook.size)

```
* But we can see that the `paperBook` and `EBook` have everything that `Book` has.
* We know that  `library` contain book.

```python
class Book():
  def __init__(self, title, author):
    self.title = title
    self.author = author
  def __str__(self):
    return '"{}" by {}'.format(self.title, self.author)
# the class for first type of Paper book.
class paperBook(Book):
  def __init__(self, title, author, numPages):
    Book.__init__(self, title, author)
    self.numPages = numPages
# the class for first type of ebook.
class EBook(Book):
  def __init__(self, title, author, size):
    Book.__init__(self, title, author)
    self.size = size

# library class
class Library:
  def __init__(self):
    self.books = []
  def addBook(self, book):
    self.books.append(book)
  def getNumBooks(self):
    return len(self.books)

mypaperBook = paperBook('The Odyssey', 'Homer', 500)
myEBook = EBook('The Odyssey', 'Homer', 2)

aadl = Library()
aadl.addBook(mypaperBook)
aadl.addBook(myEBook)

print(aadl.getNumBooks())
```
## 22.3. Overriding Methods
