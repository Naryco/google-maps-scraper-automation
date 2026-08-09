# 🗺️ Google Maps Business Data Scraper Automation (n8n + AI)

This project is a modular n8n automation that analyzes natural language commands, scrapes business data (address, phone, ratings, websites, etc.) from Google Maps, and saves it to Google Sheets using **2 separate workflows**.

## 🧠 System Architecture

The system is designed with a "Modular" approach using two distinct workflows:

### 🔵 **Workflow 1: Main System (AI Agent & Search Engine)**
Handles user interaction and performs the Google Maps search.
1. **Chat Trigger:** The user sends a command like "Get kebab shops in Denizli".
2. **AI Agent & OpenAI Model:** Analyzes the command and extracts the city and category.
3. **Map Search Tool:** Uses the `google.serper.dev` API to search Google Maps.
4. **Sub-Workflow Call:** Triggers Workflow 2 for each business found to send the data.

### 🔴 **Workflow 2: Writer Service (Data Processing & Storage)**
Triggered by Workflow 1, it cleans, enriches, and writes the data to Google Sheets.
1. **Sub-Workflow Trigger:** Starts when data is received from Workflow 1.
2. **Code in JavaScript:** Parses raw data, normalizes UUIDs, and formats fields.
3. **HTTP Request (Perplexity API):** Enriches data by fetching missing email addresses and background info.
4. **Append row in sheet:** Writes all clean data (Name, Address, Number, Website, Rating, Opening Hours, Email) to Google Sheets.

## 🛠️ Tech Stack
- n8n, OpenAI Chat Model, Serper.dev (Google Maps), Perplexity API, Google Sheets API

## ⚙️ Setup
1. Import both `.json` files into n8n separately.
2. Update all Credentials with your own API keys (OpenAI, Serper, Perplexity, Google Sheets).
3. **Publish** and activate Workflow 2.
4. In Workflow 1, update the `Call 'Google Maps Otomasyonu Otomatik Yazdırma'` node to point to the correct Workflow 2 ID.

## 🔒 Security
No real API keys or Sheet IDs are included. All fields are replaced with `YOUR_...` placeholders.

## 📷 Previews
**Workflow 1 (Main AI & Search System):**
![Workflow 1](images/workflow1.png)

**Workflow 2 (Data Processing & Writer Service):**
![Workflow 2](images/workflow2.png)

## 🎬 Credits & Acknowledgments

The foundational logic and AI Agent structure of this workflow were learned following the comprehensive training **"n8n ile Yapay Zeka Ajanları Kur ve Sat (5 Saatlik Eğitim – Sıfır Kodlama)"** (Build and Sell AI Agents with n8n - 5 Hour Training) by **[Burhan Kocabıyık](https://www.youtube.com/@burhan.kocabiyik)**.

While the core principles from the course were applied, further customization was done based on personal needs and logic. A big thank you for the valuable training content!