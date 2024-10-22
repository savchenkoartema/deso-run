# DeSo

## 1. Clone the Repository

First, clone the `run` repository to your local machine:

```bash
git clone https://github.com/deso-protocol/run.git
cd run
```

This will download the project to a folder called `run`.

---

## 2. Install Dependencies

After cloning the repository, you need to install the required dependencies using `npm`:

```bash
npm install
```

This will install all the packages necessary for the project.

---

## 3. Set Up Environment Variables

The `run` project requires some environment variables to work properly. Create a `.env` file in the root directory:

```bash
touch .env
```

In the `.env` file, add the following variables:

```bash
# .env
DESO_API_URL=https://node.deso.org/api
```

You can adjust the `DESO_API_URL` depending on which node you're interacting with (testnet or mainnet).

---

## 4. Running the Application

Once the environment variables are set, you can run the application with:

```bash
npm start
```

This command will start the server and you should see output like this:

```bash
> run@1.0.0 start /path-to-your-project/run
> node index.js

Server running on http://localhost:3000
```

Now, the project should be running at `http://localhost:3000`.

---

## 5. Key Features and Code Examples

Here are some basic functionalities of the DeSo Protocol that you can experiment with:

### a. **Creating a New User**

To create a new user, use the `createUser` method from the `deso-protocol` package:

```javascript
const deso = require('deso-protocol');

async function createUser() {
  const response = await deso.identity.createSeed();
  const seedHex = response.seedHex;
  console.log("New user seed:", seedHex);
}

createUser();
```

### b. **Fetching a User's Profile**

To fetch the profile of a specific user, you can use the following code:

```javascript
const deso = require('deso-protocol');

async function fetchProfile(publicKey) {
  const profile = await deso.user.getSingleProfile({
    PublicKeyBase58Check: publicKey
  });
  console.log(profile);
}

const publicKey = "BC1YLh...";
fetchProfile(publicKey);
```

Replace `BC1YLh...` with a valid public key.

### c. **Posting a Transaction**

You can use the DeSo protocol to post content on the blockchain:

```javascript
const deso = require('deso-protocol');

async function submitPost() {
  const request = {
    UpdaterPublicKeyBase58Check: "BC1YLh...",
    BodyObj: {
      Body: "This is my first post on DeSo!",
    },
    MinFeeRateNanosPerKB: 1000,
  };

  const response = await deso.posts.submitPost(request);
  console.log(response);
}

submitPost();
```

This snippet posts a message to the DeSo blockchain from the user with the public key `BC1YLh...`.

### d. **Sending Deso Tokens**

Here’s how you can send a transaction to transfer DeSo tokens between two users:

```javascript
const deso = require('deso-protocol');

async function sendDeso() {
  const response = await deso.transaction.sendDeso({
    SenderPublicKeyBase58Check: "BC1YLh...",
    RecipientPublicKeyOrUsername: "BC1YLf...",
    AmountNanos: 1000000, // Amount in DeSo nanos (1 DeSo = 1e9 nanos)
    MinFeeRateNanosPerKB: 1000
  });

  console.log(response);
}

sendDeso();
```

Replace the `SenderPublicKeyBase58Check` and `RecipientPublicKeyOrUsername` with actual keys.

---

## 6. Testing

To run tests for the `run` repository, use the following command:

```bash
npm test
```

This will execute the test suite and ensure that all functionalities are working as expected.

---

## 7. Deploying

To deploy the project, you can use services like **Heroku**, **Vercel**, or any other Node.js hosting platform.

For deployment on Heroku, for example:

```bash
heroku create
git push heroku master
```
