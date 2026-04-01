## Node.js / Express / MongoDB Exam — Questions & Answers

---

## Exercice 1 : QCM

#### 1) Qu'est-ce que Node.js ?

- A. Un système de base de données relationnelle
- B. Un framework de serveur web
- C. Un système d'exploitation
- D. Un environnement d'exécution JavaScript

**Réponse / Answer:** **D**

**FR :** Node.js permet d’exécuter JavaScript côté serveur.

**EN :** Node.js is a JavaScript runtime environment used to run JS outside the browser.

---

#### 2) Quel module est utilisé pour créer un serveur web dans Node.js ?

- A. http
- B. url
- C. fs
- D. path

**Réponse / Answer:** **A**

**FR :** Le module natif `http` sert à créer un serveur web en Node.js.

**EN :** The built-in `http` module is used to create a web server.

---

#### 3) Qu'est-ce que Express.js ?

- A. Une bibliothèque JavaScript frontend
- B. Un framework de test pour Node.js
- C. Un framework d'application web pour Node.js
- D. Un ORM pour Node.js

**Réponse / Answer:** **C**

**FR :** Express simplifie la création d’API et de routes.

**EN :** Express is a lightweight web framework for building APIs and servers.

---

#### 4) Quelle commande npm est utilisée pour installer Express dans un projet Node.js ?

- A. npm express install
- B. npm add express
- C. npm install express
- D. npm get express

**Réponse / Answer:** **C**

**FR :** C’est la commande correcte pour installer Express.

**EN :** This is the standard npm command to install Express.

---

#### 5) Comment démarre-t-on une application Express de base ?

- A. express start
- B. node start.js
- C. npm start
- D. node app.js

**Réponse / Answer:** **D**

**FR :** Si votre fichier principal s’appelle `app.js`, on démarre avec `node app.js`.

**EN :** If your main file is `app.js`, you run it with `node app.js`.

> ⚠️ `npm start` peut aussi fonctionner si configuré dans `package.json`, mais dans un examen basique on attend souvent `node app.js`.

---

#### 6) Quelle méthode HTTP est utilisée pour récupérer des données depuis un serveur dans Express ?

- A. GET
- B. POST
- C. PUT
- D. DELETE

**Réponse / Answer:** **A**

**FR :** `GET` sert à lire/récupérer des données.

**EN :** `GET` is used to fetch data from the server.

---

#### 7) Quelle méthode Express est utilisée pour gérer les requêtes POST ?

- A. app.post()
- B. app.get()
- C. app.put()
- D. app.delete()

**Réponse / Answer:** **A**

**FR :** `app.post()` permet de traiter les requêtes POST.

**EN :** `app.post()` handles POST requests.

---

#### 8) Quel middleware est couramment utilisé pour analyser du JSON dans Express ?

- A. express.json()
- B. bodyParser.json()
- C. jsonParser()
- D. parse.json()

**Réponse / Answer:** **A**

**FR :** `express.json()` permet de lire les données JSON envoyées dans `req.body`.

**EN :** `express.json()` parses incoming JSON request bodies.

---

#### 9) Comment peut-on accéder aux paramètres d'URL dans un gestionnaire de route Express ?

- A. req.params
- B. req.query
- C. req.body
- D. req.url

**Réponse / Answer:** **A**

**FR :** Les paramètres dans l’URL se récupèrent avec `req.params`.

**EN :** Route parameters are accessed using `req.params`.

**Exemple :**

```javascript
app.get('/student/:code', (req, res) => {
  console.log(req.params.code);
});
```

---

#### 10) Quelle méthode Express est utilisée pour servir des fichiers statiques ?

- A. app.static()
- B. app.useStatic()
- C. app.staticFiles()
- D. app.use()

**Réponse / Answer:** **D**

**FR :** Pour servir des fichiers statiques, on utilise généralement :

```js
app.use(express.static('public'));
```

**EN :** Static files are usually served using `app.use(express.static(...))`.

---

# Exercice 2 : Questions théoriques

#### 1. C’est quoi la différence entre Node.js et Express.js ?

**Réponse / Answer :**

**FR :** 

- Node.js est un environnement d’exécution JavaScript, qui permet d’exécuter du code JavaScript côté serveur.
- Express.js est un framework construit au-dessus de Node.js qui facilite la création d’applications web et d’API.

**EN :** 

- Node.js is a JavaScript runtime used to execute JavaScript on the server side.
- Express.js is a framework built on top of Node.js that makes building web applications and APIs easier.

---

#### 2. Expliquez en quelques phrases ce qu'est Mongoose et quel est son rôle dans une application Node.js utilisant MongoDB.

**Réponse / Answer :**

**FR :** 

- Mongoose est une bibliothèque ODM (Object Data Modeling) pour MongoDB et Node.js.
- Il permet de définir des schémas, créer des modèles et manipuler facilement les documents dans MongoDB.

**EN :** 

- Mongoose is an ODM library for MongoDB in Node.js.
- It helps define schemas, create models, and interact with MongoDB more easily.

---

#### 3. Quelle est la différence entre MongoDB et une base de données relationnelle comme MySQL ou PostgreSQL ?

**Réponse / Answer :**

**FR :** 

- MongoDB est une base de données **NoSQL** qui stocke les données sous forme de **documents JSON/BSON**.
- MySQL et PostgreSQL sont des bases de données **relationnelles** qui stockent les données dans des **tables avec lignes et colonnes**.

