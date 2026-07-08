# Atividade III: Criando página de Back-end para integração

### Objetivo Geral
Desenvolver um servidor web utilizando **Node.js** com o framework **Express** e o motor de templates **EJS** para renderizar dinamicamente o seu portfólio/currículo profissional. O objetivo principal é centralizar todos os seus dados (cursos e certificações) em um único objeto JavaScript estruturado (`db`) e fazer com que o servidor injete essas informações automaticamente em uma única página HTML, eliminando a necessidade de duplicar código estático manualmente para cada novo item adicionado.

### 1. Servidor Express (Endpoint `/`)
Gerencia a rota raiz e renderiza o HTML.
```javascript
const express = require('express');
const app = express();

app.set('view engine', 'ejs');

app.get('/', (req, res) => {
    res.render('portfolio', { dados: db }); // Item 4: Passagem de Argumentos
});

app.listen(3000);
```

### 2. Template Engine (EJS)
Mistura HTML com JavaScript. O servidor gera HTML puro.
* `<%= valor %>`: Exibe dados.
* `<% código %>`: Executa lógica (loops/condicionais).
* **Referência:** [ejs.co](https://ejs.co)

### 3. Objeto de Dados (`db`)
Armazena as informações estruturadas do aluno.
```javascript
const db = {
    cursos: [
        { nome: "Node.js", horas: "40h" },
        { nome: "React", horas: "30h" }
    ],
    certificados: [
        { titulo: "Full Stack", ano: 2025 },
        { titulo: "Scrum Master", ano: 2026 }
    ]
};
```

### 4. Passagem de Argumentos
Envia o objeto `db` para o EJS através da chave `dados` dentro de `res.render('portfolio', { dados: db })`.

### 5. Renderização Dinâmica (`portfolio.ejs`)
Usa a variável `dados` e loops para criar o HTML automaticamente.
```html
<h2>Meus Cursos</h2>
<ul>
    <% dados.cursos.forEach(curso => { %>
        <li><%= curso.nome %> - <%= curso.horas %></li>
    <% }); %>
</ul>

<h2>Certificados</h2>
<ul>
    <% dados.certificados.forEach(cert => { %>
        <li><%= cert.titulo %> (<%= cert.ano %>)</li>
    <% }); %>
</ul>
```
