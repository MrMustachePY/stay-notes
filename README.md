
Certainly! Below is the simplified version of the code that combines everything into a single HTML file, with embedded CSS and JavaScript. You can copy and paste this into a single file:

html
Copier le code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Note Cacher</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 500px;
            width: 100%;
            background: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
        }
        .login-form, .note-form {
            display: none;
        }
        .login-form.active, .note-form.active {
            display: block;
        }
        input, textarea, button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            background-color: #007bff;
            color: #fff;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <form class="login-form active" id="loginForm">
            <h2>Login</h2>
            <input type="text" id="username" placeholder="Enter your name" required />
            <input type="password" id="password" placeholder="Enter your code" required />
            <button type="button" onclick="login()">Login</button>
        </form>
        <form class="note-form" id="noteForm">
            <h2>Your Notes</h2>
            <textarea id="note" placeholder="Write your note here..." rows="5"></textarea>
            <button type="button" onclick="saveNote()">Save Note</button>
            <h3>Saved Notes:</h3>
            <ul id="notesList"></ul>
        </form>
    </div>

    <script>
        const username = "Othmane";
        const password = "mama";

        const loginForm = document.getElementById("loginForm");
        const noteForm = document.getElementById("noteForm");
        const notesList = document.getElementById("notesList");

        function login() {
            const enteredUsername = document.getElementById("username").value;
            const enteredPassword = document.getElementById("password").value;

            if (enteredUsername === username && enteredPassword === password) {
                loginForm.classList.remove("active");
                noteForm.classList.add("active");
                loadNotes();
            } else {
                alert("Incorrect name or code!");
            }
        }

        function saveNote() {
            const note = document.getElementById("note").value;

            if (note.trim() !== "") {
                let notes = JSON.parse(localStorage.getItem("notes")) || [];
                notes.push(note);
                localStorage.setItem("notes", JSON.stringify(notes));
                document.getElementById("note").value = "";
                loadNotes();
            } else {
                alert("Note cannot be empty!");
            }
        }

        function loadNotes() {
            const notes = JSON.parse(localStorage.getItem("notes")) || [];
            notesList.innerHTML = "";
            notes.forEach((note, index) => {
                const li = document.createElement("li");
                li.textContent = note;
                notesList.appendChild(li);
            });
        }
    </script>
</body>
</html>
Explanation:
HTML: Contains the structure for the login form and notes interface.
CSS: Embedded styles within the <style> tag to make the page look neat.
JavaScript: Handles login, saving, and loading notes, using localStorage to persist data.
How it works:
On the initial load, the login form appears.
After successful login with the correct credentials (Othmane / mama), the user is shown the note-taking interface.
The notes are saved to localStorage so they persist even after the page is reloaded.
Notes are displayed in a list below the text area.
You can save this as an .html file and open it in your browser.