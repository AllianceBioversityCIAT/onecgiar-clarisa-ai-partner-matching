
# Project Structure - CLARISA AI Partners

## Folder Organization

```
clarisa_ai_partners/
├── backend/                          # Backend API (Python/FastAPI)
│   ├── src/
│   │   ├── main.py                   # Application entry point
│   │   ├── config.py                 # Configuration
│   │   ├── api/                      # Routes and endpoints
│   │   ├── services/                 # Business logic services
│   │   ├── embeddings/               # Embeddings service with AWS Bedrock
│   │   ├── duplicate_detection/      # Duplicate detection logic
│   │   ├── persistence/              # Database access (Supabase)
│   │   └── audit/                    # Logging and auditing
│   ├── requirements.txt              # Python dependencies
│   ├── .env                          # Environment variables
│   ├── test_*.py                     # Test scripts
│   └── *.xlsx                        # Test files
│
├── frontend/                         # Frontend Angular/TypeScript
│   ├── src/
│   ├── package.json
│   └── ...
│
├── run_backend.py                    # Script to run the backend
├── .env                              # Environment variables (root)
├── .env.example                      # Example environment variables
└── ...
```

## How to Run the Backend

### Option 1: From the project root (Recommended)

```bash
python run_backend.py
```

This script:
- Changes to the `backend/` directory
- Sets up the Python path
- Starts Uvicorn at http://0.0.0.0:8000

### Option 2: From the backend directory

```bash
cd backend
python -m uvicorn src.main:app --reload
```

### Option 3: From anywhere using the full path

```bash
python -m uvicorn backend.src.main:app --reload --cwd backend
```

## Installing Dependencies

```bash
cd backend
pip install -r requirements.txt
```

Or if you use conda:

```bash
cd backend
conda create -n clarisa python=3.9
conda activate clarisa
pip install -r requirements.txt
```

## Environment Variables

Environment variables should be set in `backend/.env`:

```env
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_key
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your_aws_key
AWS_SECRET_ACCESS_KEY=your_aws_secret
CLARISA_API_URL=https://api.clarisa.cgiar.org/api/institutions
USE_MOCK_EMBEDDINGS=false
USE_MOCK_SUPABASE=false
```

## API Endpoints

### Upload Duplicates
- **POST** `/institutions/duplicates/upload` - Upload Excel file to detect duplicates

### Analysis History
- **GET** `/institutions/analysis` - List all performed analyses
- **GET** `/institutions/analysis/{file_id}` - Get details of a specific analysis

## Backend Structure

### `src/api/` - Routes
- `institutions.py` - Endpoints for institution and duplicate management

### `src/services/` - Business logic
- `excel_parser.py` - Excel file parser
- `normalization.py` - Data normalization
- `clarisa_sync_service.py` - Sync with CLARISA API
- `embedding_service.py` - Embeddings management

### `src/embeddings/` - Embeddings
- `bedrock_service.py` - AWS Bedrock service to generate embeddings

### `src/duplicate_detection/` - Detection
- `detector.py` - Duplicate detection logic based on 7 rules

### `src/persistence/` - Database
- `supabase_client.py` - Supabase client for CRUD operations

### `src/audit/` - Auditing
- `logger.py` - Audit and operations logging

## Testing

Run tests:

```bash
cd backend
python test_api.py
python test_embedding_format.py
```

## Development Notes

- The backend uses **FastAPI** for the REST server
- Database: **Supabase** (PostgreSQL)
- Embeddings: **AWS Bedrock Titan v2** (1024 dimensions)
- Duplicate detection based on:
  1. Exact name match
  2. Semantic similarity > 0.75
  3. Rule-based signals

## Important URLs

- Backend: http://localhost:8000
- API Docs: http://localhost:8000/docs
- Supabase: https://app.supabase.com
