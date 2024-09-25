# EX01 Developing a Simple Webserver
## Date:
25/09/2024
## AIM:
To develop a simple webserver to serve html pages and display the configuration details of laptop.

## DESIGN STEPS:
### Step 1: 
HTML content creation.

### Step 2:
Design of webserver workflow.

### Step 3:
Implementation using Python code.

### Step 4:
Serving the HTML pages.

### Step 5:
Testing the webserver.

## PROGRAM:
```
from flask import Flask, render_template_string
import platform
import psutil
import socket

app = Flask(__name__)

def get_system_info():
    return {
        "Operating System": platform.system(),
        "OS Version": platform.version(),
        "Machine": platform.machine(),
        "Processor": platform.processor(),
        "CPU Cores (Logical)": psutil.cpu_count(logical=True),
        "CPU Cores (Physical)": psutil.cpu_count(logical=False),
        "Total RAM (GB)": round(psutil.virtual_memory().total / (1024 ** 3), 2),
        "Used RAM (GB)": round(psutil.virtual_memory().used / (1024 ** 3), 2),
        "Available RAM (GB)": round(psutil.virtual_memory().available / (1024 ** 3), 2),
        "Disk Usage": f"{psutil.disk_usage('/').percent}%",
        "IP Address": socket.gethostbyname(socket.gethostname())
    }

@app.route('/')
def index():
    system_info = get_system_info()
    html_template = """
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>System Configuration</title>
        <style>
            body { font-family: Arial, sans-serif; background-color: #f4f4f9; padding: 20px; }
            table { width: 50%; margin: auto; border-collapse: collapse; }
            th, td { padding: 10px; text-align: left; border: 1px solid #ddd; }
            th { background-color: #333; color: white; }
            td { background-color: #fff; }
        </style>
    </head>
    <body>
        <h1 style="text-align: center;">Laptop Configuration Details</h1>
        <table>
            <tr>
                <th>Component</th>
                <th>Details</th>
            </tr>
            {% for key, value in system_info.items() %}
            <tr>
                <td>{{ key }}</td>
                <td>{{ value }}</td>
            </tr>
            {% endfor %}
        </table>
    </body>
    </html>
    """
    return render_template_string(html_template, system_info=system_info)

if __name__ == '__main__':
    app.run(debug=True)
```

## OUTPUT:
![Screenshot (95)](https://github.com/user-attachments/assets/6c898a5d-5a8d-4d7c-8b58-65171fa47739)


## RESULT:
The program for implementing simple webserver is executed successfully.
