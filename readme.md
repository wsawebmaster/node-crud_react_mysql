# CRUD NODE REACT MYSQL

## Preparando Backend da aplicação

Na pasta api execute os seguintes comandos:

`npm init -y`

`npm install -g yarn`

`yarn add express nodemon mysql cors`

Estrutura de diretórios recomendada

```shell
  ├── api
      ├── controllers
      │   └── user.js
      ├── routes
      │   └── users.js
      ├── db.js
      ├── index.js
      ├── package.json
      ├── yarn.lock
```

controllers/user.js

    import { db } from "../db.js";

    export const getUsers = (_, res) => {
      const q = "SELECT * FROM usuarios";

      db.query(q, (err, data) => {
        if (err) return res.json(err);

        return res.status(200).json(data);
    });
    };

routes/users.js

    import express from "express";
    import { getUsers } from "../controllers/user.js";

    const router = express.Router();

    router.get("/", getUsers);

    export default router;

db.js

    import mysql from "mysql";

    export const db = mysql.createConnection({
      host: 'localhost',
      user: 'root',
      password: '',
      database: 'crud-node'
    });

index.js

import express from "express";
import userRoutes from "./routes/users.js";
import cors from "cors";

const app = express();

app.use(express.json());
app.use(cors());

app.use("/", userRoutes);

app.listen(8800);

package.json

    {
      "name": "api",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "type": "module",
      "scripts": {
        "start": "nodemon index.js"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "dependencies": {
        "cors": "^2.8.5",
        "express": "^4.18.2",
        "mysql": "^2.18.1",
        "nodemon": "^2.0.22"
      }
    }

<hr>

## Preparando Frontend da aplicação

Na pasta frontend execute os seguintes comandos

`npx create-react-app ./`

`yarn add styled-components axios react-icons react-toastify`

Acesse a pasta src e exclua os arquivos
App.css | App.test.js | index.css | logo.svg | reportWebVitals.js | setupTests.js

Obs.: Para facilitar exportei o banco de dados em uma nova pasta database

`yarn start` - Iniciar projeto na pasta frontend
`yarn start` - Iniciar projeto na pasta api
