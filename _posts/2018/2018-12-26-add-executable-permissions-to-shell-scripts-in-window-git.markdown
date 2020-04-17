---
title: "Add Executable Permissions to Shell Scripts in Window Git"
date: "2018-12-26 14:19"
categories: git shell bash windows
---

When adding a shell script into Git, sometimes, it's need to add executabe permission for it. In Linux like system, it's very easy, as we can run `chmod +x <file>`, then push to Git repository as usual. But it's not possible in Windows with same way.

However, it's possible to use command `git update-index` to add permission.
* Check if a file has executabe Permissions

  Run `git ls-files --stage | grep foo.sh`, it will show as,
  ```bash
  100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c53910    foo.sh
  ```
  So, the file mode is `644`, doesn't have executabe permission
* Add executabe permission for the files

  Run `git update-index --chmod=+x foo.sh`, then run above command will show as,
  ```bash
  100755 e69de29bb2d1d6434b8b29ae775ad8c2e48c53910    foo.sh
  ```
  Now, the file has executabe permision, and just push it.
