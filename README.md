<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Nintendo Switch - Cadastro de Cliente</title>

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f2f2f2;
    }

    header {
      background: #e60012;
      color: white;
      text-align: center;
      padding: 25px;
    }

    nav {
      background: #111;
      padding: 15px;
      text-align: center;
    }

    nav a {
      color: white;
      text-decoration: none;
      margin: 12px;
      font-weight: bold;
    }

    nav a:hover {
      color: #e60012;
    }

    .container {
      width: 90%;
      max-width: 1000px;
      margin: 30px auto;
      background: white;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 0 10px #ccc;
    }

    h2 {
      color: #e60012;
      text-align: center;
    }

    label {
      font-weight: bold;
    }

    input, select {
      width: 100%;
      padding: 12px;
      margin: 8px 0 15px;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 15px;
    }

    button {
      padding: 10px 15px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
      margin: 4px;
    }

    .btn-salvar {
      width: 100%;
      background: #e60012;
      color: white;
      font-size: 16px;
    }

    .btn-salvar:hover {
      background: #111;
    }

    .btn-editar {
      background: #ffc107;
      color: black;
    }

    .btn-excluir {
      background: #dc3545;
      color: white;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 25px;
    }

    th {
      background: #e60012;
      color: white;
      padding: 12px;
    }

    td {
      border: 1px solid #ccc;
      padding: 10px;
      text-align: center;
    }

    footer {
      background: #111;
      color: white;
      text-align: center;
      padding: 15px;
      margin-top: 30px;
    }
  </style>
</head>

<body>

<header>
  <h1>Nintendo Switch</h1>
  <p>Sistema de Cadastro de Clientes</p>
</header>

<nav>
  <a href="#cadastro">Cadastrar Cliente</a>
  <a href="#lista">Lista de Clientes</a>
</nav>

<div class="container" id="cadastro">
  <h2>Cadastrar Cliente</h2>

  <input type="hidden" id="indice">

  <label>Nome:</label>
  <input type="text" id="nome" placeholder="Digite o nome do cliente">

  <label>Email:</label>
  <input type="email" id="email" placeholder="Digite o email">

  <label>Telefone:</label>
  <input type="text" id="telefone" placeholder="Digite o telefone">

  <label>CPF:</label>
  <input type="text" id="cpf" placeholder="Digite o CPF">

  <label>Produto favorito:</label>
  <select id="produto">
    <option value="">Selecione</option>
    <option>Nintendo Switch</option>
    <option>Nintendo Switch OLED</option>
    <option>Nintendo Switch Lite</option>
    <option>Mario Kart 8 Deluxe</option>
    <option>Zelda Tears of the Kingdom</option>
    <option>Super Mario Odyssey</option>
    <option>Pro Controller</option>
    <option>Joy-Con</option>
  </select>

  <button class="btn-salvar" onclick="salvarCliente()">Cadastrar Cliente</button>
</div>

<div class="container" id="lista">
  <h2>Clientes Cadastrados</h2>

  <table>
    <thead>
      <tr>
        <th>Nome</th>
        <th>Email</th>
        <th>Telefone</th>
        <th>CPF</th>
        <th>Produto Favorito</th>
        <th>Ações</th>
      </tr>
    </thead>

    <tbody id="tabelaClientes"></tbody>
  </table>
</div>

<footer>
  <p>Site Nintendo Switch - Cadastro de Clientes</p>
</footer>

<script>
  let clientes = [];

  function salvarCliente() {
    let indice = document.getElementById("indice").value;
    let nome = document.getElementById("nome").value;
    let email = document.getElementById("email").value;
    let telefone = document.getElementById("telefone").value;
    let cpf = document.getElementById("cpf").value;
    let produto = document.getElementById("produto").value;

    if (nome === "" || email === "" || telefone === "" || cpf === "" || produto === "") {
      alert("Preencha todos os campos!");
      return;
    }

    let cliente = {
      nome: nome,
      email: email,
      telefone: telefone,
      cpf: cpf,
      produto: produto
    };

    if (indice === "") {
      clientes.push(cliente);
      alert("Cliente cadastrado com sucesso!");
    } else {
      clientes[indice] = cliente;
      document.getElementById("indice").value = "";
      alert("Cliente editado com sucesso!");
    }

    limparCampos();
    listarClientes();
  }

  function listarClientes() {
    let tabela = document.getElementById("tabelaClientes");
    tabela.innerHTML = "";

    clientes.forEach((cliente, index) => {
      tabela.innerHTML += `
        <tr>
          <td>${cliente.nome}</td>
          <td>${cliente.email}</td>
          <td>${cliente.telefone}</td>
          <td>${cliente.cpf}</td>
          <td>${cliente.produto}</td>
          <td>
            <button class="btn-editar" onclick="editarCliente(${index})">Editar</button>
            <button class="btn-excluir" onclick="excluirCliente(${index})">Excluir</button>
          </td>
        </tr>
      `;
    });
  }

  function editarCliente(index) {
    document.getElementById("indice").value = index;
    document.getElementById("nome").value = clientes[index].nome;
    document.getElementById("email").value = clientes[index].email;
    document.getElementById("telefone").value = clientes[index].telefone;
    document.getElementById("cpf").value = clientes[index].cpf;
    document.getElementById("produto").value = clientes[index].produto;
  }

  function excluirCliente(index) {
    clientes.splice(index, 1);
    listarClientes();
    alert("Cliente excluído com sucesso!");
  }

  function limparCampos() {
    document.getElementById("nome").value = "";
    document.getElementById("email").value = "";
    document.getElementById("telefone").value = "";
    document.getElementById("cpf").value = "";
    document.getElementById("produto").value = "";
  }
</script>

</body>
</html>
