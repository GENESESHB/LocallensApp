# LocallensApp
@mobileApp
### Simple React Native Component Example

Here’s a basic example of a React Native component that displays a welcome message, an image, and a button:

```js
import React from 'react';
import { View, Text, Image, Button, StyleSheet } from 'react-native';

const WelcomeScreen = () => {
  const handlePress = () => {
    alert('Welcome to React Native!');
  };

  return (
    <View style={styles.container}>
      <Text style={styles.welcomeText}>Welcome to My App!</Text>
      <Image
        style={styles.logo}
        source={{ uri: 'https://reactnative.dev/img/tiny_logo.png' }}
      />
      <Button title="Press Me" onPress={handlePress} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f5f5f5',
  },
  welcomeText: {
    fontSize: 24,
    marginBottom: 20,
  },
  logo: {
    width: 100,
    height: 100,
    marginBottom: 20,
  },
});

export default WelcomeScreen;
```

### Steps to Build a Full Application (Frontend + Backend)

To create a full application with both a **frontend (React Native)** and a **backend (Node.js with Express and MongoDB)**, follow these steps:

---

### 1. **Set Up the Backend (Node.js with Express and MongoDB)**

#### a. Install Node.js and Create a New Project
First, install Node.js on your machine, and then create a new Node.js project:

```bash
mkdir backend
cd backend
npm init -y
```

#### b. Install Express and Mongoose (for MongoDB)
Install the necessary packages for Express (web framework) and Mongoose (ODM for MongoDB):

```bash
npm install express mongoose
```

#### c. Create a Simple API in `server.js`
```js
const express = require('express');
const mongoose = require('mongoose');

const app = express();
app.use(express.json()); // For parsing JSON requests

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/myapp', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log('MongoDB connected'))
  .catch(err => console.log(err));

// Define a schema and model for user data
const userSchema = new mongoose.Schema({
  name: String,
  email: String
});

const User = mongoose.model('User', userSchema);

// Create a simple route
app.get('/', (req, res) => {
  res.send('Hello World');
});

// Route to create a user
app.post('/users', async (req, res) => {
  const { name, email } = req.body;
  const user = new User({ name, email });
  await user.save();
  res.send(user);
});

// Start the server
app.listen(5000, () => console.log('Server running on port 5000'));
```

#### d. Test the API
You can use tools like **Postman** or **cURL** to test the API:

- `GET http://localhost:5000/` to check if the server is running.
- `POST http://localhost:5000/users` with a JSON body to add a new user:
  ```json
  {
    "name": "John Doe",
    "email": "johndoe@example.com"
  }
  ```

