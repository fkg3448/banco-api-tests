# Banco API Tests

Automação de testes de API REST para o projeto **Banco API**, utilizando JavaScript e ferramentas do ecossistema Node.js.

## 🎯 Objetivo

Este projeto tem como objetivo automatizar a validação dos principais comportamentos da API REST do projeto [Banco API](https://github.com/juliodelimas/banco-api).

Os testes realizam requisições HTTP contra a API e validam, entre outros pontos, os códigos de status HTTP e o conteúdo das respostas. A autenticação é realizada por meio do endpoint de login, utilizando o token retornado pela API nos cenários que necessitam de autorização.

O projeto de testes está disponível em:

- [banco-api-tests](https://github.com/fkg3448/banco-api-tests)

A API que será testada está disponível em:

- [banco-api](https://github.com/juliodelimas/banco-api)

> **Importante:** a API Banco API precisa estar em execução e acessível pela URL configurada em `BASE_URL` antes da execução dos testes.

---

## 🛠️ Stack utilizada

| Tecnologia / Biblioteca | Utilização |
| --- | --- |
| **JavaScript** | Linguagem utilizada para implementação dos testes |
| **Node.js** | Ambiente de execução do projeto |
| **Mocha** | Framework utilizado para organização e execução dos testes |
| **Supertest** | Biblioteca utilizada para realizar requisições HTTP e auxiliar nos testes da API |
| **Chai** | Biblioteca de asserções utilizada para validar os resultados dos testes |
| **dotenv** | Carregamento das variáveis definidas no arquivo `.env` |
| **Mochawesome** | Reporter utilizado para gerar os relatórios dos testes em HTML |

As dependências e respectivas versões utilizadas pelo projeto estão definidas no `package.json`. Atualmente, o projeto declara `chai`, `dotenv`, `mocha`, `mochawesome` e `supertest` como dependências. O script `npm test` executa os testes com Mocha e utiliza o reporter Mochawesome. 

---

## 📁 Estrutura de diretórios

A estrutura principal do projeto é organizada da seguinte maneira:

```text
banco-api-tests/
├── fixtures/
│   ├── postLogin.json
│   └── ...
├── helpers/
│   ├── autenticacao.js
│   └── ...
├── test/
│   ├── *.test.js
│   └── ...
├── .gitignore
├── .env                 # criado localmente pelo usuário
├── package.json
└── package-lock.json
```

### `fixtures/`

Contém os arquivos JSON utilizados como massa de dados pelos testes.

Por exemplo, os dados utilizados na autenticação são mantidos em `fixtures/postLogin.json`, evitando que o corpo das requisições fique diretamente misturado à implementação dos testes.

### `helpers/`

Contém funções auxiliares e reutilizáveis.

Um dos helpers é `autenticacao.js`, responsável por realizar o login na API e retornar o token JWT obtido na resposta. A requisição utiliza `process.env.BASE_URL` como endereço base da API.

### `test/`

Contém os arquivos responsáveis pela implementação dos cenários automatizados.

Os arquivos seguem o padrão `*.test.js` e são encontrados pelo comando configurado no `package.json`:

```bash
mocha ./test/**/*.test.js
```

### `.env`

Arquivo de configuração local que **não deve ser versionado**. O `.gitignore` do projeto já o exclui do Git, juntamente com `node_modules/` e `mochawesome-report/`.

### `package.json`

Define as informações do projeto, dependências e scripts de execução.

### `package-lock.json`

Registra as versões específicas das dependências instaladas pelo npm.

---

## ⚙️ Pré-requisitos

Antes de executar os testes, é necessário ter instalado:

- **Node.js**
- **npm**
- A API **Banco API** em execução
- Acesso à URL da API que será testada

A versão do Node.js deve ser compatível com as versões das dependências instaladas no projeto. Para o ambiente atual, consulte também os requisitos da versão do Mocha utilizada no `package.json`.

---

## 🔐 Configuração do `.env`

O arquivo `.env` **não é disponibilizado no repositório** porque contém configurações específicas do ambiente de execução.

Crie um arquivo chamado `.env` na raiz do projeto:

```text
banco-api-tests/
├── .env
├── package.json
├── fixtures/
├── helpers/
└── test/
```

O conteúdo mínimo esperado é:

```env
BASE_URL=http://localhost:3000
```

Substitua a URL pelo endereço em que a API Banco API estiver disponível.

### Exemplo

Se a API estiver executando localmente na porta `3000`:

```env
BASE_URL=http://localhost:3000
```

Se estiver disponível em outro endereço:

```env
BASE_URL=http://localhost:8080
```

O valor de `BASE_URL` é utilizado pelos testes por meio de:

```javascript
process.env.BASE_URL
```

O projeto utiliza `dotenv` para carregar as variáveis do `.env` para `process.env`.

> **Atenção:** não altere o nome da variável. O projeto espera especificamente `BASE_URL`.

---

## 📦 Instalação

Clone o repositório:

```bash
git clone https://github.com/fkg3448/banco-api-tests.git
```

Entre no diretório:

```bash
cd banco-api-tests
```

Instale as dependências:

```bash
npm install
```

Depois, crie o arquivo `.env` na raiz do projeto e configure a `BASE_URL`.

---

## ▶️ Execução dos testes

Com a API em execução e o `.env` configurado, execute:

```bash
npm test
```

O script atualmente configurado no `package.json` é:

```json
"test": "mocha ./test/**/*.test.js --timeout 200000 --reporter mochawesome"
```

Isso significa que o comando:

1. Localiza os arquivos de teste dentro de `test/`;
2. Executa os testes utilizando o Mocha;
3. Define timeout de `200000` ms;
4. Utiliza o Mochawesome como reporter.

Também é possível executar diretamente:

```bash
npx mocha ./test/**/*.test.js --timeout 200000 --reporter mochawesome
```

---

## 📊 Relatórios com Mochawesome

Após a execução dos testes, o Mochawesome gera os arquivos de relatório no diretório:

```text
mochawesome-report/
```

Normalmente, a estrutura gerada inclui arquivos como:

```text
mochawesome-report/
├── assets/
├── mochawesome.html
└── mochawesome.json
```

O principal arquivo para visualização é:

```text
mochawesome-report/mochawesome.html
```

Abra esse arquivo em um navegador para visualizar o relatório detalhado da execução.

O relatório HTML apresenta informações como:

- quantidade de testes executados;
- testes aprovados;
- testes com falha;
- duração dos testes;
- suites e casos de teste;
- detalhes das falhas;
- stack trace quando aplicável.

O diretório `mochawesome-report/` está incluído no `.gitignore`, portanto os relatórios são gerados localmente e não são enviados ao repositório.

### Gerar o relatório

Não é necessário executar um comando adicional para gerar o relatório: o próprio `npm test` já utiliza:

```bash
--reporter mochawesome
```

Portanto:

```bash
npm test
```

é suficiente para executar os testes e gerar o relatório.

### Abrir o relatório

Após a execução:

```text
mochawesome-report/mochawesome.html
```

Abra o arquivo no navegador.

---

## 🔄 Fluxo de execução

O fluxo básico para executar o projeto é:

```text
1. Clonar o repositório
          ↓
2. Instalar as dependências
          ↓
3. Criar e configurar o arquivo .env
          ↓
4. Iniciar a Banco API
          ↓
5. Executar npm test
          ↓
6. Mocha executa os testes
          ↓
7. Supertest realiza as requisições HTTP
          ↓
8. Chai valida as respostas
          ↓
9. Mochawesome gera o relatório
          ↓
10. Abrir mochawesome-report/mochawesome.html
```

---

## 🔑 Autenticação

Os cenários que necessitam de autenticação utilizam o endpoint de login da API.

O helper `helpers/autenticacao.js` realiza uma requisição para:

```http
POST /login
```

A URL base é obtida de:

```javascript
process.env.BASE_URL
```

Após a autenticação, o token retornado pela API é utilizado pelos testes que necessitam de autorização.

Isso permite centralizar a lógica de autenticação em um helper reutilizável, evitando duplicação dessa implementação nos diferentes arquivos de teste.

---

## 🧪 Exemplo de validação

Um cenário de teste segue a estrutura do Mocha e utiliza o Chai para realizar as asserções.

Exemplo simplificado:

```javascript
describe('Login', () => {
    describe('POST /login', () => {
        it('Deve retornar 200 com token em string quando usar credenciais válidas', async () => {
            const resposta = await request(process.env.BASE_URL)
                .post('/login')
                .set('Content-Type', 'application/json')
                .send(bodyLogin);

            expect(resposta.status).to.equal(200);
            expect(resposta.body.token).to.be.a('string');
        });
    });
});
```

Esse padrão separa claramente:

- preparação dos dados;
- execução da requisição;
- validação da resposta.

---

## 🧹 Arquivos ignorados pelo Git

O projeto possui um `.gitignore` configurado para não versionar:

```text
node_modules/
mochawesome-report/
.env
```

Esses arquivos e diretórios são específicos do ambiente local ou são gerados durante a execução dos testes.

---

## 📚 Documentação das dependências

### Mocha

Framework utilizado para estruturar e executar os testes JavaScript.

- [Documentação oficial do Mocha](https://mochajs.org/)
- [Getting Started](https://mochajs.org/getting-started/)

### Supertest

Biblioteca utilizada para realizar requisições HTTP e facilitar a criação de testes para APIs.

- [Documentação / pacote no npm](https://www.npmjs.com/package/supertest)

### Chai

Biblioteca de asserções utilizada para verificar se os resultados obtidos pela API correspondem aos resultados esperados.

- [Documentação oficial do Chai](https://www.chaijs.com/)
- [API de asserções](https://www.chaijs.com/api/assert/)

### dotenv

Biblioteca utilizada para carregar as variáveis do arquivo `.env` para `process.env`.

- [Documentação / pacote no npm](https://www.npmjs.com/package/dotenv)

### Mochawesome

Reporter utilizado pelo Mocha para gerar relatórios detalhados em HTML e JSON.

- [Documentação / pacote no npm](https://www.npmjs.com/package/mochawesome)
- [Repositório oficial](https://github.com/adamgruber/mochawesome)

---

## 🔗 Projetos relacionados

### Banco API

API REST utilizada como sistema sob teste:

[https://github.com/juliodelimas/banco-api](https://github.com/juliodelimas/banco-api)

### Banco API Tests

Projeto de automação responsável pelos testes:

[https://github.com/fkg3448/banco-api-tests](https://github.com/fkg3448/banco-api-tests)

---

## 👨‍💻 Autor

Projeto de automação de testes desenvolvido em JavaScript para validação da API REST Banco API.

---

## 📄 Licença

O projeto de testes possui a licença definida em seu `package.json`.

