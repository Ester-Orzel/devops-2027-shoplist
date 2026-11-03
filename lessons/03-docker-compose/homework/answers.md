# שיעור 3 - תשובות

1. שני containers. Compose בונה image לכל service, אבל השני לוקח הכל מה-cache, אז בפועל זה אותו image בשני שמות.
2. 9001 מחזיר `Shalom, Rivka!` ו-9002 מחזיר `Hello, Rivka!`.
3. פורט במחשב יכול להיות תפוס רק ע"י דבר אחד. בתוך ה-container לכל אחד יש רשת משלו, אז 8000 בשניהם לא מתנגש.
4. עוד service:
```yaml
  # greeter בצרפתית
  greeter-fr:
    build:
      context: ../../02-docker-basics/homework/greeter
    environment:
      GREETING: Bonjour
    ports:
      - "9003:8000"
```
5. greeter לא שומר שום מידע, אין לו מה לאבד. postgres שומר את המוצרים, והם צריכים להישאר גם כשה-container נמחק.
