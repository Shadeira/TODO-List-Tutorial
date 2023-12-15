# How to Create a To-Do List App with HTML, CSS, & JavaScript

## Introduction 
Tired of your "to-do" list looking more like a "to-don't" list? Today's the day we flip the script! We're turning your to-dos into to-dones!

Follow along with this tutorial as we work together to check off every incomplete task on our to-do list using HTML,CSS, and JavaScript. By the end of the tutorial you’ll be able to ADD,DELETE, EDIT, and most importantly COMPLETE tasks. 

Here are the following tasks you will need to complete:
* Add Tasks
* Read Tasks
* Update Tasks
* Delete Tasks
* Count Number of Complete and Uncomplete Tasks


The final project should look similar to this: 

![alt text](/assets/images/gif-todo-list.gif "To-Do List Project Gif")

Let's do this!

## Getting Started
Let’s set up our editor. For this application, we will be using our PC terminal and Visual Studio Code (VS Code).

If you don't have VS Code downloaded, you can [download it here](https://code.visualstudio.com/download).

**Note:** _If you prefer to use an online editor such as Replit you are more than welcome to do so._


First, we need to create a directory and files for our project using the terminal. Once you open the terminal `cd` into your Desktop. This is where we will add our directory. You can name it anything you like but to make it easier let's name it **todo-list-project**:

```
cd Desktop
mkdir todo-list-project
cd todo-list-project
touch index.html script.js styles.css
```

Now, let's see what we have created. Open VS Code and navigate to the top left corner. Click on "File" from the dropdown menu, choose "Open Folder". Proceed to locate and open the **todo-list-project** folder on your Desktop.

Once you have open this folder on VS Code. Within this folder, you will see the necessary files we created to build out your application.

![alt text](/assets/images/vs-code-screen.png "VS Code Screenshot")

The following files have been created in our **todo-list-project** folder:
* **index.html** - we will write our HTML code, and this is what will be displayed on our webpage.
* **style.css** - we will write our CSS code to design how our application looks
* **script.js** - our JavaScript code is where we will add our interactions 


## Task 1: Create TODO List Input
In our **index.html** file we have included a `title` and `link` tag inside of the `head`. For the title we set the name of the app to **TO-DO List**. We also linked the `style.css` file because, trust, styling is gonna make it look super cool later. 

Toward the end of our code we need to include our `script` tag. This will link our JS file where we will create variables and functions that will make everything work just right.

Let's check this out: 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>TO-DO List</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
  <script type="text/javascript" src="script.js"></script>
</body>
</html>

```

Now, let's create a text `input` box for typing in all those todo tasks, including an "Add" button:
```html
<!--index.html-->
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>TO-DO List</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <!--create a container for the todo list-->
    <div id="todo-container">
      <!--todo list header-->
      <div id="header">
        <h1>To Do List</h1>
      </div>

      <!--create input box-->
      <div id="todo-form">
        <input
          type="text"
          class="input-item"
          name="input_box"
          id="input-box"
          placeholder="Add Task"
        />

        <!-- Add button  -->
        <button id="input-button" onclick="addTask()">Add</button>
      </div>

       <!-- task list -->
      <h2>Task List</h2>
      <ul id="list-container"> </ul>
    </div>

    <script type="text/javascript" src="script.js"></script>
  </body>
</html>

```

- First, we make a `<div>` and give it an `id` of `"todo-container"`, to act as a container for our todo list.
- We create another `<div>` and give it an `id` of  `"header"`. Inside of the `<div>` we create an `<h1>` tag with the title `“To-Do List”`.
- Then, we use the `<input>` element for the new task in which the user writes the name of the task.
- We then create a `<button>` tag with an `id` of `“input-button”` for our `“Add”` button to add our task to the list.
- Right beneath that, we create an `<h2>` tag with the title `“Task List”`  along with a `<ul>` unordered list element, and give it an `id` of `"list-container"` this is where we will display each task.

Now, let’s take a look at our app in the browser. It should look something like this:

![alt text](/assets/images/input-box.png "Input-Box")

The button won’t work just yet. But don’t worry, we’ll get there!

## Task 2: Add Counter

Let's say we want to be able to calculate the number of task we have completed and the ones we have yet to get done. Let's make tracking our progress a bit simpler with counters for completed and uncompleted tasks.

Below your `<ul>` list container, add these lines of code: 
```html
 <hr />
     <!-- task list counter  -->
      <div class="counter-container">
        <div id="task-counters">
          Completed: <span id="completed-counter">0</span> | Uncompleted:
          <span id="uncompleted-counter">0</span>
        </div>
      </div>