**EN :** 

- MongoDB is a **NoSQL** database that stores data as **documents**.
- MySQL and PostgreSQL are **relational databases** that store data in **tables**.

---

#### 4. Qu'est-ce qu'une fonction asynchrone en JavaScript ? Comment cela diffère-t-il d'une fonction synchrone ?

**Réponse / Answer :**

**FR :**

- Une fonction **asynchrone** permet d’exécuter des opérations longues (comme accès base de données, API, fichiers) sans bloquer le programme. 
- Elle utilise souvent `async/await` ou des Promises. 
- Une fonction **synchrone** exécute les instructions ligne par ligne et bloque l’exécution jusqu’à la fin.

**EN :** 

- An **asynchronous** function allows long operations (database calls, API calls, file reading) to run without blocking the program. 
- It often uses `async/await` or Promises.
- A **synchronous** function runs line by line and blocks execution until it finishes.

---

#### 5. Comment Node.js gère-t-il les requêtes HTTP ? Décrivez brièvement le processus du début à la fin.

**Réponse / Answer :**

**FR :** 

- Lorsqu’un client envoie une requête HTTP, le serveur Node.js la reçoit. Ensuite, Express (ou le module `http`) analyse la requête et cherche la route correspondante. 
- Les middlewares peuvent traiter la requête (authentification, parsing JSON, etc.). Puis la logique métier est exécutée (par exemple lecture/écriture dans MongoDB). Enfin, le serveur envoie une réponse HTTP au client.

**EN :** 

- When a client sends an HTTP request, the Node.js server receives it. Then Express (or the `http` module) processes it and matches it to the correct route. Middlewares may handle authentication, JSON parsing, etc. 
- Then the application logic runs (for example, querying MongoDB). Finally, the server sends an HTTP response back to the client.

---

# Exercice 3 : Code Node.js

#### 1. Connectez-vous à une base de données MongoDB nommée `myDatabase`.

**Réponse / Answer :**

```js
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    const uri = mongodb://127.0.0.1:27017/myDatabase;
  
    const conn = await mongoose.connect(uri);
    console.log('MongoDB Connected');
  } catch (error) {
    console.error('MongoDB connection error');
  }
};
```

---

## 2. Définissez un modèle de schéma Mongoose pour une collection `Étudiant` avec les champs `nom`, `prénom`, `date de naissance`, `note`, `adresse`, `code`.

**Réponse / Answer :**

```js
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
    firstName: {
        type: String,
        required: true
    },
    lastName: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: true,
        unique: true,
        lowercase: true
    },
    password: {
        type: String,
        required: true,
        minlength: 8
    },
    role: {
        type: String,
        enum: ['agent', 'manager', 'admin'],
        default: 'admin'
    },
}, { timestamps: true });

module.exports = mongoose.model('User', userSchema);
```

---

## 3. Écrivez une fonction en Node.js qui utilise Mongoose pour insérer un nouvel étudiant dans la base de données.

**Réponse / Answer :**

```javascript
const User = require('./models/user');

const createUser = async (req, res, next) => {
  try {
    req.body.createdBy = req.user.id;

    const user= await User.create(req.body);
    res.status(201).json({ success: true, user});
  } catch (error) {
    console.log("sth went wrong", err);
  }
};

module.exports ={ createUser };
```

---

## 4. Routes Express.js

### a) Écrivez une route Express.js qui récupère tous les étudiants de la base de données MongoDB et les renvoie au format JSON.

**Réponse / Answer :**

```javascript
const Etudiant = require('./models/Etudiant');

router.get('/etudiants', async (req, res, next) => {
  try {
    const clients = await Etudiant.find();
    res.status(200).json(etudiants);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
};
```

### b) Écrivez une route Express.js qui récupère un étudiant de la base de données MongoDB avec `code` et le renvoie au format JSON.

**Réponse / Answer :**

```js
router.get('/etudiants/:code', async (req, res) => {
  try {
    const etudiant = await Etudiant.findOne({ code: req.params.code });

    if (!etudiant) {
      return res.status(404).json({ message: 'Étudiant non trouvé' });
    }

    res.status(200).json(etudiant);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
});

```

---

## 5. Écrivez une requête MongoDB qui met à jour l'âge d'un utilisateur ayant pour nom `Aymen` et `note = 16`.

**Réponse / Answer :**

### Version Mongoose

```js
await Etudiant.updateOne(
  { nom: 'Aymen', note: 16 },
  { $set: { age: 22 } }
);
```

### Version MongoDB Shell

```js
db.etudiants.updateOne(
  { nom: 'Aymen', note: 16 },
  { $set: { age: 22 } }
);
```

---

# Notes / Remarques importantes

## ⚠️ Pièges fréquents en examen

### 1) Oublier `await`

```js
const etudiants = await Etudiant.find();
```

### 2) Oublier `express.json()`

```js
app.use(express.json());
```

### 3) Confondre `req.params`, `req.query`, `req.body`

- `req.params` → paramètres URL
- `req.query` → query string
- `req.body` → données envoyées en POST/PUT

### 4) Mauvaise syntaxe Mongoose

```js
const Etudiant = mongoose.model('Etudiant', etudiantSchema);
```

### 5) Toujours gérer les erreurs avec `try/catch`

 