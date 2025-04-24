# Temel Kod Şablonu (Google Colab ile çalıştır)
# Tüm kütüphaneler yüklü gelsin
!pip install requests pandas

import requests, json, smtplib
from email.mime.text import MIMEText

# API Key'ler
ALPHA_VANTAGE_KEY = "AU4PA9806TQH7T51"
NEWSAPI_KEY = "AU4PA9806TQH7T51"

def get_stock_data(symbol):
    url = f"https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol={symbol}&apikey={ALPHA_VANTAGE_KEY}"
    data = requests.get(url).json()
    return float(data['Global Quote']['05. price'])

nvda_price = get_stock_data("NVDA")
amzn_price = get_stock_data("AMZN")
# ... Diğer hisseler

# Mail Gönderimi
msg = MIMEText(f"Nvidia: {nvda_price}$, Amazon: {amzn_price}$")
msg['Subject'] = 'Günlük Borsa Raporu'
msg['From'] = 'borsacimarul@gmail.com'
msg['To'] = 'sezerinci59@gmail.com'

with smtplib.SMTP('smtp.gmail.com', 587) as server:
    server.starttls()
    server.login('borsacimarul@gmail.com', 'sjpe vwrm daax mfsy')
    server.send_message(msg)
