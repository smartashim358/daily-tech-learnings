
# Daily Tech Learnings Day 17 - Express & 3D Design

**Date:** 28 Jan 2026  
**Author:** Ashim Nepali  

---

## 1. Express.js Basics

Today, I focused on learning **Express.js**, a minimal and flexible Node.js framework for building web applications and APIs. Express makes server-side development much faster and easier by providing a simple interface for routing, middleware, and handling HTTP requests.

### Why Express.js?

- Lightweight and fast
- Easy routing and middleware support
- Works perfectly with JSON and REST APIs

---

## 2. Middleware in Express

Middleware functions in Express are functions that execute during the request-response cycle. They can:

- Process incoming requests
- Transform request data
- Handle errors
- Control access

### Example: Using JSON Middleware

```javascript
const express = require('express');
const app = express();

// Middleware to parse JSON data from requests
app.use(express.json());

app.get('/', (req, res) => {
    res.send('Hello World!');
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

Here, `express.json()` converts incoming JSON payloads into JavaScript objects, which makes them easy to work with in your routes.

---

## 3. Request (`req`) and Response (`res`) Methods

Express provides powerful objects to handle HTTP requests and responses:

### Common `req` properties:

- `req.params` → Access route parameters
- `req.query` → Access query strings
- `req.body` → Access JSON or form data from the client

### Common `res` methods:

- `res.send()` → Sends a response to the client
- `res.json()` → Sends a JSON response
- `res.status()` → Sets HTTP status codes
- `res.redirect()` → Redirects the client to another route

### Example: CRUD Routes

```javascript
const products = [];

// POST: Add a product
app.post('/products', (req, res) => {
    const product = req.body;
    products.push(product);
    res.status(201).json({ message: 'Product added', product });
});

// PUT: Update a product
app.put('/products/:id', (req, res) => {
    const id = req.params.id;
    products[id] = req.body;
    res.json({ message: 'Product updated', product: products[id] });
});

// DELETE: Remove a product
app.delete('/products/:id', (req, res) => {
    const id = req.params.id;
    const deleted = products.splice(id, 1);
    res.json({ message: 'Product deleted', deleted });
});
```

**Note:** Testing these routes can be easily done using **Postman**, which allows sending GET, POST, PUT, DELETE requests to your server.

---

## 4. 3D Design Introduction (Three.js)

Today, I also explored **3D design basics** using **Three.js**, a JavaScript library for creating 3D graphics in the browser.

### Why Three.js?

- Lightweight and browser-friendly
- Supports WebGL without deep knowledge of it
- Can create 3D models, animations, and interactive graphics

### Basic Example:

```javascript
import * as THREE from 'three';

// Create scene
const scene = new THREE.Scene();

// Create camera
const camera = new THREE.PerspectiveCamera(
  75, window.innerWidth / window.innerHeight, 0.1, 1000
);

// Create renderer
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

// Create a cube
const geometry = new THREE.BoxGeometry();
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);

// Camera position
camera.position.z = 5;

// Render loop
function animate() {
  requestAnimationFrame(animate);
  cube.rotation.x += 0.01;
  cube.rotation.y += 0.01;
  renderer.render(scene, camera);
}

animate();
```

This sets up a simple 3D cube that rotates continuously, giving a hands-on introduction to interactive 3D design.

---

## 5. Key Takeaways

1. Express.js simplifies backend development and API creation.  
2. Middleware is essential for handling requests, especially parsing JSON.  
3. Understanding `req` and `res` objects is crucial for building RESTful APIs.  
4. Postman is a helpful tool for testing backend routes.  
5. Three.js introduces exciting opportunities for creating interactive 3D web content.  

---

**Next Steps:**

- Practice more CRUD operations and complex routes in Express  
- Explore advanced middleware like authentication, logging, and error handling  
- Dive deeper into Three.js: lights, textures, and animations  

---

**End of Learnings**
