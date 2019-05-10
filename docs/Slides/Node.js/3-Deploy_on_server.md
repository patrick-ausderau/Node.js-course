# express and mongoose on jelasitc

## Prerequisite

You should already have created your jelastic account and got it activated.

(In no order)

* Create a github/gitlab/bitbuckets/gnu savanah/framagit/... project
  * with .gitignore for node
  * (readme, licences,...)

* Generate [public/private keys](https://docs.jelastic.com/ssh-generate-key) (DO NOT USE ONE OF YOUR EXISTING KEY PAIR)
  * public key to [github and private to jelastic](https://docs.jelastic.com/git-ssh)

* In Jelastic, create a NodeJS (10.x or11.x) ** with npm ** with MongoDB (4.x) servers and reserve 2 cloudlets
  * Once created, you should receive an email with DB credentials
    * Create your [cat database](/W2-2-NoSQL-MongoDB-mongoose.html) 
    * Create a [user with read/write permissions](https://docs.mongodb.com/manual/tutorial/enable-authentication/#create-additional-users-as-needed-for-your-deployment) (or follow the link from your DB email) to your jelastic cat database

## Locally

1. `git clone` your repo on your local computer
1. add `.env` in the .gitignore
1. do your normal `npm init` 
  * your main should be `server.js` (jelastic default)
1. do your normal `npm install --save` all required libraries
1. also install [dotenv](https://www.npmjs.com/package/dotenv) 
1. create a `.env` file at the root of your repo (this is [why](https://12factor.net/config))
  * add `DB_HOST`, `DB_PORT`, `DB_USER` and `DB_PASSWORD` which match your localhost db settings
1. edit your `server.js` and connect to the database using your env const 
```javascript
mongoose.connect(`mongodb://${process.env.DB_USER}:${process.env.DB_PASS}@${process.env.DB_HOST}:${process.env.DB_PORT}/cat`).then(() => {/* ... */}
```
1. Test locally `node -r dotenv/config server.js` and update your package.json start script
1. `git commit -m` your local changes

## Remote

1. `git push` your local changes to your remote repo
1. in jelastic, [deploy your node project via git](https://docs.jelastic.com/nodejs-git-svn) using your public/private key (and consider periodic autoredeploy)
1. Once cloned, create the `.env` file (on your Nodejs server, click config button then navigate to Favourites -> ROOT), this time matching your jelastic MongoDB settings

---

### Example

* [express+mongo+.env](https://github.com/patrick-ausderau/testdb) (was deployed successfully)