#### e. MongoDB
Make sure MongoDB is installed and running on your system. You can install it from [MongoDB’s official site](https://www.mongodb.com/try/download/community).

---

### 2. **Set Up the Frontend (React Native)**

#### a. Install React Native CLI
If you haven't set up React Native yet, install the CLI:

```bash
npm install -g react-native-cli
```

#### b. Create a New React Native Project
```bash
react-native init MobileApp
cd MobileApp
```

#### c. Install Axios for API Calls
You will need Axios to make API requests to your backend:

```bash
npm install axios
```

#### d. Create a Component to Fetch and Display Data
You can create a screen that fetches user data from the backend and displays it.

```js
import React, { useEffect, useState } from 'react';
import { View, Text, Button, FlatList, StyleSheet } from 'react-native';
import axios from 'axios';

const UsersScreen = () => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetchUsers();
  }, []);

  const fetchUsers = async () => {
    try {
      const response = await axios.get('http://10.0.2.2:5000/users'); // Use 10.0.2.2 for Android emulator
      setUsers(response.data);
    } catch (error) {
      console.error('Error fetching users:', error);
    }
  };

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Users List</Text>
      <FlatList
        data={users}
        keyExtractor={(item) => item._id}
        renderItem={({ item }) => (
          <Text style={styles.user}>{item.name} ({item.email})</Text>
        )}
      />
      <Button title="Refresh" onPress={fetchUsers} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
  },
  header: {
    fontSize: 24,
    marginBottom: 10,
  },
  user: {
    fontSize: 18,
    marginBottom: 5,
  },
});

export default UsersScreen;



Simple React Native Component Example
Here’s a basic example of a React Native component that displays a welcome message, an image, and a button:

js
Copier le code
import React from 'react';
import { View, Text, Image, Button, StyleSheet } from 'react-native';

const WelcomeScreen = () => {
  const handlePress = () => {
    alert('Welcome to React Native!');
  };

  return (
    <View style={styles.container}>
      <Text style={styles.welcomeText}>Welcome to My App!</Text>
      <Image
        style={styles.logo}
        source={{ uri: 'https://reactnative.dev/img/tiny_logo.png' }}
      />
      <Button title="Press Me" onPress={handlePress} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f5f5f5',
  },
  welcomeText: {
    fontSize: 24,
    marginBottom: 20,
  },
  logo: {
    width: 100,
    height: 100,
    marginBottom: 20,
  },
});

export default WelcomeScreen;
Steps to Build a Full Application (Frontend + Backend)
To create a full application with both a frontend (React Native) and a backend (Node.js with Express and MongoDB), follow these steps:

1. Set Up the Backend (Node.js with Express and MongoDB)
a. Install Node.js and Create a New Project
First, install Node.js on your machine, and then create a new Node.js project:

bash
Copier le code
mkdir backend
cd backend
npm init -y
b. Install Express and Mongoose (for MongoDB)
Install the necessary packages for Express (web framework) and Mongoose (ODM for MongoDB):

bash
Copier le code
npm install express mongoose
c. Create a Simple API in server.js
js
Copier le code
const express = require('express');
const mongoose = require('mongoose');

const app = express();
app.use(express.json()); // For parsing JSON requests

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/myapp', { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log('MongoDB connected'))
  .catch(err => console.log(err));

// Define a schema and model for user data
const userSchema = new mongoose.Schema({
  name: String,
  email: String
});

const User = mongoose.model('User', userSchema);

// Create a simple route
app.get('/', (req, res) => {
  res.send('Hello World');
});

// Route to create a user
app.post('/users', async (req, res) => {
  const { name, email } = req.body;
  const user = new User({ name, email });
  await user.save();
  res.send(user);
});

// Start the server
app.listen(5000, () => console.log('Server running on port 5000'));
d. Test the API
You can use tools like Postman or cURL to test the API:

GET http://localhost:5000/ to check if the server is running.
POST http://localhost:5000/users with a JSON body to add a new user:
json
Copier le code
{
  "name": "John Doe",
  "email": "johndoe@example.com"
}
e. MongoDB
Make sure MongoDB is installed and running on your system. You can install it from MongoDB’s official site.

2. Set Up the Frontend (React Native)
a. Install React Native CLI
If you haven't set up React Native yet, install the CLI:

bash
Copier le code
npm install -g react-native-cli
b. Create a New React Native Project
bash
Copier le code
react-native init MobileApp
cd MobileApp
c. Install Axios for API Calls
You will need Axios to make API requests to your backend:

bash
Copier le code
npm install axios
d. Create a Component to Fetch and Display Data
You can create a screen that fetches user data from the backend and displays it.

js
Copier le code
import React, { useEffect, useState } from 'react';
import { View, Text, Button, FlatList, StyleSheet } from 'react-native';
import axios from 'axios';

const UsersScreen = () => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetchUsers();
  }, []);

  const fetchUsers = async () => {
    try {
      const response = await axios.get('http://10.0.2.2:5000/users'); // Use 10.0.2.2 for Android emulator
      setUsers(response.data);
    } catch (error) {
      console.error('Error fetching users:', error);
    }
  };

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Users List</Text>
      <FlatList
        data={users}
        keyExtractor={(item) => item._id}
        renderItem={({ item }) => (
          <Text style={styles.user}>{item.name} ({item.email})</Text>
        )}
      />
      <Button title="Refresh" onPress={fetchUsers} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
  },
  header: {
    fontSize: 24,
    marginBottom: 10,
  },
  user: {
    fontSize: 18,
    marginBottom: 5,
  },
});

export default UsersScreen;



