---
layout: post
title: "Serving static files"
categories: ["tutorial", "programming", "devops"]
permalink: /serving-static-files
---

![Screenshot](/assets/2021-10-12-static-files/library.jpg)

Today, modern web applications needed static files to serve users. There are many kinds of files: music, videos, archives, documents, or any type. A basic functions:

1. Users can upload his/her file to the server
2. Users can download/view files

There are plenty of solutions in terms of framework or programming language. In PHP, files store in the same directory of codes. The Django project, it has its own library to serve files. There was a ready solution for beginners/startups for not worrying about serving the files. The size of the project is small and the number of static files is not huge, that's okay, it will work as expected.

Let's think about a project with a large scope with files and low latency.

**1-option**: 3rd party solution: [AWS S3](https://aws.amazon.com/s3/){:target="_blank"}

S3 server is basically, a solution by Amazon, it has packages for famous languages to use its API: to upload/delete the file. And your files are stored in AWS servers and you do not worry about load balancing, backup, and so on. But, you need to pay for bandwidth, for example, your files are mostly are videos, you need to pay money per downloaded GB. If you need with low latency of files, even you can integrate with AWS Cloudfront. It is basically, cached files in with different regions around the world.

**2-option**: 3rd party free software: [Minio](https://minio.io/){:target="_blank"}

Minio is a package serving the files same as AWS S3 structure but in your server. You need to use a Docker container to run Minio. Now, you do not worry about AWS prices. But, you need to be aware of backups, system crashes and pays for traffic for your server provider. If you have files in AWS S3, you can [copy all files](https://www.scaleway.com/en/docs/tutorials/migrate-data-minio-client/){:target="_blank"} to own minio server. Here simple docker-compose file to test in local machine: docker-compose.yml

```
version: '3.7'

services:
  minio:
    user: root
    image: bitnami/minio:2023.8.29-debian-11-r0
    restart: always
    volumes:
      - 'minio_data:/bitnami/minio/data'
    ports:
      - "8001:9000"
      - "8002:9001"
    environment:
      MINIO_ROOT_USER: ${MINIO_ACCESS_KEY}
      MINIO_ROOT_PASSWORD: ${MINIO_SECRET_KEY}
volumes:
  minio_data:
    driver: local
```

To start run the following command: docker-compose up -d.

**3-option**: Recently, [Cloudflare](https://blog.cloudflare.com/introducing-r2-object-storage/){:target="_blank"} launched its object storage service at a very inexpensive price.

For now, I know those solutions, if you have a better approach, let me know in the comments.

[Link](https://ergashevn.blogspot.com/2021/10/serving-static-files.html){:target="_blank"}
