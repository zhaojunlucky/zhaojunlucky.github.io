---
title: "Traps in MySQL Version 5.6.27 Versus 5.6.33"
date: "2019-03-11 16:27"
categories: ["MySQL", "SQL", "Isolation Leve", "Insert Ignore"]
---

MySQL different version may have different behaviors or maybe it's bug, even if execute exactly same SQL.

MySQL's default transaction islocation leve is READ REPEATABLE. If we,
* Change transaction isolation level and execute update SQL as following
  ```sql
  SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;

  INSERT INTO table (...);
  ```
  In version 5.6.27, will receive error.

  | Error Code | Error Message                                                |
  | ---------- | ------------------------------------------------------------ |
  | 1665       | Cannot execute statement: impossible to write to binary log since BINLOG_FORMAT = STATEMENT and at least one table uses a storage engine limited to row-based logging. InnoDB is limited to row-logging when transaction isolation level is READ COMMITTED or READ UNCOMMITED. |

  It will pass in version 5.6.33 or later.

* Execute "INSERT IGNORE" with an non-existing foreign key id reference.

  In version 5.6.27, will receive error.

  | Error Code | Error Message                                                |
  | ---------- | ------------------------------------------------------------ |
  | 1452       | Cannot add or update a child row: a foreign key constraint fails (...) |

  In version 5.6.33, it will only log a warning message, but the SQL execution overall status is success.

  This is a bug to "INSERT IGNORE", [https://bugs.mysql.com/bug.php?id=78853](https://bugs.mysql.com/bug.php?id=78853).
