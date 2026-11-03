# שיעור 4 - תשובות

1. stats מגיע אליו ברשת של Compose לפי השם: `http://backend:5000`. הדפדפן לא מגיע אליו ישירות, הוא פונה ל-Nginx ב-8080 ו-Nginx מעביר את `/api/` ל-backend.

2. אחרי down ו-up המוצרים נשארו, כי הם ב-named volume `postgres-data` ו-down לא מוחק אותו. down -v מוחק את ה-volume, והמסד מתחיל ריק.

3. bind mount, כי בצד שמאל יש נתיב לקובץ במחשב ולא שם של volume. שינוי אחרי שהמסד נוצר לא ישפיע, כי init.sql רץ רק בפעם הראשונה. צריך down -v ו-up.

4. הרשת `docker_default` וה-volume `docker_postgres-data`. Compose מוסיף לשמות את שם התיקייה של הקובץ (`docker`).

5. ב-image הסופי יש רק Nginx, התיקייה dist וה-nginx.conf. אין Node ואין build.js, הם נשארו בשלב הראשון. אין CMD כי יורשים אותו מ-nginx. ל-stats אין שלב בנייה, והוא צריך Node גם כשהוא רץ.

6. single 92.7MB, multi 92.7MB, kitchen 244MB. multi כמו single כי בשניהם יש רק Nginx וכמה קבצים קטנים. Node נשאר ב-kitchen.

7. Nginx בוחר את ה-location עם הקידומת הארוכה יותר, ו-`/api/stats` ארוך מ-`/api/`. הלוכסן בסוף מוריד את `/api/`, אז `/api/products` מגיע ל-backend בתור `/products`.
