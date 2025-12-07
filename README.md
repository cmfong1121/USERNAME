# MoneyFlow – Personal Finance Tracker with Spending Prediction

#### Video Demo:  <https://youtu.be/YOUR_VIDEO_LINK_HERE>

![/workspaces/215702683/project/static/Dashboard.PNG.](<img width="1336" height="919" alt="Dashboard" src="https://github.com/user-attachments/assets/074c091b-ee55-4d7b-ac18-ccde91cb2f20" />)

#### Description:

Hey! This is the final project I built for CS50x 2025, and honestly, it’s the first piece of software I’ve ever made that I actually use every single day.

MoneyFlow is a complete personal-finance web application that lets you register, log in, add income and expenses, see beautiful interactive charts, get a scarily accurate prediction of how much you’ll spend next month using real machine learning, and export any month as CSV or a clean, printable PDF.

Everything is built with exactly the tools we were taught in CS50x 2025:
- Python + Flask for the backend
- SQLite (via cs50.SQL) for the database
- HTML, Bootstrap 5, Jinja2, custom CSS, and vanilla JavaScript for the front-end
- Chart.js for the graphs
- pandas and scikit-learn for the spending prediction
- WeasyPrint for PDF export

No external APIs, no paid services — it all runs locally.

### What the app actually does

When you first visit the site you’re asked to register or log in. I used Flask-Login and Werkzeug’s password hashing exactly like we learned in the Finance problem set, but I made the forms look way nicer with Bootstrap 5.

Once you’re in, the dashboard is the star of the show:
- Three huge cards at the top show total income, total expenses, and current balance (starting cash is $10,000 like in Finance, but you can change it later if you want).
- A colorful doughnut chart instantly shows this month’s expense breakdown by category.
- A 30-day line chart of daily spending. I spent hours making sure every single day appears, even if you spent $0. The line is smooth and looks professional.

From the navbar you can go to:
- Add Transaction — a fast form with smart category dropdowns that change depending on whether you select “income” or “expense”. There’s also a “Custom category…” option in case your weird expense doesn’t fit my list.
- History — pick any month from a dropdown and see all transactions in a clean table. Two big buttons let you export that month as CSV or PDF with one click.
- Prediction — my absolute favorite page. It grabs the last 12 months of expense totals, feeds them into scikit-learn’s Linear Regression, and tells you “Next month you will probably spend about $X”. I tested it with my real data for the past six months and it was within $50 every single time.

There’s also a dark/light mode toggle in the bottom-right corner because I code at night and my eyes were dying.

### Why I made the choices I made

I could have just reskinned the Finance pset and called it a day, but I wanted something that felt modern and useful. Once I discovered Chart.js in week 9, I went down a rabbit hole and spent two full days making the charts perfect.

The prediction feature started as a simple average of the last three months. Then I remembered CS50 AI introduced scikit-learn, so I thought “why not?” — and six lines of code later the app suddenly felt intelligent. Seeing the prediction slowly climb when I buy too much bubble tea is low-key motivating.

PDF export was the last feature I added. I tried a few libraries and settled on WeasyPrint because it lets me reuse almost the same HTML I already had, so the PDFs look exactly like the web version.

Dark-mode toggle was a small detail that took maybe ten minutes but makes the app feel modern and saves my eyes in the dead of night.

### Complete file list and what each does

File Structure under Project “MoneyFlow”:
project/
├── app.py
├── requirements.txt
├── finance.db
├── README.md
├── static/
│   ├── style.css
│   └── chart-config.js
└── templates/
    ├── layout.html
    ├── index.html
    ├── login.html
    ├── register.html
    ├── add.html
    ├── history.html
    ├── prediction.html
    └── pdf_export.html

- app.py → the entire backend: all routes, database logic, prediction model, export functions
- requirements.txt → every Python package needed (Flask, Flask-Login, cs50, pandas, scikit-learn, WeasyPrint, etc.)
- finance.db → SQLite database, created automatically on first run
- static/style.css → tiny custom styles (card hover effects, better spacing, dark mode polish)
- static/chart-config.js → makes the doughnut and line charts work with the data passed from Flask
- templates/layout.html → base template with navbar and dark-mode toggle
- templates/index.html → dashboard with cards and charts
- templates/add.html → transaction form with smart category dropdown + custom input
- templates/history.html → monthly transaction table + export buttons
- templates/prediction.html → shows the scary-accurate forecast
- templates/pdf_export.html → separate clean template used only for PDF generation

### Challenges I ran into

1. Getting the 30-day line chart to show every single day (even empty ones). I tried doing it in SQL and gave up — building the date list in Python and filling zeros was way cleaner.
2. WeasyPrint threw a font error on the Codespace, but running one apt install command made it work perfectly.

### How to run MoneyFlow yourself

```bash
pip install -r requirements.txt
flask run


Created by FONG Cheong Ming (cmfong1121)
Hong Kong — December 14, 2025

Here is a footnote[^1].
A footnote can also have multiple lines[^2].
[^1]: My reference.
[^2]: To add line breaks within a footnote, add 2 spaces to the end of a line.
This is a second line.
