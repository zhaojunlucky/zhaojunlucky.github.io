---
title: "Fetch Old Release Archies in Ubuntu"
date: "2019-01-14 15:39"
categories: linux docker
---

Rcently, when building a MySQL 5.6 Docker in Ubuntu 14.04, got errors:
```bash
W: Failed to fetch http://security.ubuntu.com/ubuntu/dists/trusty-security/universe/source/Sources  404  Not Found [IP: 91.189.88.41 80]

W: Failed to fetch http://security.ubuntu.com/ubuntu/dists/trusty-security/main/binary-amd64/Packages  404  Not Found [IP: 91.189.88.41 80]

W: Failed to fetch http://security.ubuntu.com/ubuntu/dists/trusty-security/restricted/binary-amd64/Packages  404  Not Found [IP: 91.189.88.41 80]

W: Failed to fetch http://security.ubuntu.com/ubuntu/dists/trusty-security/universe/binary-amd64/Packages  404  Not Found [IP: 91.189.88.41 80]

W: Failed to fetch http://security.ubuntu.com/ubuntu/dists/trusty-security/multiverse/binary-amd64/Packages  404  Not Found [IP: 91.189.88.41 80]

E: Some index files failed to download. They have been ignored, or old ones used instead.

```

This approach works well before, and just because some updates made in the `Dockerfile`, and cause to redownload the MySQL 5.6.

This is because the offical source **security** of ubuntu 14.04 is out of date, so, we can change it to a mirror source to fix the issue.

For example, replace the **security** by running following command before apt update in the Dockerfile.

  ```bash
    RUN sed -i "s/security\.ubuntu\.com/mirrors\.asnet\.am/g" /etc/apt/sources.list
  ```
You can check more mirros here [https://launchpad.net/ubuntu/+archivemirrors](https://launchpad.net/ubuntu/+archivemirrors).
