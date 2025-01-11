# Rag_project_2.ipynb
## 📚 Rag Project 2 - Your Guide to PDF Analysis

Welcome to Rag Project 2! This project is designed to process and analyze PDF documents using powerful tools from langchain. Follow this step-by-step guide to get started. 🌟

## ✨ Features

 Effortless PDF processing and analysis.

 Seamless integration with langchain and related libraries.

 Optimized for collaboration on Google Colab.

## 📋 Requirements

A Google account to use Google Colab.

Basic knowledge of Python.

A PDF file you want to analyze.

## 🚀 Let's Get Started

# 1️⃣ Open the Notebook in Google Colab

Click the badge below to open the notebook in Google Colab:

# 2️⃣ Install the Required Libraries 📦

Run the following commands to install all necessary libraries:

!pip install langchain_community pypdf -q langchain_google_genai langchain_chroma
!pip install --upgrade -q google-auth google-auth-oauthlib google-auth-httplib2 google-cloud

# 💡 Tip: These libraries enable PDF processing and cloud integrations.

# 3️⃣ Upload Your PDF File 📄

Download the sample PDF file from this link.

Upload it to your Colab session.

# 4️⃣ Load the PDF Using LangChain 🤖

Use the following code to load the PDF:

from langchain_community.document_loaders import PyPDFLoader

loader = PyPDFLoader("/content/YOUR_PDF_FILE_NAME.pdf")
data = loader.load()

Replace YOUR_PDF_FILE_NAME.pdf with the name of your uploaded file.

# 5️⃣ Analyze the Document 📊

Once the PDF is loaded, you can process it using langchain tools. Customize this step as per your requirements!

# 🎯 Pro Tips

Ensure your PDF is correctly uploaded to the Colab environment.

Verify package installations before proceeding to the next steps.

# 🤝 Contributions

Feel free to contribute by creating pull requests or reporting issues. Let’s make this project even better together! 💪

# 📞 Support

For any queries, reach out via the GitHub issues section. Happy coding! 😊

## 📚 Rag Project 3 

# 🌐 Dynamic Web Scraper: Your Ultimate Data Extraction Tool 🚀

## Overview

This project demonstrates various applications of Google's Generative AI embedding models, LangChain, and Chroma for text and image embedding, vector storage, and similarity search. It also integrates image embedding through FaceNet for facial recognition tasks. Below are the detailed steps and functionalities implemented in this project.

---

## Prerequisites

Before running the code, ensure you have the following:

- Python 3.8+
- Necessary libraries (installable via pip commands in the script).
- Google API Key configured for Generative AI access.
- Basic knowledge of embeddings, vector similarity search, and RAG (Retrieval-Augmented Generation).

---

## Setup

1. Clone this repository and navigate to the project directory.
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   ```
2. Install the required libraries:
   ```bash
   pip install -q -U google-generativeai langchain-chroma langchain-google-genai facenet-pytorch pillow
   ```
3. Configure your Google API key for Generative AI embedding models.
   ```python
   import google.generativeai as genai
   genai.configure(api_key="<YOUR_GOOGLE_API_KEY>")
   ```

---

## Features and Steps

### 1. **Text Embedding and Vectorization**

- Use Google's `text-embedding-004` model to embed both single strings and lists of strings.
- Generate embeddings for semantic search and similarity tasks.

**Code Overview:**

- Single string embedding:
  ```python
  result = genai.embed_content(model="models/text-embedding-004", content="Pakistan zinda bad we love our country", task_type="retrieval_document", title="Embedding of single string")
  ```
- List of strings embedding:
  ```python
  result = genai.embed_content(model="models/text-embedding-004", content=["What is the meaning of life?", "How does the brain work?"], task_type="retrieval_document", title="Embedding of list of strings")
  ```

### 2. **Building Vector Stores with LangChain and Chroma**

- Store embeddings in a vector database using Chroma for efficient similarity search.
- Perform similarity searches based on vector distances.

**Code Overview:**

- Create a document store:
  ```python
  from langchain_chroma import Chroma
  vectorstore = Chroma.from_documents(documents, embedding=embeddings)
  ```
- Search for similar content:
  ```python
  vectorstore.similarity_search("cat")
  ```

### 3. **Retrieval-Augmented Generation (RAG)**

- Integrate a retriever to fetch relevant documents and feed them into a Large Language Model (LLM) for enhanced responses.

**Code Overview:**

- Define a retriever:
  ```python
  retriever = RunnableLambda(vectorstore.similarity_search).bind(k=1)
  ```
- Chain retriever, prompt, and LLM for RAG:
  ```python
  rag_chain = {"context": retriever, "question": RunnablePassthrough()} | prompt | llm
  response = rag_chain.invoke("Tell about sharks?")
  print(response.content)
  ```

### 4. **Image Embedding with FaceNet**

- Utilize FaceNet for facial recognition by embedding images into vector form.

**Code Overview:**

- Preprocess images:
  ```python
  def preprocess_image(image_path):
      preprocess = transforms.Compose([...])
      return preprocess(image).unsqueeze(0)
  ```
- Generate image embeddings:
  ```python
  def create_image_embedding(image_path):
      input_tensor = preprocess_image(image_path)
      embeddings = model(input_tensor)
      return embeddings.squeeze().numpy()
  ```

### 5. **Image Download Utility**

- Functionality to download images from URLs and save them locally.

**Code Overview:**

```python
def save_image_from_url(image_url, image_name):
    response = requests.get(image_url, stream=True)
    with open(f"images/{image_name}", 'wb') as file:
        file.write(response.content)
```

---

## Use Cases

1. Semantic Search: Find relevant documents or responses using text embeddings.
2. Facial Recognition: Embed and compare facial features using FaceNet.
3. Retrieval-Augmented Generation: Enhance LLM responses with context-driven data.
4. Vector Similarity Search: Identify similar items or concepts based on embeddings.

---

## Folder Structure

```
project/
├── images/                 # Directory for downloaded images
├── main_script.py          # Main implementation script
├── requirements.txt        # Required libraries
└── README.md               # Documentation
```

---

## Contribution

Feel free to open issues or create pull requests for new features or improvements.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.

