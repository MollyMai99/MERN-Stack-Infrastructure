# MERN

## Setup

1. Create `vite` project -> `npm create vite`
   1. Answer the questions -> `mern` folder
2. `cd mern` && `npm install`

## Git setup

1. `git init`
2. Add on the `.gitignore` from <https://www.toptal.com/developers/gitignore/api/windows,osx,node,visualstudiocode>
3. `git add .` && `git commit -m ...`

Goto `github.com` and create a new EMPTY repo

```bash
 git remote add origin git@git.generalassemb.ly:simonlau/mern-50.git
  git branch -M main
  git push -u origin main
```

## Optional lint-staged + git-hooks + prettier

`npm install -D prettier`
`npx mrm@2 lint-staged`

`husky` -> git hook manager
`lint-staged`

install into `package.json` in devDepencies

new `lint-staged` in `package.json`
new `.husky`

- `pre-commit` -> `npx lint-staged`

## Edit for CommonJS

Inside `.eslintrc.cjs` change to

`env: { browser: true, es2020: true, node: true },`

Inside `package.json`

Remove `type: "module"`

## Adaptation for vite dist instead of CRA build

Inside `server.js`

```js
app.use(favicon(path.join(__dirname, "dist", "vite.svg")));
app.use(express.static(path.join(__dirname, "dist")));
```

## Setup nodemon

`npm install -D nodemon`

in `package.json` add to "scripts":

```js
    "dev:react": "vite",
    "dev:express": "node --watch server.js",
    "dev:express-win": "nodemon server.js",
```

## Clean up

`main.js` -> remove CSS

Unused files

```bash
rm src/*.css
rm -r src/assets
```

## React convention

Folder -> name is same as the actual Component

split into `pages` and stand-alone `components` folders

## dotenv pitfall

dotenv-safe -> `.env.example`

changing `.env` -> does not restart express

## debug in express

In server.js -> `const debug = require("debug")("mern:server");`
In `config/database.js` -> `const debug = require("debug")("mern:config:database");`

In package.json change to

`"dev:express": "DEBUG=mern:* node --watch server.js",`

## debug in react

in `App.js` as well as every other file you want to log

```js
import debug from "debug";

const log = debug("mern-50:pages:App:App");
```

in `main.jsx` -> write once -> `localStorage.debug = "mern-50:*";`

## Structure

React -> src -> pages / components etc
Express -> server.js, models, controllers etc

Project
--> React
--> Express

## Proxy setup

In `vite.config.js`, change to

```js
// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    proxy: {
      "/api": "http://localhost:3000",
    },
  },
});
```

## Deploy -> Vercel

## Routing

- React -> React Router -> /movies
- Express -> ALL start with `/api` like /api/movies

## Why Class Components

Last time -> functional components have NO hooks

## Sign UP -> REST -> Create User

### React

- `/` -> AuthPage -> SignUpForm
- User fill in the SignUpForm -> onSubmit
- preventDefault() -> users-service -> users-api -> FETCH

Fetch (Network) -> `/api/users`, POST + JSON Body (Bruno also)

### Express

`server.js` -> `/api/users` -> usersRouter
usersRouter -> `/` (`/api/users`) + POST -> usersController.create
create -> req.body
create user -> const user = await User.create()
user -> makeJWT -> JWT
-> res.json(jwt)

### Back to React

users-api -> JSON -> users-service
users-service -> SignUpForm (onSubmit) -> console.log -> Not right

## JWT

### Security Terms

encrypt <-> decrypt : Casear Cypher
plain text + key -> algo -> encrypted text

encode -> change format (no key) -> decode
<https://www.google.com.sg/search?q=singapore's+best+boot+camp>

hashing -> algo(text) -> hash

- one-way
- fast -> compared to encryption
- hash("abcdefg") -> "1234567"
- hash("abcdefgh") -> "52632877"

Authentication -> check if the person is who he says he is
Authorization -> check if the person can do he wants
