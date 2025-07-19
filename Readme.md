# Physics Department Website

## Folder Structure

PhysicsWebsite/

│

├── app.py # Main Flask backend

├── requirements.txt # Python dependencies

├── credentials/ # Google Service Account JSON

│ └── credentials.json

├── data/ # JSON & CSV sample data

│ ├── faculty.json

│ ├── research.json

│ ├── labs.json

│ ├── contact_submissions.csv (given just for storing in local database)

│ ├── achievemnets.json

│ ├── publications.json

│ ├── announcements.json

├── static/ # CSS, JS, Images

│ ├── css/

│ ├── js/

│ ├── images/

├── templates/ # HTML templates

│ ├── index.html

│ ├── faculty.html

│ ├── research.html

│ ├── publications.html

│ ├── contact.html

│ └── about.html

│ └── achievements.html

│ └── curriculum.html

│ └── labs.html

└── README.md

---

## Setup & Run Instructions

## 1️⃣ Clone the Repository

```
git clone https://github.com/Doofenshmirtz16/Physics-Association-Website.git
cd Physics-Association-Website
```

## 2️⃣ Install Dependencies

```
pip install -r requirements.txt
```
OR (generate yourself):
```
pip freeze > requirements.txt
```
Example requirements.txt:
```
Flask==2.3.2
gspread==6.0.2
google-auth==2.22.0
google-auth-oauthlib==1.0.0
google-auth-httplib2==0.1.0
```
## 3️⃣ Setup Google Sheets API (for Contact Form)
Create a Google Cloud project

Enable Google Sheets API

Create a Service Account → generate credentials.json

Place credentials.json in credentials/ folder

Share your Google Sheet with the service account email (Editor access)

Set the Spreadsheet ID in app.py:
```
SPREADSHEET_ID = 'your-google-spreadsheet-id'
```


#### Note: This part of setting up a google sheet is a little bit extensive. To simply just test it out locally on computer, you can just remove the following line of codes from the current app.py in repo while ensuring that you do have contact_submissions.csv under data folder. (We will basically remove the part of setting up Google Sheets and leave the local csv file to store data.)
```
import gspread
from google.oauth2.service_account import Credentials
```
```
if os.environ.get('GOOGLE_CREDS_JSON'):
    with open('temp_google_creds.json', 'w') as f:
        f.write(os.environ['GOOGLE_CREDS_JSON'])
    os.environ['GOOGLE_APPLICATION_CREDENTIALS'] = 'temp_google_creds.json'

# Setup Google Sheets API
SCOPES = ["https://www.googleapis.com/auth/spreadsheets"]
SERVICE_ACCOUNT_FILE = os.environ.get("GOOGLE_APPLICATION_CREDENTIALS", "credentials/credentials.json")

credentials = Credentials.from_service_account_file(
    SERVICE_ACCOUNT_FILE, scopes=SCOPES)
gc = gspread.authorize(credentials)

# Open the sheet by ID
SPREADSHEET_ID = '1wavyKlHG4So13TdMUJyrdeQAZacylXZgHJHassvqiww'
spreadsheet = gc.open_by_key(SPREADSHEET_ID)
sheet = spreadsheet.sheet1
```
Finally, in the section of contact form routes, you will remove:
```
# Append row to Google Sheet
sheet.append_row([name, email, subject, message])
```


## 4️⃣ Run the Application Locally
```
python app.py
```
Open your browser at:
```
[http://127.0.0.1:5000/] (http://localhost:5000 )
```

#### Note: In the file app.py, there's a code to create a credentials file just above the part of setting up Google Sheets API. This part of code is just used for hosting on Render so that credentials are not pushed on github but rather just locally included while hosting the website.


## Credits

Developed as part of Physics Association Web Development Team

Physics Department Website

Technologies used: Flask, HTML, CSS, JS, Google Sheets API

