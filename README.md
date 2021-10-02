# Cookmaster 🧑‍🍳

Este projeto foi desenvolvido durante o curso de desenvolvimento web da [Trybe](https://www.betrybe.com/).

### Descrição:
Desenvolvimento de uma aplicação que faz operações básicas no banco de dados: CREATE, READ, UPDATE, DELETE (CRUD).
Para fazer qualquer tipo de alteração no banco de dados, será necessário autenticar-se. As pessoas usuárias podem ser clientes ou administradores. Pessoas clientes apenas poderão fazer alterações nas receitas criadas por ele mesmo. Uma pessoa administradora poderá disparar qualquer ação em qualquer receita.


### Principais tecnologias utilizadas:
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white)
![Express.js](https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB)
![JWT](https://img.shields.io/badge/JWT-black?style=for-the-badge&logo=JSON%20web%20tokens)
![Mocha](https://img.shields.io/badge/-mocha-%238D6748?style=for-the-badge&logo=mocha&logoColor=white)

### Habilidades Desenvolvidas: 

- Autenticação via [JWT](https://jwt.io/introduction)
- Trafegar arquivos em requisições com o [Multer](https://github.com/expressjs/multer)
- Arquitetura REST
- Testes usando [Mocha](https://mochajs.org/)
- Mocks com [Sinon](https://sinonjs.org/releases/latest/)
- Melhoria de legibilidade dos testes com [Chai](https://www.chaijs.com/api/bdd/)
- Validações com [Joi](https://joi.dev/api/?v=17.4.2)

### Como rodar a aplicação:

```bash
# Clone o repositório:
git clone https://github.com/Marcuscps19/cookmaster.git

# Entre no diretório
cd cookmaster

# Instale as depêndencias
npm install

# Rode o projeto
npm start
```

### Para efetuar as requisições:
*Utilize ferramentas como [Postman](https://www.postman.com/), [Insomnia](https://insomnia.rest/), [Thunder Client](https://www.thunderclient.io/) ou outra de sua preferência.*

#### Criar nova pessoa usuária não administradora
```bash
# rota da requisição POST
 https://localhost:3000/users

# no corpo da requisição adicionar o seguinte formato:
  {
    "name": "string",
    "email": "string",
    "password": "string"
  }
```
- No corpo da requisição, name, email e password são obrigatórios, caso não coloque a API retornará uma mensagem informando o erro.
- O email deve possuir um formato válido. Ex: ```email@email.com```
- O email deve ser único, se cadastrar um email que já existe a API retornará uma mensagem informando o erro.
- Se a pessoa usuária for cadastrada com sucesso será retornado da API a pessoa usuária cadastrada.

#### Criar nova pessoa usuária administradora
```bash
# rota da requisição POST
 https://localhost:3000/users/admin

# no corpo da requisição adicionar o seguinte formato:
  {
    "name": "string",
    "email": "string",
    "password": "string"
  }
```
- No corpo da requisição, name, email e password são obrigatórios, caso não coloque a API retornará uma mensagem informando o erro.
- O email deve possuir um formato válido. Ex: ```email@email.com```
- O email deve ser único, se cadastrar um email que já existe a API retornará uma mensagem informando o erro.
- Somente uma pessoa usuária autenticada com a role ```admin``` poderá efetuar cadastros de novas pessoas administradoras, para isso utilize a seguinte pessoa administradora previamente cadastrada:
```bash
{ name: 'admin', email: 'root@email.com', password: 'admin', role: 'admin' }
```
- Se a pessoa usuária administradora for cadastrada com sucesso será retornado da API a pessoa usuária administradora cadastrada.

#### Login de pessoas usuárias
```bash
# rota da requisição POST
 https://localhost:3000/login

# no corpo da requisição adicionar o seguinte formato:
 {
  "email": "string",
  "password": "string"
  }
```
- No corpo da requisição, email e password são obrigatórios, caso não coloque a API retornará uma mensagem informando o erro.
- O email deve possuir um formato válido. Ex: ```email@email.com```
- O email e o password devem ter sido previamente cadastrados através da tora ```users```, caso contrário, a API retornará uma mensagem informando o erro.
- Se o login for feito com sucesso a API retornará um token, guarde esse token para utilizar em requisições específicas.

#### Cadastro de receitas
```bash
# rota da requisição POST
 https://localhost:3000/recipes

# no corpo da requisição adicionar o seguinte formato:
 {
  "name": "string",
  "ingredients": "string",
  "preparation": "string"
}

# no header da requisição adicionar o seguinte formato:
 Authorization: "token JWT gerado ao fazer login"
```

- No corpo da requisição, name, ingredients e preparation são obrigatórios, caso não coloque a API retornará uma mensagem informando o erro.
- Se o token for inválido ou faltante a API retornará  uma mensagem informando o erro.
- Se o cadastro da receita for feito com sucesso a API retornará a receita cadastrada.

#### Listagem de receitas
```bash
# rota da requisição GET
 https://localhost:3000/recipes
```

- Essa rota pode ser acessada por pessoas usuárias logadas ou não.
- Se a requisição for feita com sucesso, serão listadas as receitas cadastradas.

#### Listagem de receita específica
```bash
# rota da requisição GET
 https://localhost:3000/recipes/:id
```

- Essa rota pode ser acessada por pessoas usuárias logadas ou não.
- Se o id for inválido ou não existir a API retornará uma mensagem informando o erro.
- Se a requisição for feita com sucesso, sera listada a receita cadastrada.

#### Edição de receita específica
```bash
# rota da requisição PUT
 https://localhost:3000/recipes/:id
 
# no corpo da requisição adicionar o seguinte formato:
 {
  "name": "string",
  "ingredients": "string",
  "preparation": "string"
}

# no header da requisição adicionar o seguinte formato:
 Authorization: "token JWT gerado ao fazer login"
```

- No corpo da requisição, name, ingredients e preparation são obrigatórios, caso não coloque a API retornará uma mensagem informando o erro.
- Se o token for inválido ou faltante a API retornará  uma mensagem informando o erro.
- A receita só poderá ser atualizada se a pessoa usuária autenticada for a proprietária da receita ou uma pessoa administradora.
- Se a atualização da receita for feita com sucesso a API retornará a receita atualizada.

#### Exclusão de receita específica
```bash
# rota da requisição DELETE
 https://localhost:3000/recipes/:id
 
# no header da requisição adicionar o seguinte formato:
 Authorization: "token JWT gerado ao fazer login"
```

- Se o token for inválido ou faltante a API retornará  uma mensagem informando o erro.
- A receita só poderá ser deletada se a pessoa usuária autenticada for a proprietária da receita ou uma pessoa administradora.
- Se a exclusão da receita for feita com sucesso a API não retornará um corpo.

#### Adição de uma imagem em uma receita específica
```bash
# rota da requisição PUT
 https://localhost:3000/recipes/:id/image
 
# no corpo da requisição adicionar o seguinte formato em multipart:
 image imagem.jpeg(imagem carregada)
 
# no header da requisição adicionar o seguinte formato:
Authorization: "token JWT gerado ao fazer login"
```

- Se o token for inválido ou faltante a API retornará  uma mensagem informando o erro.
- A imagem só poderá ser adicionada se a pessoa usuária autenticada for a proprietária da receita ou uma pessoa administradora.
- Se a adição da imagem for feita com sucesso a API retornará a receita atualizada com a imagem carregada e o nome da imagem igual ao id da receita.

#### Acessar imagem de uma receita
```bash
# rota da requisição get
 https://localhost:3000/images/<id-da-receita>.jpeg
```

- Essa rota pode ser acessada por pessoas usuárias logadas ou não.
- Se a requisição da imagem for feita com sucesso a API retornará a imagem da receita.


### Repositório do projeto para mais detalhes: https://github.com/tryber/sd-010-a-cookmaster



