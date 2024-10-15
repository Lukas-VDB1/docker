# Gebruik een officiële Python runtime als parent image
FROM python:3.13-slim

# Stel de werkdirectory in de container in
WORKDIR /usr/src/app

# Kopieer pip requirements file en installeer Python dependencies
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Kopieer de rest van de applicatiecode
COPY . .

# Stel environment variabelen in
ENV FLASK_APP=app.py

# Expose de poort waarop de app draait
EXPOSE 5000

# Specificeer de command om de app te draaien
CMD flask run
