# Zip-Code-Searcher-Node-Red [![platform](https://img.shields.io/badge/plataform-Node--RED-red)](https://nodered.org)
This project provides a ZIP code lookup system: a form where the user enters a ZIP code, a route that builds and sends an HTTP request to an external API, and an HTML response that displays the returned address data.

## Table of contents
- [Overview](#Overview)
- [Using Input Field](#Using-Input-Field)
- [Using Route Parameter](#Using-Route-Parameter)
- [Installation](#installation)
- [Usage](#Usage)
- [Flow Structure](#Flow-Structure)
- [Route zip-code-search](#Route-zip-code-search)
- [get/Address-by-zip](#get/Address-by-zip)


## Overview
This project demonstrates two different ways of sending a code to the system:

### Using Input Field
The user enters the code manually in a text box.

<p align="center">
  <img  src="/assets/zip code seacher.gif" alt="A gif showing the works of the Api" width="40%">
</p>

---
### Using Route Parameter
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

--- 
## Route Address-by-zip

<img width="1067" height="320" alt="Image" src="https://github.com/user-attachments/assets/866e35f5-9ea1-4c2b-b9b4-79e096ccea45" />

### get/Address-by-zip

Receives the ZIP code entered by the user via query string:

### Monta URL (function)
This node takes the ZIP code received and builds the query API URL.
Probably something like this:

### requisição HTTP
Uses the built URL and calls the external API.

It generates a msg.payload with the API return (JSON).

### Retorno HTML 

This node takes the received JSON and transforms it into HTML to send to the browser.

### HTTP Response
Sends this HTML page to the browser.

Result: the user sees the ZIP code data on the screen.

## Auxiliary nodes
<img width="448" height="183" alt="Image" src="https://github.com/user-attachments/assets/1ffe5421-06b8-41e4-a5f8-127fa3531724" />


They receive the same return from the HTTP request:

1. Generate URL (function)

&nbsp;&nbsp;&nbsp;&nbsp;Used only for debugging, displaying the URL used (msg.url).


2. Debug numCep (function)

&nbsp;&nbsp;&nbsp;&nbsp;Also for debugging, probably shows the ZIP code received (msg.numCep).


3. Request return (debug)

&nbsp;&nbsp;&nbsp;&nbsp;Shows the JSON received from the API in the debug panel
