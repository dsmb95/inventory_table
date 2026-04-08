# 🚀 Instructions Manual: Deploying a Full-Stack Inventory Application

This class will guide you through validating your MongoDB Atlas setup, preparing your backend with environment variables, deploying your application to **Render**, and finally connecting your frontend to the deployed backend.

---

## ✅ Step 1: Validate MongoDB Atlas Setup

1. Log in to your **MongoDB Atlas** account.
2. Verify that you have a database named `inventory`.
3. Inside the database, confirm you have a collection named `products`.

### Example Model (Mongoose Schema)

```js
  name: String,
  sku: String,
  qty: Number,
  price: Number
```

### Insert Sample Data with `insertMany`
If you haven't created a database yet, you can use the below sample data
```js
import Product from "./models/Product.js";

await Product.insertMany([
  { name: "Widget A", sku: "WA-001", qty: 15, price: 9.99 },
  { name: "Widget B", sku: "WB-002", qty: 7, price: 14.5 },
  { name: "Widget C", sku: "WC-003", qty: 10, price: 19.99 },
  { name: "Widget D", sku: "WD-004", qty: 5, price: 24.99 },
  { name: "Widget E", sku: "WE-005", qty: 8, price: 29.99 },
  { name: "Widget F", sku: "WF-006", qty: 12, price: 34.99 },
  { name: "Widget G", sku: "WG-007", qty: 14, price: 39.99 },
  { name: "Widget H", sku: "WH-008", qty: 9, price: 44.99 },
  { name: "Widget I", sku: "WI-009", qty: 6, price: 49.99 },
  { name: "Widget J", sku: "WJ-010", qty: 11, price: 54.99 }
]);
```

---

## ✅ Step 2: Configure Backend Environment Variables

1. In  your `.env` file, update your MongoDB connection string as an environment variable:

```env
PORT=3000
MONGO_URI=mongodb+srv://<username>:<password>@cluster0.mongodb.net/inventory
```


---

## ✅ Step 3: Test Locally

1. Run the **backend server**:

```bash
npm start
```

2. Run the **frontend** project:

```bash
npm run dev
```

3. Test endpoints:

* Backend: `http://localhost:3000/api/products`
* Frontend: `http://localhost:5173` (or your dev server URL)

---

## ✅ Step 4: Push Code to GitHub

1. Initialize Git (if not already):

```bash
git init
git add .
git commit -m "Initial commit"
```

2. Create a new repository on GitHub.
3. Link your local project:

```bash
git remote add origin https://github.com/<username>/<repo-name>.git
git branch -M main
git push -u origin main
```

🔒 **Important:** Before committing, open your `.gitignore` file and make sure `.env` is listed there. This ensures sensitive credentials are **not pushed to GitHub**.

---

## ✅ Step 5: Deploy Backend to Render

1. Go to [Render](https://render.com) and sign up/login.
2. Click **New → Web Service**.
3. Connect your **GitHub account**.
4. Choose the repository you pushed.
5. Fill in the settings:

   * Environment: `Node`
   * Build Command: `npm install`
   * Start Command: `npm start`
6. Add **Environment Variables**:

   ```env
   PORT=3000
   MONGO_URI=<your MongoDB Atlas URI>
   ```
7. Deploy the service.

---

## ✅ Step 6: Validate Deployment

* After deployment, Render will give you a public URL:

  ```
  https://your-app.onrender.com
  ```
* Test it:

  ```
  https://your-app.onrender.com/products
  ```

  You should see your product list returned.

---

## ✅ Step 7: Connect Frontend to Remote Backend

1. Open your frontend project.
2. Update API calls to use the Render URL instead of localhost.

Example:

```js
useEffect(() => {
  fetch("https://your-app.onrender.com/products")
    .then(res => res.json())
    .then(data => setProducts(data));
}, []);
```

3. Restart your frontend server and verify the data is being pulled from the cloud.

---

## 🎯 Final Outcome

* Backend running online with **Render**.
* Database hosted on **MongoDB Atlas**.
* Frontend fetching data from your deployed backend.
* You now have a full-stack application deployed to the cloud!

---

✅ **Pro Tip for Students:** Keep your `.env` file local and never commit it to GitHub. Render has its own environment variable settings to keep credentials safe.