MongoDB is **an open source [[NoSQL]] database management program**. [[NoSQL]] is used as an alternative to traditional [[Relationsal Database ManagementSystem]]. [[NoSQL]] databases are quite useful for working with large sets of distributed data. MongoDB is a tool that can manage document-oriented information, store or retrieve information.

MongoDB Atlas is **a fully-managed cloud database that handles all the complexity of deploying, managing, and healing your deployments on the cloud service provider of your choice** (AWS , Azure, and GCP). MongoDB Atlas is the best way to deploy, run, and scale MongoDB in the cloud.
https://cloud.mongodb.com/v2/637b55be7d00c3067d6d3355#clusters

After creating account and cluster from  Atlas, you can use simple python script to interact with MongoDB ([[NoSQL]])

If you don't want to pay just yet, you can also simulate it via Docker on your local machine.
~~~yml
version: '3'
services:
  mongodb:
    image: mongo
    restart: always
    ports:
      - '27017:27017'
    volumes:
      - ./mongodb/db:/data/db
~~~
