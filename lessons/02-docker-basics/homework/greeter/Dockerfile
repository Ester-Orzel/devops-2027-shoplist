# מתחילים מ-image של פייתון בגרסה קבועה
FROM python:3.11-slim

# תיקיית העבודה בתוך ה-container
WORKDIR /app

# קודם מעתיקים רק את רשימת הספריות
COPY requirements.txt .

# מתקינים את הספריות (לפני הקוד, בשביל ה-cache)
RUN pip install --no-cache-dir --trusted-host pypi.org --trusted-host files.pythonhosted.org -r requirements.txt

# עכשיו מעתיקים את הקוד
COPY app.py .

# השרת מאזין בפורט 8000
EXPOSE 8000

# מריצים את השרת
CMD ["python", "app.py"]
