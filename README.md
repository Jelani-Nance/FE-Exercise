# FE-Exercise

// Dog
interface Dog {
  id: string;
  img: string;
  name: string;
  age: number;
  zip_code: string;
  breed: string;
}

// Location
interface Location {
  zip_code: string;
  latitude: number;
  longitude: number;
  city: string;
  state: string;
  county: string;
}

// Login

const express = require('express');
const app = express();

app.use(express.json());

app.post('/auth/login', (req,res) => {
  // Extract request body parameters
  const { name, email } = req.body;
  
  // Perform login logic and generate access token
  
  // Response headers
  res.json({
    name: name,
    email: email,
    'fetch-access-token': 'access_token_here',
    token_expiry: new Date(Date.now() + 60 * 60 * 1000)
  });
});

app.post('/auth/logout', (req, res) => {
  // Perform logout logic and invalidate access token
  // ...

  // Response headers
  res.json({
    message: 'Logged out successfully'
  });
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});

const express = require('express');
const app = express();
app.use(express.json());

// GET /dogs/breeds
app.get('/dogs/breeds', (req, res) => {
  const breeds = ['Labrador Retriever', 'Golden Retriever', 'German Shepherd', 'Poodle', 'Bulldog', 'Beagle', 'Rottweiler', 'Boxer', 'Siberian Husky', 'Chihuahua'];
  res.json(breeds);
});

// GET /dogs/search
app.get('/dogs/search', (req, res) => {
  const { breeds, zipCodes, ageMin, ageMax, size, from, sort } = req.query;
  const resultIds = ['123', '456', '789']; 
  const total = resultIds.length; 
  const next = null; 
  const prev = null; 
  const response = { resultIds, total, next, prev };
  res.json(response);
});

const port = 3000;
app.listen(port, () => {
  console.log(`Server started on port ${port}`);
});

const express = require('express');
const app = express();
app.use(express.json());

// POST /dogs
app.post('/dogs', (req, res) => {
  // Fetch dog objects based on the provided dog IDs
  const dogObjects = fetchDogObjects(req.body);
  res.json(dogObjects);
});

// POST /dogs/match
app.post('/dogs/match', (req, res) => {
  // Select a single dog ID from the provided list
  const matchedDogId = selectMatchedDogId(req.body);
  res.json({ match: matchedDogId });
});

// POST /locations
app.post('/locations', (req, res) => {
  // Fetch Location objects based on the provided ZIP codes
  const locationObjects = fetchLocationObjects(req.body);
  res.json(locationObjects);
});

// POST /locations/search
app.post('/locations/search', (req, res) => {
  // Perform search based on the provided filters
  const { city, states, geoBoundingBox, size, from } = req.body;
  const searchResults = performSearch(city, states, geoBoundingBox, size, from);
  res.json(searchResults);
});

// Start the server
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});

// Dummy implementations of fetchDogObjects, selectMatchedDogId, fetchLocationObjects, performSearch
function fetchDogObjects(dogIds) {
  // Replace with actual implementation
  return dogIds.map(id => ({ id, name: `Dog ${id}` }));
}

function selectMatchedDogId(dogIds) {
  // Replace with actual implementation
  return dogIds[Math.floor(Math.random() * dogIds.length)];
}

function fetchLocationObjects(zipCodes) {
  // Replace with actual implementation
  return zipCodes.map(zipCode => ({ zipCode, city: `City for ${zipCode}` }));
}

function performSearch(city, states, geoBoundingBox, size, from) {
  // Replace with actual implementation
  return {
    results: [],
    total: 0
  };
}
