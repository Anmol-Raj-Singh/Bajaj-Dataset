# Bajaj-Dataset
A scalable and accurate FastAPI service that processes lab report images to extract structured medical test data. The solution uses traditional OCR and parsing techniques (no LLMs) to identify test names, values, reference ranges, and units, while automatically calculating if values fall outside normal ranges.
# Lab Report Processor

A FastAPI service that processes lab report images and extracts lab test information, including test names, values, reference ranges, and whether the values are out of range.

## Features

- Extracts lab test names, values, reference ranges, and units from images
- Calculates if test values are out of range
- Provides a RESTful API endpoint for processing images
- Supports batch processing of multiple images
- No LLM integration, uses traditional OCR and parsing techniques

## Prerequisites

- Python 3.8 or higher
- Tesseract OCR installed on your system
- Rust (for building pydantic-core)

### Installing Tesseract OCR

#### macOS
```bash
brew install tesseract
```

#### Ubuntu/Debian
```bash
sudo apt-get install tesseract-ocr
```

#### Windows
Download and install from: https://github.com/UB-Mannheim/tesseract/wiki

### Installing Rust (Required for pydantic-core)
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

## Installation

1. Clone this repository
```bash
git clone https://github.com/yourusername/lab-report-processor.git
cd lab-report-processor
```

2. Create and activate a virtual environment (recommended)
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install the required Python packages
```bash
pip install -r requirements.txt
```

## Usage

### Starting the API Server

```bash
python main.py
```

The server will start at `http://localhost:8000`

### API Endpoints

#### POST /get-lab-tests
Process a single lab report image and return extracted test data.

**Request:**
- Content-Type: multipart/form-data
- Body: `file` - Image file (PNG, JPG, JPEG)

**Response:**
```json
{
    "is_success": true,
    "data": [
        {
            "test_name": "HB ESTIMATION",
            "test_value": "9.4",
            "bio_reference_range": "12.0-15.0",
            "test_unit": "g/dL",
            "lab_test_out_of_range": true
        }
    ]
}
```

### Batch Processing

To process multiple images at once, use the provided batch processing script:

```bash
python batch_process.py
```

This will process all images in the dataset folder and save results to `lab_results.jsonl`.

## Project Structure

```
lab-report-processor/
├── main.py              # FastAPI application
├── batch_process.py     # Batch processing script
├── requirements.txt     # Python dependencies
├── README.md           # Project documentation
└── .gitignore          # Git ignore rules
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.
