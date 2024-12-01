# Document-Analysis-using-LLM
Document Analysis and generating Question and Answers using LLMs with Python

Here's a `README.md` file for the project based on your provided code:


# PDF Text Extraction, Summarization, Question Generation, and Answering

This project demonstrates how to extract text from a PDF document, summarize it, generate questions, and answer those questions using state-of-the-art models from Hugging Face's `transformers` library. The project uses the following steps:

1. **PDF Text Extraction**: Extracts text from a PDF file using `pdfplumber`.
2. **Text Summarization**: Summarizes the extracted text using the T5 model.
3. **Question Generation**: Generates questions based on the extracted text using a T5 model fine-tuned for question generation.
4. **Question Answering**: Answers the generated questions using a RoBERTa-based question-answering model.

## Requirements

To run this project, you'll need the following Python packages:

- `pdfplumber`
- `transformers`
- `nltk`

You can install them using pip:

```bash
pip install pdfplumber transformers nltk
```

## Usage

### Step 1: Extract Text from PDF

The code extracts text from the provided PDF (`google_terms_of_service_en_in.pdf`) using `pdfplumber` and saves it to a text file (`extracted_text.txt`).

### Step 2: Summarize the Extracted Text

The extracted text is passed to a T5 model to generate a summary of the document. The `summarize()` function uses the model to return a concise version of the text.

### Step 3: Generate Questions

The extracted and summarized text is split into smaller passages. Questions are generated for each passage using a T5-based model fine-tuned for question generation. The generated questions are stored and displayed.

### Step 4: Answer the Generated Questions

The generated questions are answered using a RoBERTa-based question-answering model. The answers are written to a file (`qa_output.txt`).

## File Descriptions

- **google_terms_of_service_en_in.pdf**: The PDF file from which text will be extracted.
- **extracted_text.txt**: The text file where the extracted content from the PDF is saved.
- **qa_output.txt**: A text file where the answers to the generated questions are stored.

## Code Walkthrough

1. **PDF Text Extraction**:
   - The `pdfplumber.open()` function opens the PDF, and `page.extract_text()` is used to extract text from each page.
   
2. **Summarization**:
   - The T5 model is used to summarize the text. The input text is tokenized, and the model generates a summary using beam search.
   
3. **Question Generation**:
   - The text is split into sentences, and each passage is processed to generate questions. If the number of generated questions is less than a specified minimum, additional parts of the passage are used to generate more questions.
   
4. **Question Answering**:
   - For each generated question, the `qa_pipeline` answers it by searching the corresponding passage for the most relevant information.

## Example Output

```text
Text extracted and saved to extracted_text.txt
Summary: The terms of service outline the rules for using Google's services and the responsibilities of users.

Passage 1:
...
Generated Questions:
- What are the rules for using Google's services?
- What responsibilities do users have?
- What actions are prohibited under the terms?

==================================================
```

## Notes

- **Sentence Segmentation**: The text is split into sentences using the `nltk.sent_tokenize` method, ensuring that questions are generated based on meaningful parts of the document.
- **Model Fine-Tuning**: The T5 model for question generation is fine-tuned for this specific task, ensuring high-quality question generation.
- **Answer Uniqueness**: The `answer_unique_questions()` function ensures that only unique questions are answered, avoiding duplicates.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more information.


