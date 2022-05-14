# Fylo Ver. 2

### What is changed compared to Version 1?

- Using Mapbox API
- Using MongoDB Connection and MongoDB Atlas
    - Version 1 was without MongoDB Connection
- More Boostrap 5 Syntax used

### Ininital Setting to run this project locally

You have first to clone your repo:

```bash
git clone https://github.com/mininpark/Ver2_Fylo_darktheme
```

then when the repository has been cloned:

```bash
cd your-destination-folder
npm install # installing the dependencies
npm start 
# or 
nodemon app.js
```

If you want to see the static website without NodeJS, Express, MongoDB, please go to version 3. Version 3 is downgraded from version 2. 

[https://github.com/mininpark/Ver3-Fylo-Darkthema](https://github.com/mininpark/Ver3-Fylo-Darkthema)

## My process

### Built with

- MongoDB, Mongo DB Atlas
- Mapbox API
- Bootstrap
    - Modal, Accordion, List, and many different Bootstrap attribution
- NodeJS, Express

### What I learned

CRUD, Express and MongoDB are big words for me who has never touched many server-side programming in life. 

**[Express](https://expressjs.com/) is a framework for building web applications on top of [Node.js](https://nodejs.org/en/)**. It simplifies the server creation process that is already available in Node. In case you were wondering, Node allows you to use JavaScript as your server-side language.

**[MongoDB](https://www.mongodb.com/) is a database**. This is the place where you store information for your websites (or applications).

**[CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) is an acronym for Create, Read, Update and Delete**. It is a set of operations we get servers to execute (`POST`, `GET`, `PUT` and `DELETE` requests respectively). This is what each operation does:

### Users’ Input will be collected and saved in my MongoDB

- Setting with my MongoDB

```jsx
const MongoClient = require('mongodb').MongoClient

MongoClient.connect('mongodb+srv://admin:admin@<cluster0.tpwst.mongodb.net/myFirstDatabase?retryWrites=true&w=majority', {
    useUnifiedTopology: true})
    .then(client => {
        console.log("MangoDB Connected")
        const db = client.db('fylo-database')
        const fyloCollection = db.collection('fylo')

```

- app.**get** and app.**post**

```jsx
            //Middlewares and other routes
            app.use(bodyParser.urlencoded({ extended:true }))
            app.use(express.static(path.join(__dirname, 'public')))

            app.get('/', (req, res, next) => {
                res.sendFile(__dirname + '/public/index.html')
                db.collection('fylo').find().toArray()
                    .then(results => {
                        console.log(results)
                    })
                    .catch(error => console.log.error(error))
            });
//with POST action will be inserted to my fyloCollection
            app.post('/sent', (req,res) => {
                fyloCollection.insertOne(req.body)
                .then(result => {
                  res.redirect(`/`)
                  console.log('Data added')
                })
                .catch(error => console.error(error))
            })
```

- **app.listen**

```jsx
            const server = app.listen(process.env.PORT || 8080, ()=> {
                const port = server.address().port;
                console.log(`Server is working on ${port}`);
            });
      })
    .catch(err => console.log(err))
```

### Mailbox API

```jsx
<script src="https://api.mapbox.com/mapbox-gl-js/v2.8.2/mapbox-gl.js"></script>
  <script>
    //map
  mapboxgl.accessToken = 'pk.eyJ1IjoiaHVubWlucGFyayIsImEiOiJjbDM0bmhkNjMwd3A1M2twNXE1czJwdTFhIn0.S1fFg0WMrkWe-tBt3QYX4Q';
  const map = new mapboxgl.Map({
  container: 'map', // container ID
  style: 'mapbox://styles/mapbox/streets-v11', // style URL
  center: [8.466727780617589,49.48608884048795], // starting position [lng, lat]
  zoom: 14 // starting zoom
  })
  </script>
```

### Useful resources

- [CRUD Tutorial](https://zellwk.com/blog/crud-express-mongodb/) - This helped me a lot to understand the deeper and wide view of CRUD Web-APP.
