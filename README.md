
# HybridPDFLoader

🚀 A **custom LangChain Document Loader** that extracts **text, tables, and images** from complex PDFs — all in one place.  
It combines the strengths of multiple libraries and adds **multimodal LLM image captioning** for smarter retrieval.

---

## 📌 Problem Statement

LangChain provides a few PDF loaders (`UnstructuredPDFLoader`, `PDFMinerLoader`, `PDFPlumberLoader`), but none can reliably extract **text + tables + images** together.  

- `unstructured` often introduces dependency conflicts  
- `pdfminer` works well for **text** but not tables  
- `pdfplumber` works well for **tables** but not images  
- `fitz` (PyMuPDF) works well for **images** but not structured text  

👉 So I combined them into a single **HybridPDFLoader**.

---

## ⚙️ Features

- **Text** → `pdfminer.six`  
- **Tables** → `pdfplumber`  
- **Images** → `fitz` (PyMuPDF)  
- **Image Descriptions** → Azure OpenAI GPT-4o (multimodal)  
- Rich **metadata** for every element: bounding boxes, fonts, coordinates, file paths  
- Fully compatible with **LangChain’s `Document` schema**  
- Saves extracted images locally for reference  

---

## 📂 Project Structure

```

HybridPDFLoader/
│
├── .venv/                # Python virtual environment
├── PDF/                  # Place your input PDF files here
├── .env                  # Environment variables (Azure OpenAI keys, etc.)
├── .python-version       # Python version pin
├── main.ipynb            # Jupyter Notebook with HybridPDFLoader implementation
├── pyproject.toml        # Project dependencies (uv / poetry style)
├── uv.lock               # Dependency lock file
└── README.md             # Project documentation (this file)

````

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/your-username/HybridPDFLoader.git
cd HybridPDFLoader
````

### 2. Set up environment

Create a virtual environment (if not already created):

```bash
python -m venv .venv
source .venv/bin/activate   # Linux/Mac
.venv\Scripts\activate      # Windows
```

Install dependencies with [uv](https://github.com/astral-sh/uv) (or pip):

```bash
uv sync
```

### 3. Configure Azure OpenAI

Create a `.env` file in the project root:

```env
AZURE_OPENAI_DEPLOYMENT_NAME=your-deployment
AZURE_OPENAI_API_KEY=your-key
AZURE_OPENAI_API_VERSION=2024-02-01
AZURE_OPENAI_ENDPOINT=https://your-endpoint.openai.azure.com/
```

### 4. Run the loader

Open the notebook:

```bash
jupyter notebook main.ipynb
```

Inside, you can load a PDF:

```python
from main import HybridPDFLoader

loader = HybridPDFLoader("PDF/Test.pdf")
docs = loader.load()

print(docs[0].page_content)
print(docs[0].metadata)
```

---

## 🔮 Roadmap / Improvements

* [ ] Add **OCR fallback** (Tesseract / Azure Form Recognizer) for scanned PDFs
* [ ] Smarter **table parsing** (Camelot/Tabula integration)
* [ ] Deduplication of duplicate images
* [ ] Performance improvements for large PDFs
* [ ] Privacy filters before sending content to LLMs

---

## 🤝 Contributing

Pull requests and discussions are welcome!
If you have better approaches for table extraction, OCR, or multimodal description, feel free to open an issue or PR.

---

## 📜 License

MIT License – free to use, modify, and share.

---

## 🙌 Acknowledgements

* [LangChain](https://github.com/langchain-ai/langchain)
* [PyMuPDF](https://pymupdf.readthedocs.io/)
* [pdfplumber](https://github.com/jsvine/pdfplumber)
* [pdfminer.six](https://github.com/pdfminer/pdfminer.six)
* [Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/)



