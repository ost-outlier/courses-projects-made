Esse código é um pequeno aplicativo React que usa a **API do Unsplash** para buscar e exibir fotos aleatórias com base em um termo de pesquisa. Abaixo está a explicação linha por linha e por blocos, como se estivesse te ensinando do zero:

---

### 📦 **Importações iniciais**

```js
import React from "react";
import ReactDOM from "react-dom";
```

- **React** é a biblioteca usada para criar interfaces.
- **ReactDOM** é usado para renderizar o componente no navegador.

---

### 🧠 **Desestruturação de hooks do React**

```js
const { useState, useEffect, useRef } = React;
```

- `useState`: cria estados dentro de componentes funcionais.
- `useEffect`: executa efeitos colaterais (ex: carregar dados).
- `useRef`: permite criar referências a elementos da DOM.

---

### 🔑 **Credenciais e constantes**

```js
const clientID = "t-FQWYk2PUt13LidWIblzu7SNd9HVOQsK3QA7Lg1Mg4";
const utm = "?utm_source=scrimba_degree&utm_medium=referral";
var API_KEY = "NpRvp4rxQt7jYkbu95fWvCMrZKxyQKlWcNZfzeopGfI";
```

- `clientID`: necessário para autenticar na API do Unsplash.
- `utm`: parâmetro de rastreamento para os links de crédito.
- `API_KEY`: declarada mas **não é usada** no código.

---

### 🌐 **Função para carregar dados**

```js
const loadData = (options) => {
  fetch(options.url)
    .then((response) => response.json())
    .then((data) => {
      if (options.onSuccess) options.onSuccess(data);
    });
};
```

- Uma função genérica que faz requisições HTTP usando `fetch`.
- Recebe um `url` e uma função `onSuccess` para lidar com os dados.

---

### 💻 **Componente Principal `App`**

```js
const App = (props) => {
```

- Um componente React funcional que recebe `props` (como `name` e `emoji`).

---

### 📸 **Estados do componente**

```js
let [photos, setPhotos] = useState([]);
let [query, setQuery] = useState("carrot cake");
const queryInput = useRef(null);
```

- `photos`: array com as fotos retornadas.
- `query`: termo de busca (inicialmente "carrot cake").
- `queryInput`: uma referência para o campo de entrada (input).

---

### 🔗 **URL base da API do Unsplash**

```js
const numberOfPhotos = 200;
const url =
  "https://api.unsplash.com/photos/random/?count=" +
  numberOfPhotos +
  "&client_id=" +
  clientID;
```

- Monta a URL da API para buscar **200 fotos aleatórias** com a `client_id`.

---

### ⚡ **Hook `useEffect`**

```js
useEffect(() => {
  const photosUrl = query ? `${url}&query=${query}` : url;

  loadData({
    url: photosUrl,
    onSuccess: (res) => {
      setPhotos(res);
    },
  });
}, [query, url]);
```

- Executado **sempre que `query` mudar**.
- Monta a URL com o termo de busca.
- Chama `loadData` para buscar e armazenar as fotos.

---

### 🔍 **Função de busca**

```js
const searchPhotos = (e) => {
  e.preventDefault();
  setQuery(queryInput.current.value);
};
```

- É chamada quando o usuário envia o formulário.
- Evita o recarregamento da página.
- Atualiza o estado `query` com o valor digitado.

---

### 🖼️ **Renderização**

```jsx
return (
  <div className="box">
    <h2>{props.emoji}</h2>
    <h1>{props.name}'s website</h1>
    <div className="grid">
      {query
        ? photos.map((photo) => (
            <div key={photo.id} className="item">
              <img className="img" src={photo.urls.regular} />
              <div className="caption">
                <span className="credits">
                  Photo by
                  <a href={photo.user.links.html + utm}> {photo.user.name} </a>
                  <span> on </span>
                  <a href={"https://unsplash.com" + utm}>Unsplash</a>
                </span>
              </div>
            </div>
          ))
        : ""}
    </div>
  </div>
);
```

- Renderiza um título e a grade de imagens.
- Cada imagem inclui:

  - Foto.
  - Créditos com link para o fotógrafo e Unsplash.

---

### 🚀 **Renderização na página**

```js
ReactDOM.render(<App name="Per" emoji="🎉" />, document.getElementById("root"));
```

- Renderiza o componente `App` dentro do elemento com `id="root"`.
- Passa `name="Per"` e `emoji="🎉"` como props.

---

### ✅ Resumo geral:

- Usa React para construir uma galeria de fotos.
- Busca imagens aleatórias da API do Unsplash com base em uma palavra-chave.
- Permite ao usuário alterar a busca.
- Exibe cada foto com seus devidos créditos.

