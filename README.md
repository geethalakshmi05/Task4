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




