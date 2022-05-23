# nano-ORM-py
## Nano-ORM in Python
#### For generating SQL for basic CRUD statements


## Usage examples:

    >>> upsert("tbl", LogID=500, LoggedValue=5)
    "INSERT INTO tbl (LogID, LoggedValue) VALUES ('500', '5') ON DUPLICATE KEY UPDATE LogID = '500', LoggedValue = '5';"

    >>> read("tbl", **{"username": "morten"})
    "SELECT * FROM tbl WHERE username = 'morten';"

    >>> read("tbl", **{"user_type": 1, "user_group": "admin"})
    "SELECT * FROM tbl WHERE user_type = '1' AND user_group = 'admin';"

    >>> parameterized(insert("test", c1=None, c2="?"))
    "INSERT INTO test (c1, c2) VALUES (NULL, ?);"


## **Note**: Don't pass user-controlled variables un-sanitized! 
### Examples of malicious use / SQL injection:

    >>> read("tbl", **{"user_group": "random'; DROP TABLE tbl; --"})
    "SELECT * FROM tbl WHERE user_group = 'random'; DROP TABLE tbl; --';"
