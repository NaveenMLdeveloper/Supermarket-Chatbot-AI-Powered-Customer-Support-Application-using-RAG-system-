Supermarket Chatbot
A Retrieval-Augmented Generation (RAG) based chatbot for supermarket customer support.
📜 Project Overview
The Supermarket Chatbot is a web-based application designed to assist supermarket customers by answering queries about product availability, prices, stock quantities, and categories. It uses natural language processing (NLP) to understand customer queries and provides friendly, concise responses. The chatbot leverages a Retrieval-Augmented Generation (RAG) pipeline to retrieve relevant product information from a MySQL database and generate responses using the DeepSeek V3 0324 (free) model via OpenRouter.
Purpose

Enhance customer support with an automated, 24/7 assistant.
Reduce workload on human staff by handling repetitive queries.
Improve customer experience with quick, accurate responses.

Features

Semantic search for products using FAISS and Sentence Transformers.
Natural language response generation using DeepSeek V3 0324 (free) via OpenRouter.
Fuzzy matching to handle misspelled queries (e.g., "coka cola" → "Coca Cola").
Modern UI with chat bubbles, loading animation, and clear chat functionality.
Logging for debugging and monitoring.

🛠️ Technologies Used

Flask: Lightweight web framework for the backend.
MySQL: Relational database to store product data.
FAISS: For efficient similarity search of product embeddings.
Sentence Transformers (all-MiniLM-L6-v2): To generate embeddings for semantic search.
OpenRouter API (DeepSeek V3 0324): For natural language response generation.
FuzzyWuzzy: For fuzzy string matching.
Python Libraries: requests, python-dotenv, numpy, watchdog.

📂 Project Structure
Supermarket-Chatbot/
│
├── data/
│   ├── faiss_index/
│   │   └── product_index.faiss      # FAISS index for product embeddings
│   └── mappings/
│       └── product_mapping.pkl      # Mapping of FAISS indices to product IDs
├── src/
│   ├── app.py                       # Flask app (backend)
│   ├── build_index.py               # Script to build FAISS index
│   ├── db_connect.py                # MySQL database connection
│   ├── rag_pipeline.py              # RAG pipeline for query processing
│   └── utils.py                     # Utility functions (logger, config)
├── templates/
│   └── chatbot.html                 # UI template
├── .env                             # Environment variables (API key, model)
├── supermarket_chatbot.log          # Log file for debugging
├── README.md                        # Project documentation
└── workflow_diagram.png             # Workflow diagram (to be added)

🖼️ Workflow Diagram
The following diagram illustrates the end-to-end workflow of the Supermarket Chatbot:

🚀 Getting Started
Follow these steps to set up and run the Supermarket Chatbot on your local machine.
Prerequisites

Python 3.8+: Ensure Python is installed.
MySQL: Install MySQL and set up a database.
OpenRouter API Key: Sign up at OpenRouter and obtain an API key for the DeepSeek V3 0324 (free) model.

Step 1: Clone the Repository
git clone <repository-url>
cd Supermarket-Chatbot

Step 2: Set Up a Virtual Environment
python -m venv myenv
source myenv/bin/activate  # On Windows: myenv\Scripts\activate

Step 3: Install Dependencies
Install the required Python packages:
pip install flask mysql-connector-python faiss-cpu sentence-transformers requests fuzzywuzzy python-dotenv watchdog numpy

Step 4: Configure MySQL Database

Start your MySQL server.

Create a database named Supermarket:
CREATE DATABASE Supermarket;


Create the Product_details table:
USE Supermarket;
CREATE TABLE Product_details (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    stock_quantity INT NOT NULL,
    category VARCHAR(100),
    description TEXT
);


Insert sample products:
INSERT INTO Product_details (name, price, stock_quantity, category, description)
VALUES 
    ('Orange (1kg)', 3.50, 40, 'Fruits', 'Fresh oranges, 1kg pack'),
    ('Coca Cola', 1.99, 50, 'Beverages', 'A refreshing cola drink'),
    ('Apple (1kg)', 2.99, 40, 'Fruits', 'Fresh apples, 1kg pack'),
    ('Banana (1 dozen)', 1.50, 60, 'Fruits', 'Fresh bananas, 1 dozen');


Update src/db_connect.py with your MySQL credentials (if different):
# src/db_connect.py
mysql_config = {
    'host': 'localhost',
    'user': 'your_mysql_user',
    'password': 'your_mysql_password',
    'database': 'Supermarket'
}



