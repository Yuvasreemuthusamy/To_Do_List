# Ex03 To-Do List using JavaScript
## Date: 12.05.2026

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
# index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>My To-Do App</title>

  <style>

    *{
      margin:0;
      padding:0;
      box-sizing:border-box;
    }

    body{
      font-family: "Poppins", sans-serif;
      background:#000;
      display:flex;
      justify-content:center;
      align-items:center;
      min-height:100vh;
      color:white;
      padding:20px;
    }

    .todo-container{
      width:450px;
      background:#161616;
      padding:30px;
      border-radius:22px;
      box-shadow:0 0 35px rgba(132,0,255,0.45);
    }

    h1{
      text-align:center;
      color:#b066ff;
      font-size:28px;
      margin-bottom:10px;
      text-shadow:0 0 12px #8a2eff;
    }

    .subtitle{
      text-align:center;
      color:#ddd;
      margin-bottom:22px;
      font-size:14px;
    }

    .instructions{
      background:#232323;
      padding:16px;
      border-radius:14px;
      margin-bottom:22px;
      color:#d0d0d0;
      font-size:14px;
      line-height:2;
    }

    .input-section{
      display:flex;
      gap:10px;
      margin-bottom:18px;
    }

    input{
      flex:1;
      padding:14px;
      border-radius:12px;
      border:2px solid #333;
      background:#0d0d0d;
      color:white;
      font-size:15px;
      outline:none;
      transition:0.3s;
    }

    input:focus{
      border-color:#a259ff;
      box-shadow:0 0 10px rgba(162,89,255,0.8);
    }

    .add-btn{
      border:none;
      padding:14px 18px;
      border-radius:12px;
      background:linear-gradient(135deg,#7d3cff,#a259ff);
      color:white;
      font-weight:bold;
      cursor:pointer;
      transition:0.3s;
      box-shadow:0 0 15px rgba(162,89,255,0.8);
    }

    .add-btn:hover{
      transform:scale(1.05);
    }

    #taskCounter{
      text-align:center;
      margin-bottom:25px;
      font-weight:bold;
      color:#f0f0f0;
      font-size:16px;
    }

    h2{
      color:#b066ff;
      font-size:18px;
      margin-bottom:15px;
      text-shadow:0 0 8px #8a2eff;
    }

    ul{
      list-style:none;
      margin-bottom:20px;
    }

    li{
      background:#262626;
      padding:14px;
      margin-bottom:14px;
      border-radius:12px;
      display:flex;
      justify-content:space-between;
      align-items:center;
      border-left:4px solid #a259ff;
      transition:0.3s;
    }

    li:hover{
      background:#2f2f2f;
    }

    li.completed{
      text-decoration:line-through;
      color:#999;
      border-left:4px solid gray;
      opacity:0.8;
    }

    .actions{
      display:flex;
      gap:8px;
    }

    .actionBtn{
      border:none;
      width:32px;
      height:32px;
      border-radius:8px;
      cursor:pointer;
      font-size:16px;
      background:#1c1c1c;
      transition:0.3s;
    }

    .actionBtn:hover{
      transform:scale(1.1);
    }

    .completeBtn{
      color:#00ffbf;
      box-shadow:0 0 10px rgba(0,255,191,0.7);
    }

    .deleteBtn{
      color:#ff4d6d;
      box-shadow:0 0 10px rgba(255,77,109,0.7);
    }

    footer{
      text-align:center;
      margin-top:20px;
      color:#999;
      font-size:13px;
      line-height:2;
    }

  </style>
</head>

<body>

  <div class="todo-container">

    <h1>✨ My To-Do App ✨</h1>

    <p class="subtitle">
      Stay productive, stay organized 💪
    </p>

    <div class="instructions">
      <p>➡️ Type your task in the box below and click <b>Add</b>.</p>
      <p>✔️ Click on a task to mark it as <b>completed</b>.</p>
      <p>❌ Use delete button to remove unwanted tasks.</p>
    </div>

    <div class="input-section">

      <input
        type="text"
        id="taskInput"
        placeholder="Enter a new task..."
      >

      <button class="add-btn" onclick="addTask()">
        ➕ Add
      </button>

    </div>

    <p id="taskCounter">
      You have <span>0</span> pending tasks 📝
    </p>

    <h2>📂 Today’s Tasks</h2>

    <ul id="taskList"></ul>

    <h2>✅ Completed Tasks</h2>

    <ul id="completedList"></ul>

    <footer>
      <p>💡 Pro Tip: Break big goals into small steps!</p>
      <p>Made with ❤️ using HTML, CSS & JavaScript</p>
    </footer>

  </div>

  <script>

    const taskInput =
      document.getElementById("taskInput");

    const taskList =
      document.getElementById("taskList");

    const completedList =
      document.getElementById("completedList");

    const taskCounter =
      document.querySelector("#taskCounter span");


    function updateCounter(){

      taskCounter.textContent =
        taskList.children.length;

    }


    function addTask(){

      const taskText =
        taskInput.value.trim();

      if(taskText === ""){

        alert("Please enter a task!");

        return;
      }

      const li =
        document.createElement("li");

      const taskSpan =
        document.createElement("span");

      taskSpan.textContent = taskText;


      const actions =
        document.createElement("div");

      actions.classList.add("actions");


      const completeBtn =
        document.createElement("button");

      completeBtn.innerHTML = "✔️";

      completeBtn.classList.add(
        "actionBtn",
        "completeBtn"
      );


      completeBtn.onclick = () => {

        li.classList.add("completed");

        completedList.appendChild(li);

        completeBtn.remove();

        updateCounter();
      };


      const deleteBtn =
        document.createElement("button");

      deleteBtn.innerHTML = "❌";

      deleteBtn.classList.add(
        "actionBtn",
        "deleteBtn"
      );


      deleteBtn.onclick = () => {

        li.remove();

        updateCounter();
      };


      actions.appendChild(completeBtn);

      actions.appendChild(deleteBtn);


      li.appendChild(taskSpan);

      li.appendChild(actions);


      taskList.appendChild(li);


      taskInput.value = "";


      updateCounter();
    }


    updateCounter();

  </script>

</body>
</html>
```

## OUTPUT
<img width="1904" height="930" alt="image" src="https://github.com/user-attachments/assets/922db514-f631-4c89-bf6f-0ae160c4ec63" />


## RESULT
The program for creating To-do list using JavaScript is executed successfully.
