# Zip-Code-Searcher-Node-Red [![platform](https://img.shields.io/badge/plataform-Node--RED-red)](https://nodered.org)
Node-RED flow that provides a ZIP code lookup system: a form where the user enters a ZIP code, a route that builds and sends an HTTP request to an external API, and an HTML response that displays the returned address data.

## 🚀 Overview
This project demonstrates two different ways of sending a code to the system:

## 🔹 1. Using Input Field
The user enters the code manually in a text box.
<p align="center">
  <img  src="/assets/zip code seacher.gif" alt="A gif showing the works of the Api" width="40%">
</p>

## 🔹 2. Using Route Parameter
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


