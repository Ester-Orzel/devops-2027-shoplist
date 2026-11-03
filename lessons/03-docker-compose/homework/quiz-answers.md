# בוחן שיעור 3: אסתר אורצל

1. ב
2. ג
3. שרת שמקבל את הבקשות מהדפדפן ומעביר כל אחת לסרוויס המתאים שמאחוריו.
4. ב
5. בתור /products. הלוכסן בסוף ה-proxy_pass גורם ל-Nginx להוריד את /api/.
6. כי אף אחד מבחוץ לא צריך לגשת אליו. רק Nginx ו-stats מדברים איתו, והם ברשת הפנימית.
7. down מוחק את ה-containers והרשת, ה-volume נשאר. down -v מוחק גם את ה-volume, כלומר את הנתונים.
8. ב
9. כי הוא מחכה רק שה-container יעלה, לא שהמסד מוכן לחיבורים. בשביל זה צריך healthcheck ו-condition: service_healthy.
10. ב
11. הראשון named volume ש-Docker מנהל, בשביל לשמור את הנתונים. השני bind mount, קובץ מהמחשב שלי שנכנס ל-container.
12. ב
13. `docker compose config`
14. כי הקובץ עולה ל-Git וכולם רואים אותו. במקום זה שמים את הסיסמה בקובץ .env שלא עולה ל-Git, ובקובץ כותבים ${POSTGRES_PASSWORD}.
15. ב-nginx.conf יש את backend ו-stats, ולבד אין רשת של Compose אז Nginx לא מוצא אותם (host not found) ונופל.
