# שיעור 2 - תשובות

1. `docker build -t greeter:v1 lessons/02-docker-basics/homework/greeter`
2. `docker run -d -p 9000:8000 --name greeter greeter:v1`
3. להוסיף `-e GREETING=Shalom`
4. `{"message":"Shalom, Rivka!"}`
5. FROM, WORKDIR, ההעתקה של requirements.txt וה-pip install יהיו CACHED, כי לא השתנו. ה-COPY של app.py וכל מה שאחריו ירוצו מחדש, כי app.py השתנה ומשלב שהשתנה הכל נבנה מחדש.
