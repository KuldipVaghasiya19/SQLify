# SQLify 🚀

Introducing SQLify, our AI-powered tool designed to seamlessly bridge the gap between human language and complex database queries. Revolutionizing data retrieval, SQLify enables users to effortlessly pose questions in natural language, transforming them into precise SQL queries for efficient database interrogation.

## Overview 🌐

This is an end-to-end LLM project based on Google Palm and Langchain. We are building a system that can talk to SQL databases. Users ask questions in natural language, and the system generates answers by converting those questions into an SQL query and then executing that query on an SQL database.

## Project Highlights 🌟

  - Technologies used:
    
  - Google Palm LLM 🌴
  - Hugging Face embeddings 🤗
  - Streamlit for UI 🚀
  - Langchain framework 🛠️
  - Chromadb as a vector store 🧬
  - Few-shot learning 📚

In the UI, users can ask questions in natural language, and SQLify will produce the answers.

---

## 🧠 Architecture & Workflow

This system is designed to transform **natural language questions** into **executable SQL queries**, enabling intelligent and efficient interaction with structured databases. It integrates several modern tools—**LLMs, vector databases, semantic search, and orchestration frameworks**—to build a seamless question-answering pipeline over SQL databases.

### 🔄 End-to-End Flow

1. **🔤 Natural Language Input**
   The user initiates the interaction by asking a question in plain English. Example queries include:

   * *“How much revenue did our store generate after discounts?”*
   * *“What is the total inventory value for all S-size T-shirts?”*

2. **🔍 Embedding & Semantic Search via Hugging Face(Sentence-transformers/all-MiniLM-L6-v2) + ChromaDB**

   * A set of **sample questions and their corresponding SQL queries** are pre-curated and embedded into high-dimensional vector representations using **Hugging Face** embedding models.
   * These vectors are stored in **ChromaDB**, a performant **vector database**, enabling **semantic similarity search**.
   * When a new user question comes in, it is embedded and compared against existing samples to find the **most semantically similar examples**, providing contextual grounding for the LLM.

3. **🧩 LangChain Orchestration**

   * **LangChain** acts as the orchestration layer, connecting all components: the **LLM**, **ChromaDB**, and the **SQL database**.
   * It utilizes tools such as:

     * `SQLDatabaseChain`: for safe and structured interaction with the SQL DB.
     * `FewShotPromptTemplate`: to supply the LLM with relevant examples retrieved from ChromaDB.

4. **🧠 SQL Query Generation using Google PaLM 2**

   * The **Google PaLM 2** LLM receives the user query, along with retrieved few-shot examples and database schema context.
   * It then generates the appropriate SQL query (e.g., calculating post-discount revenue, aggregating inventory by size, etc.).
   * If uncertainty or ambiguity is detected, it leverages **semantic retrieval results from ChromaDB** to improve accuracy.

5. **🗄️ SQL Database Interaction**

   * The generated SQL query is executed against the **underlying relational database** (e.g., MySQL/PostgreSQL).
   * The query may involve joins, filters, groupings, and aggregations based on the user's request.

6. **📤 Answer Retrieval & Display**

   * The result from the SQL query is formatted and presented back to the user in a readable format.
   * The interface, labeled “AtliQ T-Shirts: Database Q\&A,” ensures a smooth and intuitive experience.

---

### 🧱 Core Components

| Component             | Role                                                            |
| --------------------- | --------------------------------------------------------------- |
| Hugging Face          | Converts text to embeddings for semantic matching               |
| ChromaDB              | Stores question-query pairs as vectors for fast retrieval       |
| LangChain             | Bridges the LLM, vector DB, and SQL DB into one coherent system |
| Google PaLM 2         | Understands natural language and generates SQL                  |
| SQLDatabaseChain      | Facilitates structured SQL interactions                         |
| FewShotPromptTemplate | Supplies relevant SQL examples to guide query generation        |

---

### 🎯 Key Advantages

* **Natural Language Interface:** Users don’t need to know SQL to ask complex data questions.
* **Semantic Search Enhanced Accuracy:** Retrieval-augmented generation boosts reliability.
* **Few-shot Learning:** LLM is primed with contextually relevant examples for better output.
* **Modular Design:** Easily replace or extend individual components (e.g., swap LLM, DB engine).

---


## Installation

1.Clone this repository to your local machine using:

```bash
  git clone https://github.com/KuldipVaghasiya19/SQLify
```
2.Navigate to the project directory:

```bash
  cd SQLify
```
3. Install the required dependencies using pip:

```bash
  pip install -r requirements.txt
```
4.Acquire an api key through makersuite.google.com and put it in .env file

```bash
  GOOGLE_API_KEY="your_api_key_here"
```
5. For database setup, run database/DataBase_Creation.sql in your PostgreSQL workbench

## Usage

1. Run the Streamlit app by executing:
```bash
streamlit run SQLify_Frontend.py


```

2.The web app will open in your browser where you can ask questions

## Sample Questions
  - How many total t shirts are left in total in stock?
  - How many t-shirts do we have left for Nike in XS size and white color?
  - How much is the total price of the inventory for all S-size t-shirts?
  - How much sales amount will be generated if we sell all small size adidas shirts today after discounts?
    
 ## Project Structure
  - SQLify_Frontend.py: Frontend logic for the Streamlit app.
  - SQLify_Backend.py: Backend logic for processing natural language queries into SQL.
  - SQLify_try.py: Experimental file for testing functionalities.
  - requirements.txt: A list of required Python packages for the project.
  - .env: Configuration file for storing your Google API key.
  - db_specifications.py: Details about used Database.
  - DataBase_Creation.sql: code for database creation.
  - FewShots.py: Contains code for Few-Shot learning. 
 

    ![SQLify in Action](https://media.wired.com/photos/641337bd5e3ab3be4fe3e789/master/w_1600%2Cc_limit/sql_normal.gif)
