# Zip-Code-Searcher-Node-Red [![platform](https://img.shields.io/badge/plataform-Node--RED-red)](https://nodered.org)
This project provides a ZIP code lookup system: a form where the user enters a ZIP code, a route that builds and sends an HTTP request to an external API, and an HTML response that displays the returned address data.

## 🚀 Overview
This project demonstrates two different ways of sending a code to the system:

### 🔹 1. Using Input Field
The user enters the code manually in a text box.
<p align="center">
  <img  src="/assets/zip code seacher.gif" alt="A gif showing the works of the Api" width="40%">
</p>

---
### 🔹 2. Using Route Parameter
The code is passed directly in the URL.
<p align="center">  
  <img  src="/assets/zip code seacher rota.gif" alt="A gif showing the works of the Api" width="60%">
</p>

## Installation
1. Install Node.js
Download it from the official website:
[Nodejs](https://nodejs.org/en)

   you can check the version using the command
  ```bash
  node --version
  ```
2.Install Node-RED

With Node.js installed, run:

```bash
npm install -g --unsafe-perm node-red
```

## Usage
1.Start Node-Red
  In the terminal:
  ```bash
  node-red
  ```
2.Then open the editor in your browser:
  http://localhost:1880
  or
  http://127.0.0.1:1880/

3.Importing the flow
 
   &nbsp;&nbsp;&nbsp;&nbsp;3.1. In the top-right corner of the screen, click the menu button (☰).
   
   &nbsp;&nbsp;&nbsp;&nbsp;3.2. Select Import from the dropdown menu.
   
   &nbsp;&nbsp;&nbsp;&nbsp;3.3. A text window will appear. Paste the file "zip code search flow.json"  that you did make the download.
   
   &nbsp;&nbsp;&nbsp;&nbsp;3.4. Click Import to load the flow into your workspace.
   
   &nbsp;&nbsp;&nbsp;&nbsp;3.5. Position the nodes as needed and then click Deploy to apply the changes.


## FLOW STRUCUTURE
This flow has two HTTP routes:
1. GET/zip-code-search
2. get/Address-by-zip


### Route zip-code-search
<img width="695" height="61" alt="Image" src="https://github.com/user-attachments/assets/caa7dc0c-8929-4717-85fa-cb85d66a58d3" /> 

1. get/zip-code-search
   
This node creates an HTTP route. When the browser accesses: http://127.0.0.1:1880/zip-code-search
The flow is triggered

3. Formulario cep
   
Here is the HTML that generates a page with an input field for entering the zip code.

```html
<html>
  <head>
    <title>Consultar CEP</title>
    <style>
      body { 
      font-family: Arial;
      background: #2f9fec;
      padding: 0px;
      display: flex;
      align-items: center;
      justify-content: center; 
      }
      form {
        background: white;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0,0,0,0.1);
        max-width: 400px;
        margin: auto;
      }
      input[type="text"] {
        padding: 10px;
        width: 90%;
        margin-bottom: 10px;
      }
      input[type="submit"] {
        padding: 10px 20px;
      }
    </style>
  </head>
  <body>
    {{!-- Direciona para url /consulta1  --}}
    <div class = cardcep> 
      <form action="/address-by-zip" method="get">
        <label>Digite o CEP:</label><br>
        <input type="text" name="formcep" id="cep" maxlength="9" placeholder="00000-000">
        <input type="submit" value="Buscar">
      </form>
    </div>
    <p>{{numCep}}</p>
      <script>
      const cepInput = document.getElementById('cep');

      cepInput.addEventListener('input', function () {
        let value = this.value.replace(/\D/g, ''); // Remove everything that is not numbers
        if (value.length > 5) {
          value = value.slice(0, 5) + '-' + value.slice(5, 8);
        }
        this.value = value;
      });
    </script>
  </body>
</html>
```

3. HTTP response
sends the HTML to the browser

