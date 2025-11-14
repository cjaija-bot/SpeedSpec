
# SpecSheet MVP – Technical Requirements (Markdown Format)

## 1. Overview
SpecSheet is an MVP tool that extracts structured data from long technical PDF specification sheets (SaaS, APIs, chips, security docs) and converts them into a sortable comparison table.

## 2. Core MVP Features
### a) PDF Upload
- Support for uploading 1–3 PDFs
- Accept PDF or image-based specs
- Validate file size < 20MB

### b) OCR + Table Extraction
- Run OCR on scanned PDFs
- Identify specification fields as key–value pairs
- Extract tables using Tabula or PDFPlumber

### c) Feature Normalization
- Map synonyms (e.g., “throughput” = “req/s”)
- Use an editable dictionary (JSON)
- User feedback updates the mapping

### d) Comparison Table UI
- Display extracted fields in a row-per-PDF layout
- Allow sorting, filtering, and searching
- Inline editing of fields

### e) Export / Sharing
- Export as CSV
- One-click “Copy to Clipboard” for slides
- Prepare a basic “Comparison Summary” text block

## 3. Technical Stack
- **Frontend:** Next.js
- **Backend:** Supabase (DB + Auth)
- **Workers:** Cloudflare Worker for OCR tasks
- **Extraction:** LangChain + Tabula/PDFPlumber
- **Storage:** Supabase bucket for PDFs

## 4. Data Model
### Table: documents
- id  
- user_id  
- original_filename  
- processed_at  
- status  

### Table: extracted_fields
- id  
- document_id  
- field_name  
- field_value  
- normalized_name  

### Table: synonym_map
- id  
- canonical_field  
- synonyms (array)

## 5. User Flow
1. User uploads PDF(s)
2. Backend processes OCR + extraction
3. System normalizes field names
4. Data is stored and served via API
5. UI displays the comparison table

## 6. Success Criteria
- Extracts ≥70% of table fields in typical spec sheets
- Zero manual copy/paste needed
- PDF → structured table in < 45 seconds

## 7. Non-Goals (MVP)
- No complex charting
- No multi-user collaboration
- No API integrations
- No enterprise SSO

## 8. Stretch Goals (Post-MVP)
- Export to Keynote/PowerPoint templates
- Automatic competitor mapping
- Compliance red-flag scanning (SOC2, GDPR)
- Full UI customization

## End of Document
