# SQLite

- [SQLite Browser](https://github.com/sqlitebrowser/sqlitebrowser)

# Import SQLite3 Library and Initialize

```
import sqlite3

conn = sqlite3.conect('db_name.sqlite')
cur = conn.cursor()
```

### Execute SQL commands: Examples
```
cur.execute('''
DROP TABLE IF EXISTS Counts''')

cur.execute('''
CREATE TABLE Counts (email TEXT, count INTEGER)''')

cur.execute('SELECT count FROM Counts WHERE email = ? ', (email, ))
```

### Write to disk
```
conn.commit()
```

### Looping through SQL
```
sqlstring = '...'

```

### Close
```
cur.close()
```