Se quiser, posso te ensinar como modificar o código para, por exemplo:

- mudar o número de imagens,
- adicionar uma barra de busca real,
- estilizar com CSS moderno.

Quer seguir com alguma dessas ideias?

---

Ótimas perguntas! Vamos respondê-las com clareza:

---

### ✅ **1. Ele busca até imagens premium da Unsplash?**

**Não.** A API pública do Unsplash **não retorna imagens premium** (ou seja, pagas). Ela trabalha apenas com as imagens **gratuitas** disponíveis na plataforma.

Mais detalhes:

- A Unsplash oferece imagens gratuitamente sob a [licença Unsplash](https://unsplash.com/license).
- Mesmo se houver parcerias comerciais ou imagens premium promovidas na interface do site, essas **não estão incluídas na API gratuita**.
- A `client_id` usada no código autentica apenas com a API pública (gratuita).

---

### ✅ **2. Como trazer o resultado por relevância ao invés de aleatoriedade?**

Atualmente o código está usando esse endpoint:

```js
"https://api.unsplash.com/photos/random";
```

Esse endpoint retorna **imagens aleatórias** (com ou sem base em um `query`).

Se você quer resultados **relevantes**, deve trocar para o endpoint de **busca normal**, que ordena por **relevância por padrão**.

---

### 🔁 Como mudar para busca por relevância:

#### ✅ Substitua a URL do código por:

```js
const url =
  "https://api.unsplash.com/search/photos?page=1&per_page=" +
  numberOfPhotos +
  "&client_id=" +
  clientID;
```

#### ✅ Depois, dentro do `useEffect`, altere:

```js
const photosUrl = query ? `${url}&query=${query}` : url;

loadData({
  url: photosUrl,
  onSuccess: (res) => {
    // resultado da busca vem dentro de `res.results`
    setPhotos(res.results);
  },
});
```

---

### 🧠 Diferença entre os endpoints:

| Tipo de busca        | Endpoint         | Ordem                   | Retorno       |
| -------------------- | ---------------- | ----------------------- | ------------- |
| Aleatória            | `/photos/random` | Aleatória               | Array direto  |
| Busca por relevância | `/search/photos` | Por relevância (padrão) | `res.results` |

---

### ✍️ Recapitulando as mudanças:

- Troque o endpoint de `/photos/random` para `/search/photos`.
- Ajuste o tratamento do JSON: os resultados estarão em `res.results`.
- A ordenação por relevância já é o padrão. Mas você pode forçar com `&order_by=relevant` se quiser garantir.

---

Se quiser, posso adaptar todo o trecho do código para você copiar e colar com essa nova busca. Deseja isso?

---

Excelente dúvida! Vamos explicar **em duas partes** com total clareza:

---

### ✅ **Parte 1: Onde vai `&order_by=relevant`?**

O parâmetro `&order_by=relevant` é usado **somente no endpoint de busca**, ou seja, quando você usa:

```
https://api.unsplash.com/search/photos
```

#### 👉 Exemplo completo da URL com busca por relevância:

```js
const url =
  "https://api.unsplash.com/search/photos?page=1&per_page=" +
  numberOfPhotos +
  "&order_by=relevant" +
  "&client_id=" +
  clientID;
```

> 🔎 Obs: `order_by=relevant` é **o padrão**, mas colocar explicitamente é útil para garantir o comportamento se a API mudar futuramente.

---

### ✅ **Parte 2: Por que precisa usar `res.results`?**

Essa diferença vem da **estrutura de resposta da API** do Unsplash.

#### 1. Quando você usa `/photos/random`:

A resposta é **um array direto** de fotos.

```json
[
  { "id": "1", "urls": { ... }, ... },
  { "id": "2", "urls": { ... }, ... }
]
```

Ou seja:

```js
setPhotos(res); // direto
```

---

#### 2. Quando você usa `/search/photos`:

A resposta é um **objeto** com vários campos, e as fotos ficam **dentro de `results`**:

```json
{
  "total": 5000,
  "total_pages": 250,
  "results": [
    { "id": "1", "urls": { ... }, ... },
    { "id": "2", "urls": { ... }, ... }
  ]
}
```

Então **você precisa acessar o array `results`**, assim:

```js
setPhotos(res.results);
```

---

### ✅ Resumo prático:

| Endpoint               | URL Base         | Resposta             | Código necessário        |
| ---------------------- | ---------------- | -------------------- | ------------------------ |
| Aleatória              | `/photos/random` | Array direto         | `setPhotos(res)`         |
| Por relevância (busca) | `/search/photos` | Objeto com `results` | `setPhotos(res.results)` |

---

Se quiser, posso te reescrever o trecho exato do código com tudo ajustado para busca por relevância. Deseja isso?
