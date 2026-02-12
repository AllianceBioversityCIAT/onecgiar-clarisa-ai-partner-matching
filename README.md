# CLARISA AI Partner Detector

Intelligent duplicate detection system enabling CGIAR institutions to identify and manage duplicate partners in the CLARISA database using AI-powered semantic similarity analysis.

## 📋 Overview

CLARISA AI Partner Detector is a modern web application combining a Python (FastAPI) backend with an Angular 17+ frontend. The system allows you to:

- **Upload institution data** from Excel files
- **Automatically detect duplicates** using semantic embeddings (AWS Bedrock)
- **Visualize results** in interactive dashboards
- **Synchronize** with the CLARISA database
- **Monitor** system health and sync status

## 🏗️ Project Structure

```
clarisa_ai_partners/
├── backend/                    # FastAPI API
│   ├── src/
│   │   ├── api/               # REST endpoints
│   │   ├── services/          # Business logic
│   │   ├── persistence/       # Supabase integration
│   │   ├── embeddings/        # AWS Bedrock
│   │   ├── duplicate_detection/
│   │   └── audit/             # Logging
│   ├── scripts/               # Utility scripts
│   └── requirements.txt
│
├── frontend/                   # Angular app
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/    # Reusable components
│   │   │   ├── pages/         # Main pages
│   │   │   ├── services/      # API services
│   │   │   └── interceptors/  # HTTP interceptors
│   │   └── assets/
│   └── package.json
│
└── README.md
```

## 🚀 Quick Start

### Prerequisites

- **Python 3.10+**
- **Node.js 18+**
- **npm** or **yarn**
- **Supabase** credentials
- **AWS Bedrock** credentials

### Backend Installation

```bash
cd backend

# Create virtual environment
python -m venv venv

# Activate environment
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
cp .env.example .env
# Edit .env with your credentials
```

### Frontend Installation

```bash
cd frontend

# Install dependencies
npm install

# Configure backend proxy (optional)
# proxy.conf.json is already set for http://localhost:8000
```

### Run the Application

**Terminal 1 - Backend:**
```bash
cd backend
python run.py
# API available at http://localhost:8000
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm start
# App available at http://localhost:4200
```

## 📚 Main Features

### 1. **Data Upload (Excel Upload)**
- Drag & drop .xlsx / .xls files
- Required columns validation
- 10MB file size limit
- Real-time progress visualization

### 2. **Duplicate Detection**
- Semantic analysis with AI embeddings
- 3 match levels:
  - **Duplicate** (≥85% similarity)
  - **Potential duplicate** (≥75% similarity)
  - **No match** (<75% similarity)
- Automatic explanation of the reason

### 3. **Interactive Results**
- Table with filtering and search
- Export to CSV/Excel
- Expandable institution details
- Similarity score visualization

### 4. **Monitoring Dashboard**
- System statistics
- Sync history
- Embeddings generated counter
- Distribution charts

### 5. **Admin Panel**
- Manual CLARISA sync
- Generate missing embeddings
- View system configuration
- Operation logs

## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/institutions/duplicates/upload` | Upload Excel and detect duplicates |
| GET | `/institutions/sync-status` | Get sync status |
| POST | `/institutions/sync-clarisa` | Sync with CLARISA |
| GET | `/institutions/health` | System health status |
| GET | `/institutions/config` | Current configuration |
| POST | `/institutions/generate-embeddings` | Generate missing embeddings |
| GET | `/institutions/test-clarisa-api` | Test CLARISA connection |

## 🎨 Themes and Styles

**Primary Color:** `#7ab800` (CGIAR Green)

Frontend uses:
- **SCSS** with theme variables
- **Responsive Design** (mobile-first)
- **Material Design components**
- **WCAG 2.1 AA accessibility**

## 🔧 Environment Variables

### Backend (.env)

```
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_key
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your_aws_key
AWS_SECRET_ACCESS_KEY=your_aws_secret
CLARISA_API_URL=https://clarisa.cgiar.org/api
```

### Frontend (environment.ts)

```typescript
export const environment = {
  production: false,
  apiUrl: 'http://localhost:8000',
  apiVersion: 'v1',
  primaryColor: '#7ab800',
  maxFileSize: 10 * 1024 * 1024,
  allowedFileTypes: ['.xlsx', '.xls']
};
```

## 📦 Technologies Used

### Backend
- **FastAPI** - Modern web framework
- **Python 3.10+** - Language
- **Supabase** - PostgreSQL database
- **AWS Bedrock** - Semantic embeddings
- **Pandas** - Data processing
- **OpenPyXL** - Excel reading

### Frontend
- **Angular 17+** - Web framework
- **TypeScript 5.0+** - Typed language
- **RxJS** - Reactive programming
- **SCSS** - Advanced styles
- **Chart.js** - Interactive charts

## 📖 Additional Documentation

- [Setup Guide Backend](./backend/SETUP_GUIDE.md)
- [README Frontend](./frontend/README.md)
- [Style Guide](./frontend/STYLE_SYSTEM_GUIDE.md)
- [Responsive Guide](./frontend/RESPONSIVE_DESIGN_GUIDE.md)

## 🧪 Testing

### Backend
```bash
cd backend
pytest
```

### Frontend
```bash
cd frontend
npm test              # Unit tests
npm run e2e           # End-to-end tests
```

## 🚢 Deployment

### Docker

```bash
# Build image
docker build -t clarisa-detector .

# Run container
docker run -p 80:80 clarisa-detector
```

### Production Build

**Frontend:**
```bash
npm run build -- --configuration=production
```

**Backend:**
```bash
python run.py  # For production use gunicorn/uvicorn
```

## 📋 Color Configuration

| Use | Color | Hex |
|-----|-------|-----|
| Primary | CGIAR Green | #7ab800 |
| Dark Primary | Dark Green | #5a8c00 |
| Light Primary | Light Green | #9ad633 |
| Secondary | Dark Blue | #2c3e50 |
| Accent | Sky Blue | #3498db |
| Success | Green | #27ae60 |
| Warning | Orange | #f39c12 |
| Danger | Red | #e74c3c |

## 🤝 Contributions

Contributions are welcome. Please:

1. Create a branch for your feature (`git checkout -b feature/AmazingFeature`)
2. Commit your changes (`git commit -m 'Add AmazingFeature'`)
3. Push to the branch (`git push origin feature/AmazingFeature`)
4. Open a Pull Request

## 📝 License

This project is under the CGIAR license.

## 👤 Author

**SantiagoSC1999**
- Email: sasa.sanchezcorre-7@hotmail.com
- GitHub: [@SantiagoSC1999](https://github.com/SantiagoSC1999)

## 📞 Support

To report bugs or request features, open an issue in the repository.

---

**Last update:** January 2026
