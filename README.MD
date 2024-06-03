1. JSON Array Object

[
{
"id": 1,
"name": "John Doe",
"email": "john@example.com"
},
{
"id": 2,
"name": "Jane Smith",
"email": "jane@example.com"
}
]

2. C# Code to Display and Update a Label

using System;
using System.Windows.Forms;
using Newtonsoft.Json.Linq;

public class MainForm : Form
{
private Label label;
private Button button;
private JArray jsonArray;

    public MainForm()
    {
        jsonArray = JArray.Parse(@"[
            { 'id': 1, 'name': 'John Doe', 'email': 'john@example.com' },
            { 'id': 2, 'name': 'Jane Smith', 'email': 'jane@example.com' }
        ]");

        label = new Label() { Location = new System.Drawing.Point(10, 10), Width = 300 };
        button = new Button() { Text = "Change Label", Location = new System.Drawing.Point(10, 40) };

        button.Click += (sender, args) => {
            label.Text = jsonArray[0]["name"].ToString();
        };

        this.Controls.Add(label);
        this.Controls.Add(button);
    }

    [STAThread]
    public static void Main()
    {
        Application.Run(new MainForm());
    }

}

3. HTTP Request and Response Logging

using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
public static async Task Main(string[] args)
{
using (HttpClient client = new HttpClient())
{
HttpResponseMessage response = await client.GetAsync("http://jsonplaceholder.typicode.com/posts");
string responseBody = await response.Content.ReadAsStringAsync();
Console.WriteLine(responseBody);
}
}
}

4. HTML to Display Response in a Table

<!DOCTYPE html>
<html>
<head>
    <title>HTTP Response Table</title>
</head>
<body>
    <table id="responseTable" border="1">
        <thead>
            <tr>
                <th>ID</th>
                <th>Title</th>
                <th>Body</th>
            </tr>
        </thead>
        <tbody>
        </tbody>
    </table>
    <script>
        fetch('http://jsonplaceholder.typicode.com/posts')
            .then(response => response.json())
            .then(data => {
                const tableBody = document.getElementById('responseTable').getElementsByTagName('tbody')[0];
                data.slice(0, 10).forEach(item => {
                    const row = tableBody.insertRow();
                    row.insertCell(0).innerText = item.id;
                    row.insertCell(1).innerText = item.title;
                    row.insertCell(2).innerText = item.body;
                });
            });
    </script>
</body>
</html>

5. Function to Delete a Row in the Table

<script>
    function deleteRow(id) {
        const table = document.getElementById('responseTable').getElementsByTagName('tbody')[0];
        for (let i = 0; i < table.rows.length; i++) {
            if (table.rows[i].cells[0].innerText == id) {
                table.deleteRow(i);
                break;
            }
        }
    }
</script>

6. Remove a Key from JSON Response

fetch('http://jsonplaceholder.typicode.com/posts')
.then(response => response.json())
.then(data => {
data.forEach(item => {
delete item.userId; // Remove the userId key
});
console.log(data); // Log the modified data
});

7. SHA-256 Hashing Function

using System;
using System.Security.Cryptography;
using System.Text;

public class Program
{
public static void Main(string[] args)
{
string input = "01112018kenpriaifabula";
string hash = ComputeSha256Hash(input);
Console.WriteLine(hash);
}

    public static string ComputeSha256Hash(string rawData)
    {
        using (SHA256 sha256Hash = SHA256.Create())
        {
            byte[] bytes = sha256Hash.ComputeHash(Encoding.UTF8.GetBytes(rawData));
            StringBuilder builder = new StringBuilder();
            foreach (byte b in bytes)
            {
                builder.Append(b.ToString("x2"));
            }
            return builder.ToString();
        }
    }

}

8. Debugging HTML

<!DOCTYPE html>
<html>
<head>
    <title>Test Debug</title>
</head>
<body>
    <p id="demo">This is a demonstration.</p>
    <button onclick="myFunction()">Click me</button>

    <script>
        function myFunction() {
            document.getElementById("demo").innerHTML = "Hello World!";
        }
    </script>

</body>
</html>

9. Login Page with Local Storage

<!DOCTYPE html>
<html>
<head>
    <title>Login Page</title>
    <script>
        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            localStorage.setItem('username', username);
            localStorage.setItem('password', password);
            document.getElementById('loginForm').style.display = 'none';
            document.getElementById('welcome').style.display = 'block';
            document.getElementById('welcomeMessage').innerText = `Selamat datang ${username}`;
        }

        function logout() {
            localStorage.removeItem('username');
            localStorage.removeItem('password');
            document.getElementById('loginForm').style.display = 'block';
            document.getElementById('welcome').style.display = 'none';
        }

        window.onload = function() {
            if (localStorage.getItem('username')) {
                document.getElementById('loginForm').style.display = 'none';
                document.getElementById('welcome').style.display = 'block';
                document.getElementById('welcomeMessage').innerText = `Selamat datang ${localStorage.getItem('username')}`;
            }
        }
    </script>

</head>
<body>
    <div id="loginForm">
        <input type="text" id="username" placeholder="Username">
        <input type="password" id="password" placeholder="Password">
        <button onclick="login()">Login</button>
    </div>
    <div id="welcome" style="display: none;">
        <label id="welcomeMessage">Selamat datang</label>
        <button onclick="logout()">Logout</button>
    </div>
</body>
</html>

10. Node.js Project with Express

const express = require('express');
const app = express();
app.use(express.json());

app.get('/api/data', (req, res) => {
res.json({ message: 'GET request received' });
});

app.post('/api/data', (req, res) => {
res.json({ message: 'POST request received', data: req.body });
});

app.listen(3000, () => {
console.log('Server is running on port 3000');
});

11. Add Headers and Validation in Express API

const express = require('express');
const app = express();
app.use(express.json());

app.use((req, res, next) => {
const userId = req.header('User-id');
const scope = req.header('Scope');
if (userId !== 'ifabula' || scope !== 'user') {
return res.status(401).json({ responseCode: 401, responseMessage: 'UNAUTHORIZED' });
}
next();
});

app.get('/api/data', (req, res) => {
res.json({ message: 'GET request received' });
});

app.post('/api/data', (req, res) => {
res.json({ message: 'POST request received', data: req.body });
});

app.listen(3000, () => {
console.log('Server is running on port 3000');
});