```
**Note:** We added an `<hr />` tag (horizontal line), to create a separation between our list items and the task counters. This way, everything stays organized. 

Your application should now look like this: 


Let's take the next steps to activate our button, counter and add our first task to the list.

## Task 3: Add JavaScript

Let's kick things into high gear by add some JavaScript!

Above, we set up the structure for our todo list using HTML.Here, we're about to create a function that will let us seamlessly add our tasks to the list. Let's open our **script.js** file where we will first create two variables.

We will use these variables for our input and todo list container:

```js
const inputBox = document.getElementById("input-box");
const listContainer = document.getElementById("list-container");
```
**We used the special `document` object and its `getElementById()` method to select our input box and list container elements. Then we assigned them to the `inputBox` and `listContainer` variables.**

###  Add Your First List Item

Next, we will create our `addTask()` function! If a user forgets to type in a task and eagerly hits that "Add" button, a friendly alert message will pop up, reminding them to "Please write down a task":

```js
function addTask(){
  const task = inputBox.value.trim();
  if (!task) {
    alert("Please write down a task");
   return;
  }
}
```
Since we have already created a `<ul>` container in our HTML file to hold our list, let’s create a new list item with the `document` object's `createElement()` method:  

```js
const li = document.createElement("li");
```
Then we will we set up the HTML content of the list item:
```js
li.innerHTML = `
    <label>
    <input type="checkbox">
    <span>${task}</span>
  </label>
      <span class="edit-btn">Edit</span>
      <span class="delete-btn">Delete</span>
    `;

```
The inner HTML of our new task item includes:

- A checkbox-type `<input>`.
- The task content (using the `${task}` placeholder).
- "Edit" and "Delete" buttons that appear at the end of every task. 


To actually add the item to our list, we will need to use our `.appendChild()` method. This will add the newly created list item to the container specified by `listContainer`:

```js
listContainer.appendChild(li);
```

Open up your application inside your browser and test it out!
![alt text](/assets/images/add-task.gif "Add Task")

Great job! You've successfully added your first task.

However, you may have noticed that when we add a new task, it remains in the input box, requiring you to delete it before entering a new task. To fix this, we can add the following:
```js
 inputBox.value = "";
```

This line of code sets the value of the input field (`inputBox`) to an empty string, clearing the field after adding the task.

## Task 4: Activate Task Buttons
In the in code provided above, we created an `input` for a checkbox and a `span	` for our "Edit" and "Delete" buttons. Each task added to our list should allow us to manipulate it. Here's how each element functions:

- Checkbox: When the checkbox next to a task is selected, it strikes a line through the task and changes its color to gray, marking it "complete".
- Edit: Allows us to modify the task's content to something else.
- Delete: Removes a task from the list.

Using the `.querySelector()` method let’s create a variable for each of our elements:

```js
const checkbox = li.querySelector("input");
const editBtn = li.querySelector(".edit-btn");
const taskSpan = li.querySelector("span");
const deleteBtn = li.querySelector(".delete-btn");
```

**Note:** As you can see we have a `taskSpan` variable that allows us to edit a specific task when the edit button is clicked.

### Checkbox
```js
checkbox.addEventListener("click", function () {
    li.classList.toggle("completed", checkbox.checked);
      });
```

Here our `.addEventListener()` method is attached to the `“checkbox”` element. It will react to a click on the checkbox.
 
- We use the `classList.toggle()` to add the "completed" class to the list item `li`.
-  When the checkbox is checked (checkbox.checked is true), and removes the "completed" class if the checkbox is unchecked (checkbox.checked is now false).

Make sure to add this code to your **style.css** file:

```css
.completed {
   text-decoration: line-through;
  color: gray;
  border: 1px solid gray;
  }
```

### Edit Button

```js
  editBtn.addEventListener("click", function () {
   const update = prompt("Edit task:", taskSpan.textContent);
   if (update !== null) {
    taskSpan.textContent = update;
    li.classList.remove("completed");
   }
 });
```

In this code we attach an `.addEventListener()` method to our "Edit" button (editBtn). It responds to a click on the "Edit" button by executing the enclosed function.

- We are using the prompt function to display a dialog box asking the user to input a new task. The default value in the prompt is set to the current content of “taskSpan”.
- Then our if condition checks if the user has provided a new input. 
- If the user provides a new input, the content of the “taskSpan” will be updated which displays the task content with the new input.

Imagine this: one of our tasks, checked off as complete, but suddenly we're have the urge to edit and bring it back to the list. In this scenario, we need to strip away that "checked" styling. Let's make it happen: 

```js
    li.classList.remove("completed");
```
### Delete Button
 
```js
 deleteBtn.addEventListener("click", function () {
   if (confirm("Are you sure you want to delete this task?")) {
     li.remove();
   }
 });
```
As you can see above we also want to remove the task. If the task is not marked as completed you can delete it or keep it unchecked. When you go to delete the task an alert message will appear confirming if you want to delete the following task.

If the answer is yes it will proceed to the next line of code and delete the task with `remove()` method.