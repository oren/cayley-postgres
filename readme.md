# Cayley graph database with Postgresql as backend

Setup Postgres
```
sudo apt-get install postgresql postgresql-contrib
sudo su - postgres
psql
createuser josh -s
\password josh (enter password: password123)
create database testdb
```

Setup cayley
```
cayley init --config=cayley.cfg
cayley load --config=cayley.cfg --quads=canada.nq
cayley http --config=cayley.cfg -assets /home/oren/projects/go/src/github.com/google/cayley/
cayley repl --config=cayley.cfg
```

repl command
```
who is justin in love with?
g.V("person:justin").Out("in love with").All()

who is in love with someone?
g.V().Tag("name").Out("in love with").All()

who is in love with justin?
g.V().Tag("name").Out("in love with").Is("person:justin").All()

who is in love with justin? (another version)
g.V("person:justin").In("in love with").All()

who is in love with justin and lives in the US?
g.V("person:justin").In("in love with").Tag("name").Out("lives in").Is("country:us").All()

who is in love with justin, lives in the US, and is moving to canada?
loveJustin = g.V("person:justin").In("in love with")
liveUS = g.V("country:us").In("lives in")
moveCanada = g.V("country:canada").In("is moving to")
loveJustin.And(liveUS).And(moveCanada).All()

who bans puppies?
g.V("animals:puppies").In("bans").All()

who is pissed with who?
g.V("type").Out("person").Out("is pissed with").All()

```

logging
```
cayley http --config=cayley.cfg -v=2 -alsologtostderr
```