Step 5: Configure Environment Variables
Create a .env file in the project root and add your OpenRouter API key and model:
DEEPSEEK_API_KEY=your_openrouter_api_key
LLM_MODEL=deepseek/deepseek-chat-v3-0324:free

Replace your_openrouter_api_key with your actual API key.
Step 6: Build the FAISS Index
Run the build_index.py script to generate the FAISS index and mappings:
python src/build_index.py

This will create:

data/faiss_index/product_index.faiss
data/mappings/product_mapping.pkl

Step 7: Run the Application
Start the Flask server:
python src/app.py

Step 8: Access the Chatbot
Open your browser and navigate to:
http://localhost:5000

You’ll see the Supermarket Chatbot UI. Start asking questions like:

“How much is Orange (1kg)?”
“Do you have Coca Cola in stock?”
“List out the available product list.”

🧪 Testing the Chatbot
Sample Queries

Price Inquiry: “How much is Orange (1kg)?”
Expected: “The price of Orange (1kg) is $3.50.”


Availability Check: “Do you have Coca Cola in stock?”
Expected: “Yes, we have Coca Cola in stock! We have 50 units available at $1.99 each.”


Product List: “List out the available product list.”
Expected: “Here are some available products: Apple (1kg) - $2.99, Banana (1 dozen) - $1.50, Coca Cola - $1.99, …”


Misspelled Query: “How much is coka cola?”
Expected: “The price of Coca Cola is $1.99.”



Debugging

Check supermarket_chatbot.log for logs and errors.
Ensure MySQL is running and the database is populated.
Verify your OpenRouter API key is valid.

📋 End-to-End Workflow Summary

Setup: Clone the repository, set up a virtual environment, and install dependencies.
Database: Configure MySQL, create the Supermarket database, and populate the Product_details table.
Environment: Add your OpenRouter API key and model to .env.
Index Building: Run build_index.py to create the FAISS index and mappings.
Run: Start the Flask app with python src/app.py.
Interact: Access http://localhost:5000 and start asking questions.

🔮 Future Improvements

Add support for discounts and offers.
Expand the product database (e.g., 100+ items).
Enhance the UI with voice input or product images.
Improve query handling for complex questions (e.g., “Compare the prices of all juices”).

📞 Contact
For any questions or support, please contact Naveen Kumar at naveenpalani75@.

Developed by: [Your Name]Date: May 12, 2025
Supermarket Chatbot
A Retrieval-Augmented Generation (RAG) based chatbot for supermarket customer support.
📜 Project Overview
The Supermarket Chatbot is a web-based application designed to assist supermarket customers by answering queries about product availability, prices, stock quantities, and categories. It uses natural language processing (NLP) to understand customer queries and provides friendly, concise responses. The chatbot leverages a Retrieval-Augmented Generation (RAG) pipeline to retrieve relevant product information from a MySQL database and generate responses using the DeepSeek V3 0324 (free) model via OpenRouter.
Purpose

Enhance customer support with an automated, 24/7 assistant.
Reduce workload on human staff by handling repetitive queries.
Improve customer experience with quick, accurate responses.

Features

Semantic search for products using FAISS and Sentence Transformers.
Natural language response generation using DeepSeek V3 0324 (free) via OpenRouter.
Fuzzy matching to handle misspelled queries (e.g., "coka cola" → "Coca Cola").
Modern UI with chat bubbles, loading animation, and clear chat functionality.
Logging for debugging and monitoring.

🛠️ Technologies Used

Flask: Lightweight web framework for the backend.
MySQL: Relational database to store product data.
FAISS: For efficient similarity search of product embeddings.
Sentence Transformers (all-MiniLM-L6-v2): To generate embeddings for semantic search.
OpenRouter API (DeepSeek V3 0324): For natural language response generation.
FuzzyWuzzy: For fuzzy string matching.
Python Libraries: requests, python-dotenv, numpy, watchdog.

📂 Project Structure
Supermarket-Chatbot/
│
├── data/
│   ├── faiss_index/
│   │   └── product_index.faiss      # FAISS index for product embeddings
│   └── mappings/
│       └── product_mapping.pkl      # Mapping of FAISS indices to product IDs
├── src/
│   ├── app.py                       # Flask app (backend)
│   ├── build_index.py               # Script to build FAISS index
│   ├── db_connect.py                # MySQL database connection
│   ├── rag_pipeline.py              # RAG pipeline for query processing
│   └── utils.py                     # Utility functions (logger, config)
├── templates/
│   └── chatbot.html                 # UI template
├── .env                             # Environment variables (API key, model)
├── supermarket_chatbot.log          # Log file for debugging
├── README.md                        # Project documentation
└── workflow_diagram.png             # Workflow diagram (to be added)

