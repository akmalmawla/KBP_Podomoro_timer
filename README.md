# KBP_Podomoro_timer
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Pomodoro Timer & To-Do List</title>
    <style>
      body {
        font-family: "Courier New", Courier, monospace;
        margin: 0;
        padding: 0;
        background: linear-gradient(135deg, #2c3e50, #4ca1af);
        color: #fff;
        display: flex;
        flex-direction: column;
        align-items: center;
        min-height: 100vh;
      }
      header h1 {
        color: aquamarine;
        line-height: 15px;
      }

      header,
      footer {
        background: #34495e;
        color: white;
        text-align: center;
        padding: 15px 10px;
        width: 100%;
        max-width: 1200px;
        font-size: 1.8rem;
        font-weight: bold;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        margin: 0 auto;
        border-radius: 10px;
      }

      header {
        margin-bottom: 20px;
      }

      footer {
        margin-top: 20px;
      }

      .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 100%;
        max-width: 1200px;
        padding: 20px;
      }

      .spotify {
        margin: 20px 0;
        width: 100%;
        text-align: center;
        background: #3b6978;
        padding: 10px;
        border-radius: 15px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 10);
      }

      .spotify iframe {
        border-radius: 10px;
        border: none;
        width: 80%;
        height: 80px;
      }

      .main-content {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-gap: 20px;
        width: 100%;
      }

      .column {
        background: #2e3b4e;
        border-radius: 15px;
        padding: 20px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
      }

      .column h3 {
        text-align: center;
        margin-bottom: 15px;
        color: #4ca1af;
      }

      .motivation {
        text-align: center;
        font-size: 1.2rem;
        color: #fff;
        line-break: anywhere;
      }

      ul {
        list-style: none;
        padding: 0;
      }

      ul li {
        background: #3a4750;
        padding: 15px;
        margin: 10px 0;
        border-radius: 10px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
      }

      ul li.done {
        text-decoration: line-through;
        color: #888;
      }

      ul li span.date {
        font-size: 0.9rem;
        color: #4ca1af;
      }

      button {
        background: #4ca1af;
        color: white;
        border: none;
        border-radius: 10px;
        padding: 10px 15px;
        cursor: pointer;
        transition: background 0.3s;
        font-size: 1rem;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
      }
      button .buttonmotiv button:hover {
        background: #2c3e50;
      }

      input[type="text"],
      input[type="number"],
      input[type="date"] {
        width: calc(100% - 30px);
        padding: 10px;
        margin: 10px 0;
        border: 2px solid #4ca1af;
        border-radius: 10px;
        outline: none;
        font-size: 1rem;
        background: #3a4750;
        color: white;
      }

      input[type="text"]::placeholder {
        color: #bbb;
      }
    </style>
  </head>
  <body>
    <header>
      <h1>Pomodoro</h1>
      Timer & To-Do List
    </header>

    <div class="spotify">
      <h1>Spotify Album</h1>
      <p>
        Penis penis apa yang bikin sakit.?<br />
        Pain is Never Permanent But Tonight Is Killing Me
      </p>
      <iframe
        style="border-radius: 12px"
        src="https://open.spotify.com/embed/artist/2TM0qnbJH4QPhGMCdPt7fH?utm_source=generator"
        width="100%"
        height="352"
        frameborder="0"
        allowfullscreen=""
        allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
        loading="lazy"
      ></iframe>
    </div>

    <div class="main-content">
      <div class="column">
        <h3>Pomodoro Timer</h3>
        <label for="study-time">Study Time (minutes): </label>
        <input type="number" id="study-time" value="25" />

        <label for="break-time">Break Time (minutes): </label>
        <input type="number" id="break-time" value="5" />

        <button onclick="startTimer()">Start Timer</button>
        <h2 id="countdown">00:00</h2>
      </div>

      <div class="column">
        <h3>To-Do List</h3>
        <div>
          <input type="text" id="new-task" placeholder="Add a new task" />
          <input type="date" id="deadline" />
          <button onclick="addTask()">Add Task</button>
        </div>
        <ul id="task-list"></ul>
      </div>

      <div class="column">
        <h3>Motivational Quotes</h3>
        <div class="motivation" id="motivation-box">
          "Stay positive, work hard, make it happen!"
        </div>
        <button id="buttonmotiv" onclick="generateQuote()">
          Get New Quote
        </button>
      </div>
    </div>

    <footer>Semangat lah cui.! Soalny klok pengen beras masih kdu bayar</footer>

    <script>
      const quotes = [
        "Djadji lah radja djawa",
        "Hey bro, ur code won't code by it self",
        "Intinya ini motivasi yak, semoga para hadirin semua ter motivasi",
        "Djangan takud gagal, Takudlah ketika ada teman ngajak mabar saat ngoding",
        "Madju Ksadria Kegelapan, Dingin Tetapi tidak kejam, Hey hey hey lihat aku di sini, Aku Bluetooth Cih Tydak akan.",
      ];

      function generateQuote() {
        const randomIndex = Math.floor(Math.random() * quotes.length);
        document.getElementById("motivation-box").textContent =
          quotes[randomIndex];
      }

      document.addEventListener("DOMContentLoaded", generateQuote);

      let timerInterval;

      function startTimer() {
        const studyTime =
          parseInt(document.getElementById("study-time").value) * 60;
        const breakTime =
          parseInt(document.getElementById("break-time").value) * 60;
        let timeRemaining = studyTime;
        let onBreak = false;

        function updateCountdown() {
          const minutes = Math.floor(timeRemaining / 60);
          const seconds = timeRemaining % 60;
          document.getElementById("countdown").textContent = `${minutes
            .toString()
            .padStart(2, "0")}:${seconds.toString().padStart(2, "0")}`;
        }

        clearInterval(timerInterval);
        timerInterval = setInterval(() => {
          if (timeRemaining > 0) {
            timeRemaining--;
            updateCountdown();
          } else {
            if (!onBreak) {
              timeRemaining = breakTime;
              onBreak = true;
              alert("Break time! Time to relax.");
            } else {
              timeRemaining = studyTime;
              onBreak = false;
              alert("Back to work!");
            }
          }
        }, 1000);
        updateCountdown();
      }

      function addTask() {
        const taskInput = document.getElementById("new-task");
        const deadlineInput = document.getElementById("deadline");

        const task = taskInput.value.trim();
        const deadline = deadlineInput.value;

        if (task === "") {
          alert("Please enter a task.");
          return;
        }

        const taskList = document.getElementById("task-list");
        const listItem = document.createElement("li");

        const taskText = document.createElement("span");
        taskText.textContent = task;

        const dateText = document.createElement("span");
        dateText.textContent = deadline ? ` (Due: ${deadline})` : "";
        dateText.classList.add("date");

        const doneButton = document.createElement("button");
        doneButton.textContent = "Done";
        doneButton.onclick = () => {
          listItem.classList.toggle("done");
        };

        const deleteButton = document.createElement("button");
        deleteButton.textContent = "Delete";
        deleteButton.onclick = () => {
          taskList.removeChild(listItem);
          saveTasks();
        };

        listItem.appendChild(taskText);
        listItem.appendChild(dateText);
        listItem.appendChild(doneButton);
        listItem.appendChild(deleteButton);
        taskList.appendChild(listItem);

        taskInput.value = "";
        deadlineInput.value = "";

        saveTasks();
      }

      function saveTasks() {
        const taskList = document.getElementById("task-list");
        const tasks = [];
        taskList.querySelectorAll("li").forEach((li) => {
          tasks.push({
            text: li.querySelector("span").textContent,
            date: li.querySelector(".date").textContent,
            done: li.classList.contains("done"),
          });
        });
        localStorage.setItem("tasks", JSON.stringify(tasks));
      }

      function loadTasks() {
        const taskList = document.getElementById("task-list");
        const tasks = JSON.parse(localStorage.getItem("tasks")) || [];

        tasks.forEach(({ text, date, done }) => {
          const listItem = document.createElement("li");

          const taskText = document.createElement("span");
          taskText.textContent = text;

          const dateText = document.createElement("span");
          dateText.textContent = date;
          dateText.classList.add("date");

          const doneButton = document.createElement("button");
          doneButton.textContent = "Done";
          doneButton.onclick = () => {
            listItem.classList.toggle("done");
            saveTasks();
          };

          const deleteButton = document.createElement("button");
          deleteButton.textContent = "Delete";
          deleteButton.onclick = () => {
            taskList.removeChild(listItem);
            saveTasks();
          };

          if (done) {
            listItem.classList.add("done");
          }

          listItem.appendChild(taskText);
          listItem.appendChild(dateText);
          listItem.appendChild(doneButton);
          listItem.appendChild(deleteButton);
          taskList.appendChild(listItem);
        });
      }

      document.addEventListener("DOMContentLoaded", loadTasks);
    </script>
  </body>
</html>
