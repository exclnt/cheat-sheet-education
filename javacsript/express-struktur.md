#  Express.js API Starter

Ini adalah struktur proyek API menggunakan Express.js yang disusun dengan arsitektur modular. Cocok untuk REST API yang rapi, scalable, dan mudah dipelihara.

---

##  Struktur Folder
```
project-api/
├── node_modules/
├── src/
│ ├── controllers/ # Logika bisnis tiap route
│ ├── routes/ # Routing endpoint
│ ├── models/ # Skema dan koneksi database
│ ├── middlewares/ # Middleware (auth, error, dll)
│ ├── config/ # Konfigurasi DB, env, dll
│ ├── utils/ # Fungsi bantu (helper)
│ └── app.js # Konfigurasi utama Express
├── .env # Variabel lingkungan (port, db, dll)
├── package.json # Informasi dan dependencies project
├── server.js # Entry point menjalankan server
```

---


##  Penjelasan Folder
###  controllers/
Berisi logika bisnis untuk setiap route.

Contoh: userController.js

```js
exports.getAllUsers = (req, res) => {
  res.send('Semua user');
};
```
###  routes/
Berisi definisi endpoint dan hubungkan ke controller.

Contoh: userRoutes.js

```js
const express = require('express');
const router = express.Router();
const userController = require('../controllers/userController');

router.get('/', userController.getAllUsers);
router.post('/', userController.createUser);

module.exports = router;
```
###  models/
Berisi skema data dan model database.

Contoh: User.js

```js
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: String,
  email: String
});

module.exports = mongoose.model('User', userSchema);
```
###  middlewares/
Berisi middleware seperti autentikasi, validasi, dan error handler.

Contoh: authMiddleware.js

```js
module.exports = (req, res, next) => {
  const token = req.headers.authorization;
  if (token === 'valid-token') {
    next();
  } else {
    res.status(401).json({ error: 'Unauthorized' });
  }
};
```
###  config/
Berisi konfigurasi database, environment, dan lainnya.

Contoh: db.js

```js
const mongoose = require('mongoose');
const connectDB = async () => {
  await mongoose.connect(process.env.MONGO_URI);
  console.log('MongoDB Connected');
};
module.exports = connectDB;
```
###  utils/
Berisi fungsi bantu seperti token generator, hashing, dsb.

###  app.js
Mengatur middleware global, parsing body, dan routing utama.

```js
const express = require('express');
const cors = require('cors');
const morgan = require('morgan');
const userRoutes = require('./routes/userRoutes');
const errorHandler = require('./middlewares/errorHandler');

const app = express();
app.use(cors());
app.use(morgan('dev'));
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

app.use('/api/users', userRoutes);
app.use(errorHandler);

module.exports = app;
```
###  server.js
Menjalankan server dan koneksi ke database.

```js
require('dotenv').config();
const app = require('./src/app');
const connectDB = require('./src/config/db');

const PORT = process.env.PORT || 3000;

connectDB().then(() => {
  app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
  });
});
```