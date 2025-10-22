# Art of Drawers - Onboarding PDF Generator

A **completely free** Streamlit application that generates personalized onboarding PDFs for Designers and Installers at Art of Drawers.

## Features

- 🎨 Clean, intuitive web interface
- 👤 Role-based templates (Designer/Installer)
- 📧 Automatic email and Canvas username generation
- 📄 Dynamic PDF generation with personalized content
- 💯 **100% Free** - uses LibreOffice for PDF conversion (no paid APIs!)
- 🔒 No external dependencies or API keys needed

## Prerequisites

- Python 3.8+
- LibreOffice (for local testing - automatically available on Streamlit Cloud)
- GitHub account (for deployment)
- Streamlit Community Cloud account (for hosting)

## Project Structure
```
aod-onboarding-pdf/
├── streamlit_app.py              # Main Streamlit application
├── embed_templates.py            # Script to embed templates as base64
├── templates/                    # Template files (not deployed)
│   ├── Designer_Onboarding_Template.docx
│   └── Installer_Onboarding_Template.docx
├── templates_base64.py           # Generated embedded templates
├── requirements.txt              # Python dependencies
├── packages.txt                  # System dependencies (LibreOffice)
└── README.md                     # This file
```

## Setup Instructions

### 1. Clone or Create Repository
```bash
mkdir aod-onboarding-pdf
cd aod-onboarding-pdf
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

**For local testing**, also install LibreOffice:
- **Ubuntu/Debian:** `sudo apt-get install libreoffice`
- **macOS:** `brew install libreoffice`
- **Windows:** Download from [libreoffice.org](https://www.libreoffice.org/download/download/)

### 3. Add Template Files

Place your two `.docx` template files in the `templates/` directory:
- `Designer_Onboarding_Template.docx`
- `Installer_Onboarding_Template.docx`

Ensure each template contains these placeholders:
- `{{GREETING}}` - Will be replaced with "FirstName,"
- `{{GMAIL}}` - Will be replaced with email address
- `{{CANVAS_USERNAME}}` - Will be replaced with Canvas username

### 4. Embed Templates

Run the embedding script to convert templates to base64:
```bash
python embed_templates.py
```

This creates `templates_base64.py` which embeds the templates directly in the code.

### 5. Local Testing

Run the app:
```bash
streamlit run streamlit_app.py
```

This will open the app in your browser. Test it with sample data.

## Deployment to Streamlit Community Cloud

### 1. Push to GitHub
```bash
git init
git add .
git commit -m "Initial commit: AOD Onboarding PDF Generator"
git branch -M main
git remote add origin https://github.com/mfluker/aod-onboarding-pdf.git
git push -u origin main
```

### 2. Deploy on Streamlit Cloud

1. Go to [share.streamlit.io](https://share.streamlit.io)
2. Click "New app"
3. Select:
   - **Repository:** `mfluker/aod-onboarding-pdf`
   - **Branch:** `main`
   - **Main file path:** `streamlit_app.py`
4. Click "Deploy"

**That's it!** No API keys or secrets needed. The `packages.txt` file automatically installs LibreOffice on Streamlit Cloud.

## Updating Templates

When you need to update the onboarding templates:

1. Update the `.docx` files in the `templates/` directory
2. Run the embedding script:
```bash
   python embed_templates.py
```
3. Commit and push the updated `templates_base64.py`:
```bash
   git add templates_base64.py
   git commit -m "Update onboarding templates"
   git push
```
4. Streamlit Cloud will automatically redeploy with the new templates

## How It Works

### Name Normalization

- **Greeting:** First name in Title Case (e.g., "Mary-Jane")
- **Email:** `first_initial + lastname@artofdrawers.com` (lowercase, alphanumeric only)
- **Canvas Username:** `firstname.lastname` (lowercase, alphanumeric only)

### Placeholder Replacement

The app replaces only these three placeholders in the templates:
- `{{GREETING}}`
- `{{GMAIL}}`
- `{{CANVAS_USERNAME}}`

All other content remains unchanged.

### PDF Generation Flow

1. User submits form with role and name
2. App loads appropriate template from embedded base64 data
3. Placeholders are replaced with personalized values
4. DOCX is generated in memory
5. **LibreOffice** converts DOCX to PDF (free!)
6. PDF is offered as download with filename: `{role}-{first}_{last}-onboarding.pdf`

## Troubleshooting

### Templates not found
- Ensure `.docx` files are in the `templates/` folder
- Run `embed_templates.py` to generate `templates_base64.py`

### LibreOffice not found (local testing)
- Install LibreOffice for your OS (see Setup Instructions)
- Make sure `libreoffice` is in your PATH

### Placeholder not replaced
- Verify placeholders are exactly `{{GREETING}}`, `{{GMAIL}}`, `{{CANVAS_USERNAME}}`
- Check that placeholders aren't split across multiple runs in Word
- Try selecting the placeholder text and retyping it

## Why This Solution is Free

- **No paid APIs** - uses LibreOffice (open source)
- **No conversion limits** - unlimited PDFs
- **No API keys** - no account setup needed
- **Works on Streamlit Cloud** - LibreOffice installed via `packages.txt`

## Support

For issues or questions, contact the development team or create an issue in the GitHub repository.

## License

Internal use only - Art of Drawers