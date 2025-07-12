# Data Formats and Protocols

This section explores the data formats used in RESTful APIs and how Web3 applications interact with blockchains. It addresses common misconceptions and explains the correct protocols and tools used in modern web and blockchain-based systems.

---

## Data Formats in REST APIs

### **Myth**

> JSON is the only data format supported by REST APIs.

### **Reality**

REST is **format-agnostic**, meaning APIs can support **multiple data formats**. The choice depends on the server and the `Content-Type`/`Accept` headers set by the client and server.

### **Common Formats Supported by REST APIs**

| Format         | Description                                       | Usage Examples                          |
| -------------- | ------------------------------------------------- | --------------------------------------- |
| **JSON**       | Lightweight, human-readable, language-independent | Default for most modern APIs            |
| **XML**        | Structured, tag-based format                      | Common in enterprise or legacy systems  |
| **Plain Text** | Unstructured raw text                             | Debugging, logs, simple messages        |
| **YAML**       | Human-readable, configuration-oriented            | Rarely used in APIs, more for configs   |
| **HTML**       | Rendered text and markup                          | Often returned from web pages, not APIs |

**Example (JSON):**

```json
{
  "id": 123,
  "name": "John Doe",
  "email": "john@example.com"
}
```

### **Why JSON Is Preferred**

* Native support in JavaScript (e.g., `JSON.parse()` and `JSON.stringify()`).
* Lightweight and compact.
* Readable by humans and machines.
* Supported by nearly all programming languages.

### **Important Concepts**

* **Content Negotiation**: Clients use `Accept` headers to specify the desired response format (e.g., `Accept: application/json`).
* **Content-Type**: Servers use this header to indicate the response format (e.g., `Content-Type: application/xml`).

> **Key Point**: REST APIs are not limited to JSON; they can exchange data in any format agreed upon by the client and server.

---

## Web3 and Blockchain Protocols

### **Myth**

> Web3 applications use standard HTTP REST calls to interact with smart contracts.

### **Reality**

Web3 applications interact with blockchain nodes using **blockchain-specific protocols**, not REST. While HTTP or WebSocket is often used as a transport layer, the **communication protocol is typically JSON-RPC**.

### **Core Web3 Interaction Methods**

| Method                  | Description                                                            |
| ----------------------- | ---------------------------------------------------------------------- |
| **JSON-RPC**            | Remote procedure call protocol encoded in JSON; used to talk to nodes. |
| **WebSockets**          | Persistent connections for listening to blockchain events.             |
| **Web3.js / ethers.js** | JavaScript libraries that abstract RPC calls into simple functions.    |


### **How It Works**

* The method call (`getBalance`) is internally translated into a JSON-RPC request.
* The request is sent to an Ethereum node via HTTP or WebSocket.
* The node executes the call and returns the result to the dApp.

### **Important Distinctions from REST**

| Aspect            | REST API                                 | Web3 Interaction                        |
| ----------------- | ---------------------------------------- | --------------------------------------- |
| **Transport**     | HTTP(S)                                  | HTTP(S) or WebSocket                    |
| **Protocol**      | REST (stateless resources)               | JSON-RPC (procedure calls)              |
| **Server Type**   | Centralized server (e.g., API Gateway)   | Decentralized blockchain node           |
| **Call Style**    | Endpoint-based (`/users/1`)              | Method-based (`contract.methods.foo()`) |
| **State Changes** | Through HTTP verbs (`POST`, `PUT`, etc.) | Through transactions on the blockchain  |

> **Key Point**: Web3 applications communicate directly with **blockchain nodes**, not REST servers. JSON-RPC is the standard protocol, typically abstracted by libraries like `Web3.js`, `ethers.js`, or `viem`.


### **Example: Interacting with a Smart Contract Using Web3.js**

```javascript
const Web3 = require('web3');
const web3 = new Web3('https://mainnet.infura.io/v3/YOUR_PROJECT_ID');

const contract = new web3.eth.Contract(abi, contractAddress);

contract.methods.getBalance().call().then(console.log);
```

---

## Additional Considerations

* **Security**: Web3 calls for **signing transactions** (e.g., via MetaMask), unlike REST APIs where a token (e.g., JWT) is typically used.
* **Error Handling**: Blockchain nodes return structured error messages via RPC, not HTTP status codes like 404 or 500.
* **Data Consistency**: Blockchain data is immutable and append-only, unlike REST APIs where data is often updated or deleted.