🖼️ Workflow Diagram
The following diagram illustrates the end-to-end workflow of the Supermarket Chatbot:

🚀 Getting Started
Follow these steps to set up and run the Supermarket Chatbot on your local machine.
Prerequisites

Python 3.8+: Ensure Python is installed.
MySQL: Install MySQL and set up a database.
OpenRouter API Key: Sign up at OpenRouter and obtain an API key for the DeepSeek V3 0324 (free) model.

Step 1: Clone the Repository
git clone <repository-url>
cd Supermarket-Chatbot

Step 2: Set Up a Virtual Environment
python -m venv myenv
source myenv/bin/activate  # On Windows: myenv\Scripts\activate

Step 3: Install Dependencies
Install the required Python packages:
pip install flask mysql-connector-python faiss-cpu sentence-transformers requests fuzzywuzzy python-dotenv watchdog numpy

Step 4: Configure MySQL Database

Start your MySQL server.

Create a database named Supermarket:
CREATE DATABASE Supermarket;


Create the Product_details table:
USE Supermarket;
CREATE TABLE Product_details (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    stock_quantity INT NOT NULL,
    category VARCHAR(100),
    description TEXT
);


Insert sample products:
INSERT INTO Product_details (name, price, stock_quantity, category, description)
VALUES 
    ('Orange (1kg)', 3.50, 40, 'Fruits', 'Fresh oranges, 1kg pack'),
    ('Coca Cola', 1.99, 50, 'Beverages', 'A refreshing cola drink'),
    ('Apple (1kg)', 2.99, 40, 'Fruits', 'Fresh apples, 1kg pack'),
    ('Banana (1 dozen)', 1.50, 60, 'Fruits', 'Fresh bananas, 1 dozen');


Update src/db_connect.py with your MySQL credentials (if different):
# src/db_connect.py
mysql_config = {
    'host': 'localhost',
    'user': 'your_mysql_user',
    'password': 'your_mysql_password',
    'database': 'Supermarket'
}



Step 5: Configure Environment Variables
Create a .env file in the project root and add your OpenRouter API key and model:
DEEPSEEK_API_KEY=your_openrouter_api_key
LLM_MODEL=deepseek/deepseek-chat-v3-0324:free

Replace your_openrouter_api_key with your actual API key.
Step 6: Build the FAISS Index
Run the build_index.py script to generate the FAISS index and mappings:
python src/build_index.py

This will create:

data/faiss_index/product_index.faiss
data/mappings/product_mapping.pkl

Step 7: Run the Application
Start the Flask server:
python src/app.py

Step 8: Access the Chatbot
Open your browser and navigate to:
http://localhost:5000

You’ll see the Supermarket Chatbot UI. Start asking questions like:

“How much is Orange (1kg)?”
“Do you have Coca Cola in stock?”
“List out the available product list.”

🧪 Testing the Chatbot
Sample Queries

Price Inquiry: “How much is Orange (1kg)?”
Expected: “The price of Orange (1kg) is $3.50.”


Availability Check: “Do you have Coca Cola in stock?”
Expected: “Yes, we have Coca Cola in stock! We have 50 units available at $1.99 each.”


Product List: “List out the available product list.”
Expected: “Here are some available products: Apple (1kg) - $2.99, Banana (1 dozen) - $1.50, Coca Cola - $1.99, …”


Misspelled Query: “How much is coka cola?”
Expected: “The price of Coca Cola is $1.99.”



Debugging

Check supermarket_chatbot.log for logs and errors.
Ensure MySQL is running and the database is populated.
Verify your OpenRouter API key is valid.

📋 End-to-End Workflow Summary

Setup: Clone the repository, set up a virtual environment, and install dependencies.
Database: Configure MySQL, create the Supermarket database, and populate the Product_details table.
Environment: Add your OpenRouter API key and model to .env.
Index Building: Run build_index.py to create the FAISS index and mappings.
Run: Start the Flask app with python src/app.py.
Interact: Access http://localhost:5000 and start asking questions.

🔮 Future Improvements

Add support for discounts and offers.
Expand the product database (e.g., 100+ items).
Enhance the UI with voice input or product images.
Improve query handling for complex questions (e.g., “Compare the prices of all juices”).

