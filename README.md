# Inventory & Order Management API

This is a RESTful API for managing products and customer orders.

## Objective

To design and implement a RESTful API that evaluates backend system design, database modeling, transaction handling, and code quality.

## Tech Stack

- **Node.js**: JavaScript runtime environment
- **Express.js**: Web framework for Node.js
- **MongoDB**: NoSQL database for data storage
- **Mongoose**: Object Data Modeling (ODM) library for MongoDB
- **MongoDB Atlas**: Cloud database service that supports transactions

---

## Getting Started

Follow these instructions to get the project up and running on your local machine.

### Prerequisites

- [Node.js](https://nodejs.org/) (v18 or later)
- [npm](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/soehtetlin/inventory-order-api.git
    cd inventory-order-api
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Set up environment variables:**
    Create a file named `.env` in the root of the project directory. This file will hold your environment-specific configurations.

    You can choose to connect to either a local MongoDB database or a cloud-hosted MongoDB Atlas cluster.

    #### Option A: Using MongoDB Atlas (Recommended)

    1.  Copy the following into your `.env` file:
        ```env
        PORT=3000
        MONGODB_URI=
        ```
    2.  Replace the value of `MONGODB_URI` with your own connection string from MongoDB Atlas. It should look like this:
        `mongodb+srv://<username>:<password>@yourcluster.mongodb.net/your_database_name?retryWrites=true&w=majority`

    #### Option B: Using a Local MongoDB Database

    1.  Ensure you have MongoDB Community Server installed and running on your machine.
    2.  Copy the following into your `.env` file:
        ```env
        PORT=3000
        MONGODB_URI=mongodb://localhost:27017/inventory_order_db
        ```
        -   You can change `inventory_order_db` to any database name you prefer.
        -   **Note:** Using a local standalone MongoDB instance does not support transactions. The "Place Order" feature will work, but without the atomicity guarantee provided by transactions.

4.  **Run the development server:**
    ```bash
    npm run dev
    ```
    The server will start on `http://localhost:3000`.

---

## API Endpoints

Here are the available API endpoints. You can use tools like Postman or Thunder Client to test them.

### Product Management

| Method | Endpoint              | Description                      |
| :----- | :-------------------- | :------------------------------- |
| `POST` | `/api/products`       | Create a new product             |
| `GET`  | `/api/products`       | Get a list of all products       |
| `GET`  | `/api/products/:id`   | Get a single product by its ID   |
| `PUT`  | `/api/products/:id`   | Update an existing product       |
| `DELETE`| `/api/products/:id`  | Delete a product                 |

**Example `POST /api/products` Body:**
```json
{
    "name": "Laptop",
    "price": 1200,
    "stock": 50
}
```

## Testing

This project includes a suite of unit tests to ensure the reliability and correctness of the core business logic. The tests are written using the **Jest** framework.

### Key Areas Tested

**Product Controller:**

- Successful creation of a new product.
- Fetching all products and a single product by ID.
- Updating and deleting existing products.
- Error handling for invalid input (e.g., missing fields) and non-existent products.

**Order Controller:**

- Successful placement of a new order, ensuring product stock is correctly decremented.
- Error handling for insufficient stock.
- Logic for restoring product stock when an order is cancelled.
- Fetching all orders and orders by a specific customer.

### How to Run Tests

To run the entire test suite, use the following command from the project's root directory:

```bash
npm test