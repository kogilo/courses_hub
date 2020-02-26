# Introduction to the Specialization
## What you'll learn:
* python languages fundamentals
* data structure navigation
* data formatting

## Completion Goals:
* Write longer programs
* comfort using python Modules
* Comfort using external tools

# Welcome to Python Classes and Inheritance
### Classes & Instances: Combine Methods & Data
### Class Inheritance: Better Code Reuse
### Test Cases: Specify what a function or class should do Unit Tests
### Exceptions: Handle Runtime Errors

## How to Use the Interactive Textbook
## Runestone -make use of it everyday
### 20.1. Introduction: Classes and Objects - the Basics
### 20.1.1. Object-oriented programming
* Python is an **object-oriented programming language**.
  - That means it provides features that support **object-oriented programming (OOP)**.

* **Object-oriented programming** has its roots in the **1960s**, but it wasn’t until the mid **1980s** that it became the main programming paradigm used in the creation of new software.
  - It was developed as a way to handle the rapidly increasing size and complexity of software systems and to make it easier to **modify these large and complex systems over time**.
* Up to now, some of the programs we have been writing use a **procedural programming paradigm**.
  - In **procedural programming** the focus is on writing functions or procedures which operate on data.
  - In **object-oriented programming** the focus is on the **creation of objects** which contain **both data and functionality together**.
  - Usually, each object definition corresponds to some object or concept in the real world and the functions that operate on that object correspond to the ways real-world objects interact.
### 20.2. Objects Revisited
* In Python, every value is actually **an object**.
  - Whether it be **a dictionary, a list, or even an integer**, they are all objects.
  - Programs manipulate those objects either by performing computation with them or by asking them to **perform methods**.
  - To be more specific, we say that an object has **a state** and a collection of **methods** that it can perform.
  - The state of an object represents those things that the object knows about itself. The state is stored in instance variables. For example, as we have seen with turtle objects, each turtle has a state consisting of the **turtle’s position, its color, its heading** and so on.
  - Each turtle also has the ability to **go forward**, **backward**, or **turn right or left**.
  - Individual turtles are different in that even though they are all turtles, they differ in the specific values of the individual state attributes (maybe they are in a different location or have a different heading).

## User-Defined Classes
* Let create a python class to represent point.
- eg. point x=10, y=2 or x=8 and y=-3
```python
class Point():
  pass
```
* Here, **Point** is like factory that product goods.
* So, Instances of points created as below:

```python
class Point():
  pass
point1 = Point()
point2 = Point()
```
* If you print out the value of these point, it will give you point object.

```python
print(point1)
print(point2)
print(point1=point2)
```

* Now we can assign the Instances point with the value:

```python
class Point():
  pass
point1 = 5
point2 = 10
print(point1)
print(point2)
print(point1=point2)
```
* Now let fill out the class by defining **a method**
```python
class Point():
  def getx(self):
      return self.x
point1 = Point()
point2 = Point()
point1 = 5
point2 = 10
print(point1.getx())
```
## 20.3. User Defined Classes
* We’ve already seen classes like `str, int, float` and `list`. These were defined by Python and made available for us to use.
* However, in many cases when we are solving problems we need to create data objects that are related to the problem we are trying to solve. We need to create `our own classes`.
* As an example, consider the concept of a mathematical point. In two dimensions, a point is two numbers (coordinates) that are treated collectively as a single object. Points are often written in parentheses with a comma separating the coordinates. For example, `(0, 0)` represents the origin, and `(x, y)` represents the point x units to the right and y units up from the origin. This `(x,y)` is the state of the point.

* Some of the typical operations that one associates with points might be to ask the point for its x coordinate, `getX`, or to ask for its y coordinate, `getY`. You would want these types of functions available to prevent accidental changes to these instance variables since doing so would allow you to view the values without accessing them directly. You may also wish to calculate the distance of a point from the origin, or the distance of a point from another point, or find the midpoint between two points, or answer the question as to whether a point falls within a given rectangle or circle. We’ll shortly see how we can organize these together with the data.
