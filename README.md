<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
    <link rel="stylesheet" href="style.css">
</head>
<style>
    body {
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif, sans-serif;
        background-color: #ecdbdf;
    }
    
    header {
        background-color: #8bb4f3;
        color: #fff;
        padding: 1em;
        text-align: center;
    }
    
    main {
        max-width: 600px;
        margin: 2em auto;
        padding: 2em;
        background-color: #fff;
        border: 1px solid #ddd;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    
    #task-input {
        width: 100%;
        padding: 1em;
        margin-bottom: 1em;
        border: 1px solid #ccc;
    }
    
    #add-task-btn {
        background-color: #4CAF50;
        color: #fff;
        padding: 1em 2em;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
    
    #task-list {
        list-style: none;
        padding: 0;
        margin: 0;
    }
    
    #task-list li {
        padding: 0.5em;
        border-bottom: 0.5px solid #141414;
    }
    
    #task-list li:last-child {
        border-bottom: none;
    }
    
    #task-list li.done {
        text-decoration: line-through;
    }
    </style>
<body>
    <header>
        <h1>To-Do List</h1>
    </header>
    <main>
        <input type="text" id="task-input" placeholder="Add new task...">
        <button id="add-task-btn">Add Task</button>
        <ul id="task-list"></ul>
    </main>
    <script src="script.js"></script>
    <script>const taskInput = document.getElementById('task-input');
        const addTaskBtn = document.getElementById('add-task-btn');
        const taskList = document.getElementById('task-list');
        
        addTaskBtn.addEventListener('click', addTask);
        
        function addTask() {
            const taskText = taskInput.value.trim();
            if (taskText) {
                const taskListItem = document.createElement('LI');
                taskListItem.textContent = taskText;
                taskList.appendChild(taskListItem);
                taskInput.value = '';
                taskListItem.addEventListener('click', toggleDone);
            }
        }
        
        function toggleDone(event) {
            event.target.classList.toggle('done');
        }
        
        // Load existing tasks from local storage (if any)
        const storedTasks = localStorage.getItem('tasks');
        if (storedTasks) {
            const tasks = JSON.parse(storedTasks);
            tasks.forEach(task => {
                const taskListItem = document.createElement('LI');
                taskListItem.textContent = task;
                taskList.appendChild(taskListItem);
            });
        }
        
        // Save tasks to local storage when added or removed
        taskList.addEventListener('change', saveTasks);
        
        function saveTasks() {
            const tasks = Array.from(taskList.children).map(task => task.textContent);
            localStorage.setItem('tasks', JSON.stringify(tasks));
        }</script>
</body>
</html>
