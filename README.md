# README

## Project Overview

This project automates the processing of research papers (in PDF format) and generates comprehensive insights from both text and graphical content (such as figures and charts) using Generative AI models. The workflow includes text extraction from PDFs, conversion of PDF pages into images, and analysis of the graphical content alongside the text. Ultimately, the results are stored in a CSV file, and the relevant documents are indexed for retrieval based on various query types.

## Key Features

- **PDF Text Extraction**: Extracts the textual content from research papers in PDF format.
- **Image Extraction from PDFs**: Converts specific pages of PDFs into images, focusing on pages with graphical content such as graphs, charts, and figures.
- **Generative AI for Graph Interpretation**: Analyzes the graphical content with the use of a Generative AI model, offering insights into the data represented in the graphics.
- **Document Analysis and Storage**: The textual and graphical content analysis is combined into a structured format (CSV) and stored for future querying.
- **Vector Database Integration**: The text and image descriptions are indexed in a vector store for efficient similarity search.
- **Query Handling**: The project supports generating multiple perspectives of user queries to retrieve relevant documents from a vector database, providing enhanced results for research.

## Dependencies

- `os` - For interacting with the operating system and file paths.
- `fitz` - For working with PDF documents (extraction and conversion to images).
- `time` - For adding delays between tasks.
- `pandas` - For data manipulation and storage in DataFrame format.
- `langchain` - For creating and managing prompt templates, agents, and tools for AI-based workflows.
- `google.generativeai` - For interacting with Google's Generative AI API (for both text and embeddings).
- `langchain_community` - For community-contributed components such as document loaders and vector stores.
- `langchain_google_genai` - For using Google’s Generative AI models.
- `json` - For working with JSON data.

Ensure that you have the following environment variables set before running the script:

- `GOOGLE_API_KEY` - Your Google API key for accessing the Generative AI models.

## Setup Instructions

1. **Install Dependencies**: 

    Install the required Python libraries by running:
    
    ```bash
    pip install pandas fitz langchain google-generativeai langchain_community langchain_google_genai
    ```

2. **Set Google API Key**: 

    Ensure that the Google API key is set as an environment variable:
    
    ```bash
    export GOOGLE_API_KEY="your_google_api_key_here"
    ```

3. **Prepare the Folder for PDFs**: 

    Place your PDF files in a folder (e.g., `C:/Desktop/hello/`) and set the path accordingly in the script.

4. **Run the Script**: 

    Execute the Python script to process the PDFs. The script will extract text and images, analyze the graphical content, and generate insights which are saved into a CSV file.

## Workflow

1. **Extract Text from PDF**: 
    - The `extract_text_pdf` function extracts all the text content from the given PDF file.

2. **Convert PDF Pages to Images**: 
    - The `save_pdf_as_images` function converts selected pages of the PDF to image format, excluding the first and last third of the document.

3. **Process Each PDF**:
    - For each PDF, text is extracted, and relevant images are generated and uploaded to the Generative AI model for analysis.
    
4. **Analysis and Insights Generation**: 
    - The images are processed by the Generative AI to analyze graphs and figures, and textual descriptions of the graphs are created.
    - The textual data and image descriptions are then combined for each document.

5. **Store Results in a CSV File**: 
    - The results are saved in a CSV file that contains the text and image descriptions for each document.

6. **Vector Store Indexing**: 
    - The extracted text and image descriptions are indexed in a vector store (using Chroma), allowing efficient retrieval based on user queries.

7. **Answering Research Questions**: 
    - The system can answer questions by retrieving the most relevant documents and providing insights from the stored context.

## Example Query Handling

Here is an example of how to handle a research question:

```python
question = "Mention the techniques used in the given papers, and their performance analysis of techniques used?"
response = agent_executor_1.invoke({"question": question})
print(response)
