# שיעור 4 - תשובות

## 1. ל-backend אין `ports`. איך stats מגיע אליו? ואיך הדפדפן מגיע אליו?
stats פונה ל-backend בתוך הרשת הפנימית ש-Compose יצר, לפי השם שלו: `http://backend:5000`. הדפדפן בכלל לא מדבר עם ה-backend. הוא פונה ל-Nginx בפורט 8080, ו-Nginx מעביר את בקשות ה-`/api/` הלאה ל-backend.

## 2. עושים `docker compose down` ואחר כך `up`. המוצרים נשארו? ומה אם `down -v`?
כן, המוצרים נשארו, כי הם שמורים ב-volume בשם `postgres-data` ו-`down` לא נוגע בו. עם `down -v` ה-volume נמחק, אז המוצרים הולכים והמסד מתחיל מחדש, ריק.

## 3. השורה `../sql/init.sql:/docker-entrypoint-initdb.d/init.sql`: איזה סוג volume, ומה אם משנים את `init.sql` אחרי שהמסד נוצר?
זה bind mount. אפשר לזהות כי הצד השמאלי הוא נתיב לקובץ אצלי במחשב, ולא שם של volume. אם משנים את `init.sql` אחרי שהמסד כבר קיים, לא קורה כלום, כי postgres מריץ את הקובץ הזה רק בפעם הראשונה שהוא יוצר את המסד. כדי שהשינוי ייכנס צריך `down -v` ואז `up`.

## 4. מה שם הרשת ומה שם ה-volume?
הרשת נקראת `docker_default` וה-volume נקרא `docker_postgres-data`. Compose לוקח את שם התיקייה שבה נמצא קובץ ה-Compose (`docker`) ומוסיף לו את שם הרשת או ה-volume.

## 5. ב-`Dockerfile.multistage`: מה יש ב-image הסופי ומה אין? למה אין `CMD`? ולמה ל-stats לא צריך multi-stage?
ב-image הסופי יש רק Nginx עם התיקייה `dist` וקובץ ההגדרות. אין בו Node ואין `build.js`, כי הם נשארו בשלב הראשון. אין `CMD` כי ה-image של Nginx כבר יודע להפעיל את עצמו. ל-stats לא צריך multi-stage כי אין לו שלב בנייה, הוא פשוט מריץ את `server.js`, וצריך Node גם בזמן ההרצה.

## 6. שלושת הגדלים: למה `multi` כמעט בגודל של `single`?
יצא `single` 92.7MB, `multi` 92.7MB ו-`kitchen` 244MB. `multi` קטן כמו `single` כי בשניהם ה-image הסופי הוא בעצם Nginx עם כמה קבצים קטנים. Node, שמנפח את `kitchen`, נשאר בשלב הבנייה ולא עובר הלאה.

## 7. ב-`nginx.conf`: למה `/api/stats` מגיע ל-stats? ומה הלוכסן בסוף `http://backend:5000/` עושה?
`/api/stats` מתאים גם ל-`/api/stats` וגם ל-`/api/`, ו-Nginx בוחר את הקידומת הארוכה יותר, ולכן זה הולך ל-stats. הלוכסן בסוף גורם ל-Nginx להסיר את `/api/` מהכתובת, אז בקשה ל-`/api/products` מגיעה ל-backend בתור `/products`.
