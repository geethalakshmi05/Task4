<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Server Management</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Server Management</h1>
    <div class="form-container">
        <h2>Create Server</h2>
        <form id="create-form">
            <label for="name">Name:</label>
            <input type="text" id="name" required><br>
            <label for="id">ID:</label>
            <input type="text" id="id" required><br>
            <label for="language">Language:</label>
            <input type="text" id="language" required><br>
            <label for="framework">Framework:</label>
            <input type="text" id="framework" required><br>
            <button type="submit">Create Server</button>
        </form>
    </div>

    <div class="server-list">
        <h2>Server List</h2>
        <ul id="server-list"></ul>
    </div>

    <script src="app.js"></script>
</body>
</html>


body {
    font-family: Arial, sans-serif;
    margin: 20px;
}

.form-container, .server-list {
    margin-bottom: 20px;
}

form, ul {
    list-style-type: none;
    padding: 0;
}

label, input {
    display: block;
    margin-bottom: 10px;
}

button {
    background-color: #007bff;
    color: #fff;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

document.getElementById('create-form').addEventListener('submit', function(event) {
    event.preventDefault();

    let name = document.getElementById('name').value;
    let id = document.getElementById('id').value;
    let language = document.getElementById('language').value;
    let framework = document.getElementById('framework').value;

    fetch('http://localhost:8080/servers', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            "name": name,
            "id": id,
            "language": language,
            "framework": framework
        })
    })
    .then(response => response.json())
    .then(data => {
        alert('Server created successfully!');
        document.getElementById('create-form').reset();
        loadServerList();
    })
    .catch(error => console.error('Error:', error));
});

function loadServerList() {
    fetch('http://localhost:8080/servers')
    .then(response => response.json())
    .then(data => {
        let serverList = document.getElementById('server-list');
        serverList.innerHTML = '';

        data.forEach(server => {
            let li = document.createElement('li');
            li.textContent = `Name: ${server.name}, ID: ${server.id}, Language: ${server.language}, Framework: ${server.framework}`;

            let deleteButton = document.createElement('button');
            deleteButton.textContent = 'Delete';
            deleteButton.addEventListener('click', function() {
                deleteServer(server.id);
            });

            li.appendChild(deleteButton);
            serverList.appendChild(li);
        });
    })
    .catch(error => console.error('Error:', error));
}

function deleteServer(id) {
    fetch(`http://localhost:8080/servers/${id}`, {
        method: 'DELETE'
    })
    .then(response => {
        if (response.status === 200) {
            alert('Server deleted successfully!');
            loadServerList();
        } else {
            alert('Error deleting server. Server not found.');
        }
    })
    .catch(error => console.error('Error:', error));
}

loadServerList();



