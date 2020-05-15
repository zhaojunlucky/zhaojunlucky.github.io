---
last_modified_at: 2020-05-15T05:57:04+00:00
title: disable git command openssh popup
categories:
- git

---
If you don't want to input git username and password through the openssh popup, you can disable it by the following configuration.
```bash
# global configuration
git config --global core.askPass ""
# just this clone
git -c core.askPass="" clone <https_url>
```

With this configuration, the git will read username and password through the console.