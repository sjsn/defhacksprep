# Hackathon Prep!
> By Sam San Nicolas

This is a very brief Git and Python/Flask code review/lesson I made for my friends in preparation for their first Hackathon, [defHacks 2017](http://defhacks.io/). It's probably not the best, but it should get the job done in teaching them the basics of what they need to know for our project. *Designed for Windows machines*.

## Before starting
I assume you already have a GitHub account since you're reading from this private repo, but in case you're a wizard, please go make one! I also recommend registering it as a student account [here](https://education.github.com/pack). This will allow you to create an unlimited number of private repos and also gives you other perks such as free software and AWS credits!

### Common Terminology
* *Directory* - A folder on your system.
* *Type* - Put into the command prompt.
* *ReadMe.md* - This file that you're reading. GitHub uses ReadMe's as little documents inside their directories to give context about a project. the '.md' extension stands for 'MarkDown', a text formatting engine which can beautify plain text into a document such as this.
* *console* - The debugging interface. Could be the command prompt, the [Chrome Developer Tools](https://developer.chrome.com/devtools), etc.

## Things you should download
I recommend all of this! I use it and I'm a pro so it must be good.

1. [Sourcetree](https://www.sourcetreeapp.com/) - A visual Git client.
* [Python 3](https://www.python.org/downloads/) - Make sure you get the 3.x.x version! Python 2 is garbage.
  * To check if it's installed, open your command prompt (search for `cmd`) and then type python. An execution shell should open up. Then type the command `import sys` and then `print(sys.version)`. It should output (3.6.0). Type `exit()` to close the execution shell.
* [Atom](https://atom.io/) - An open source "industry standard" text editor!
* [Git](https://git-scm.com/downloads) - Git is a version control system (the industry standard) that allows multiple people to edit code at the same time without breaking everything. Think of it as a lazy Google Docs but for coding.

## Setting up
This should be done *after* downloading the shit above.

1. Open Source Tree, the command prompt, and the Atom text editor.

### Set up your repo
1. In Source Tree, clone this repo.
  1. Click the `Clone / New` button in the top left corner.
  * Paste in this repo's URL into the `Path / URL` field
    * `https://github.com/sjsn/defhacksprep.git`
  * Save it somewhere you could easily find again. I recommend to the `Desktop` folder so you can accses all your files from your home screen.
  * It will ask you to authenticate. Use your GitHub credentials from earlier.
  * It will then ask you how you want to be addressed on commits. Just use your first name and your email address from your account for now.

You should now be able to see the history of this repo! Pretty cool. Ask me questions about what it all means.

### Install the required python packages
1. In the command prompt navigate to the folder where you cloned the repo.
  * Type `dir` to list all directories within your current directory
  * Type `cd [directory name]` to change directories
    * `cd ..` moves up a directory. (Yes, that is two dots.)
    * Keep in mind this is case sensitive!
    * Typing the first couple letters and then hitting `tab` will auto complete. Saves a shit ton of time.
* Type `pip install virtualenv`
  * `pip` stands for "PIP installs Python" (yes, it is a recursive acronym). It pretty much allows us to download other peoples Python code and use it in our own code. In this instance we are installing ["virtualenv"](http://docs.python-guide.org/en/latest/dev/virtualenvs/). This allows us to create a "virtual environment", which is pretty much a subdirectory, in which to store all of the Python code we borrow from other people so it won't interfere with our own code.
* Type `virtualenv venv` to create the virtual environment in a directory called "venv".
* Type `source venv/bin/activate` to go inside the virtual environment. (Type `deactivate` to exit it)
* Type `pip install flask`
  * In this instance, we are downloading a package called ["flask"](http://flask.pocoo.org/) which is an open source (anyone can contribute to and use it) web frameworking tool. If you `cd` into the venv directory, you will see that it now contains some additional files that it got when you installed flask.

Any questions? Now's a good time to ask. We're pretty much just coding after this.

### Code it up in Atom!
1. Within Atom, open the the repo.
  * Tip! You can open whole directories as opposed to individual files. Makes it super easy to manage entire projects.
2. Create a new file called server.py
  * **Warning** I recommend reviewing python a bit before moving on. I included a *brief* python review section at the bottom of this readme
3. Copy and paste the code below into the file
```python
  # import statements to access code we installed through pip
  from flask import Flask, render_template, jsonify, redirect
  import request

  # Sets the Flask application to this file
  app = Flask(__name__)

  # The '@' symbol is a decorator in python that adds additional funcionality to a python function
  # @app.route tells the web to listen at the root directory (highest level, the '/' at the end of a url) for anyone who requests or 'GET's it
  @app.route('/', methods=['GET'])
  def main():
    # Let's store your name in this variable to render out to our website!
    your_name = 'insert your name here'

    # We give back the index.html page to anyone who requests our root directory
    # index.html is just a (pre-coded by me) web file that contains a basic website
    # We also pass in the 'your_name' variable as 'name' so our webpage can access it
    return render_template('index.html', name=your_name)

```

### Test the app!
1. Go back to the command prompt
2. Make sure you're in the project directory
3. Search for "environment variables" in the Windows search bar in the bottom left of your screen. Click on "Edit environment variables for your account".
4. Set `FLASK_APP=server.py` and `FLASK_DEBUG=1`
    * The FLASK_APP variable tells your machine that the Flask framework is going to use a file called server.py. The FLASK_DEBUG enables the debug mode to show any errors.
5. Type `flask run`
6. Launch your web browser of choice (Chrome is the best IMO, but firefox works too. Avoid edge/safari as they don't support all web standards)
7. Go to [localhost:8080](http://localhost:8080)
8. Congratulations! You made your first web app!
  * You can go back to the server.py file and change the your_name variable to whatever you want. When you save the file, come back to your browser and refresh the webpage. It will update in real-time.
9. What's going on:
  * localhost is pretty much just your computer pretending to be a website. Developers use it to test their web applications before launching them.
  * the :8080 is telling your machine to open up port 8080 (a port commonly used for web-dev) and allowing the browser to access its information.
  * A port is just a window into the files on your computer (not really but for simplicity's sake we'll go with that). It allows the browser (a file on your machine) to read and interpret the exposed information (the server.py file) and turn it into whatever the information demanded.

---

## (Very brief) Python Review!
This is a shitty and uninformative review of Python. I'd write more, but honestly, if you need more than this you can just google it. This should get you through the majority of things you'll need to do in terms of Flask, but there's plenty of other resources (such as just asking me) if you need any additional help.
```python
# Data Structures!

# Python has 2 main data structures, lists (arrays) and dictionaries (maps)
# A list stores indexed data and is declared within []'s
grocery_list = ["apples", "bananas", "carrots", "celery"] # Just listing things I need to buy
# A dictionary stores key-value pairs of data and is declared within {}'s
better_grocery_list = {"apples": False, "bananas": True, "carrots": False} # Listing things I need to buy and whether I got them

# Lists can store dictionaries such as [{...}, {...}, {...}] as well as any other data type (int, boolean, string, etc)
# Dictionaries can store lists as values such as {"key": [...], "key2": [...]} as well as any other data type
  # Note! Notice the keys MUST be strings! This is important

# List Operations

# Can add to list end of a list using .push()
grocery_list.push("juice") # New list is ["apples", "bananas", "carrots", "celery", "juice"]
# Can add anywhere else using index (Remember 0-based indexing!)
grocery_list[4] = "bread" # New list is ["apples", "bananas", "carrots", "celery", "bread"]
# Can remove from end of list with .pop()
print(grocery_list.pop()) # prints "bread" and new list is ["apples", "bananas", "carrots", "celery"]
# Can reference list using index
print(grocery_list[0]) # prints "apples"

# Dictionary Operations

# Can add to dictionary using key
better_grocery_list["juice"] = False # New dictionary is {"apples": False, "bananas": True, "carrots": False, "bread": False}
# Can reference value using key
print(better_grocery_list["juice"]) # prints False

# ------------------------------------------------------------------------------------------------------------ #

# Looping!

# for loops
# Think of as for-each (for each value in this data structure, do this...)
for item in grocery_list:
  print(item) # Would print "apples", "bananas", "carrots", "celery"

# ------------------------------------------------------------------------------------------------------------ #

# Functions!

# Use def to define a function. Anything within the parenthesis is passed in as parameters. You don't need to specify the type of parameter.
# You can specify a default value for a parameter by assigning it in the parameter area
def hello(param1, param2="This is the default"):
  # param1 could be of type String, and int, and float, etc.
  # param2 defaults to "This is the default" if the user didn't specify the value

  # Use print() to log stuff to the console. (*Note*: Python 3 requires the paranthesis for print statements. Python 2 did not.)
  print(param1) # Python is a whitespace language. Don't need semicolons, only tabs and indentation
  print(param2)

# Call a function by typing its name alongside any parameters
hello("test") # Would print "test" followed by "This is the default"
hello("Another test", "Tests are stupid") # Would print "Another Test" followed by "Tests are stupid"

```
