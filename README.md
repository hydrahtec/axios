# Axios

- Estudo de APIs com axios -

https://www.devmedia.com.br/consumindo-uma-api-com-react-js-e-axios/42900

# React Axios
- Axios é um cliente HTTP baseado em Promises para fazer requisições. Pode ser utilizado tanto no navegador quanto no Node.js ou qualquer serviço de API.

# Características

- Usando o Ajax como uma camada abaixo, faz requisições através do browser via XMLHttpRequests;
- Faz requisições HTTP com o Node.js;
- Suporta a Promises;
- Todas as respostas são transformadas e retornadas em JSON;
- Tem suporte a falsificação de solicitações entre sites, conhecido como XRSF.

# Instalação e Configuração

- npx create-react-app react-axios
- npm install axios
    - criar um arquivo chamado api.js

* api.js
    -import axios from "axios";

    const api = axios.create({
    baseURL: "https://api.github.com",
    });

    export default api;

* app.js
    - import React, { useEffect, useState } from "react";
    import api from "./services/api";

    export default function App() {
    const [user, setUser] = useState();

    return (
        <div className="App">
        <p>Usuário: {user?.login}</p>
        <p>Biografia: {user?.bio}</p>
        </div>
    );
    }

* Requisição com GET
    import React, { useEffect, useState } from "react";
    import api from "./services/api";

    export default function App() {
    const [user, setUser] = useState();

    useEffect(() => {
        api
        .get("/users/romulo27")
        .then((response) => setUser(response.data))
        .catch((err) => {
            console.error("ops! ocorreu um erro" + err);
        });
    }, []);

    return (
        <div className="App">
        <p>Usuário: {user?.login}</p>
        <p>Biografia: {user?.bio}</p>
        </div>
    );
    }

* Requisição com POST
    useEffect(() => {
    api
        .post("https://minhaapi/novo-usuario",{
            nome: “Romulo”,
            sobrenome: “Sousa”
    })
        .then((response) => setUser(response.data))
        .catch((err) => {
        console.error("ops! ocorreu um erro" + err);
        });
    }, []);

* A diferença dos métodos get() e post() é que, no get() os parâmetros serão passados através do cabeçalho da requisição HTTP, e no post() os parâmetros são enviados através do corpo da requisição. 

* Os verbos mais comuns para requisições HTTP são: GET, POST, DELETE e PUT.
    -  // Verbo GET
        api.get(endpoint)

    - // Verbo POST
        api.post(endpoint, dados)


    - // Verbo DELETE
        api.delete(endpoint, dados)

    - // Verbo PUT
        api.put(endpoint, dados)

# Axios Token

* É comum certos recursos serem protegidos para que somente usuários autenticados tenham acesso. Nesses casos os Tokens são utilizados para enviar uma requisição.

* O Token é gerado por serviços de autenticação, como JWT, Passport, entre outros. Ele é enviado dentro do headers da requisição.

- Para enviar um token através do Axios: 
    api.defaults.headers.authorization = `Bearer ${token}`;

    - Essa validação deve ser inserida no arquivo de configuração da API (services/api.js). Ela vai funcionar como um validador para o usuário. Caso ele tenha um token ativo, libera o acesso para usar um endpoint da API.

    import axios from "axios";

    const api = axios.create({
    baseURL: "https://api.github.com",
    });

    api.interceptors.request.use(async config => {
    // Declaramos um token manualmente para teste.
    const token = "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9";

    if (token) {
        api.defaults.headers.authorization = `Bearer ${token}`;
    }

    return config;
    });

export default api;
# Etapas e tempos de requisições HTTP

- https://www.devmedia.com.br/etapas-e-tempos-de-requisicoes-http/32618

