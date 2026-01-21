# Day 10 leanring tech
## Flask - Variable Rule
Flask variable rules allow us to create dynamic URLs by defining variable parts within the route. This makes it possible to capture values from the URL and pass them to view functions.
Variable Rules
-	A variable rule is defined using <variable-name> within the route.
-	The captured variable is automatically passed as a keyword argument to the associated function.
-	This feature helps build more flexible and interactive web applications by allowing dynamic content retrieval based on user input.
## Dynamic URLs Variable In Flask
The following converters are available in Flask-Variable Rules:
- String - It accepts any text without a slash(the default).
- int - accepts only integers. ex =23 
-	float - like int but for floating point values ex. = 23.9
-	path - like the default but also accepts slashes.
-	any - matches one of the items provided.
-	UUID = accepts UUID string
	

## Simple flask program
```python from flask import Flask
app = Flask(__name__)


@app.route('/')
def msg():
    return "Welcome To The GreeksForGreeks"

 # we run code in debug mode
if __name__=="__main__":
   app.run(debug=True)
 ```
## String Variable in Flask
In this code, we will define a function that handles a dynamic string variable in the URL.

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def msg():
    return "Welcome"

# We defined string  function
@app.route('/vstring/<name>')
def vstring(name):
    return "My Name is %s" % name

# we run app debugging mode
if __name__=="__main__:
 app.run(debug=True)
 ```
 **Explanation:**
-	@app.route('/'): Defines the homepage route that returns a welcome message.
-	@app.route('/vstring/<name>'): A dynamic route that takes a string parameter and displays it in a message.
-	app.run(debug=True): Runs the Flask app with debugging enabled.

# Integer Variable in Flask
To understand how integer variables work in flask let's create a function that handles integers since Flask doesn't define it by default. Finally, we return the integer value and run the app. To access the integer page, we include the function name and an integer in the URL.

```python 
from flask import Flask
app = Flask(__name__)

@app.route('/')
def msg():
    return "Welcome"

# define int function
@app.route('/vint/<int:age>')
def vint(age):
    return "I am %d years old " % age

# we run our code in debug mode
if __name__=="__main__":
  app.run(debug=True)
```
# Float Variable in Flask
To demonstrate a float variable in Flask, we define a float function since Flask doesn’t define it by default. The function returns the float value, and we run the app using Flask run. To access the float page, we include the function name and a floating-point number in the URL.
```python 
from flask import Flask
app = Flask(__name__)

@app.route('/')
def msg():
    return "Welcome"

# define float function
@app.route('/vfloat/<float:balance>')
def vfloat(balance):
    return "My Account Balance %f" % balance

 # we run our code in debugging mode
if __name__=="__main__":
  app.run(debug=True)
  ```
	
