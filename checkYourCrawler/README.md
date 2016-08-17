# Check your Crawler with Neo4j!

## Introduction

Ixxo Web Mining has developped a product called Fetch-Server. This is a configurable Web Spider (aka Web Crawler) who can fetch the Web 
to extract data and push it into the Ixxo Indexer like showed in the schema below:

![Fig1. General process](./general_process.png "Fig1. General process")

After downloading the interesting part of a Web page, the Fetch Server sends the data to the Ixxo Indexer, able to extract entities from data (like Organizations, Countries, etc.).

Neo4j helped us to rule our Crawler by checking page traversal of it. 
 

## How a Web Spider works?

A Web Spider is a process able to recursively download pages and extract URLs from them. Then the extracted URLs are downloaded and so on.


Each extracted Url is put into a queue called Frontier. The treatment polls the next url in the Frontier and download the page. 
Usually, any Crawler implements some common features: 

* A selection policy: a white list/black list principle to rule the pages to download or not
* A politness policy: a think time or other stuffs to ensure to the visited site we are not malicious
* A re-visit policy: a trigger to say to the main process that page has changed and we need to download it again

## How the Fetch-Server works?

The Fetch-Server is a Web Spider with the following features:
* The selection policy is divided in two parts: a URLs selection policy (download the page or not) and a Content selection policy (to send the extracted data to Ixxo Indexer or not)
* The politness policy is ruled by a think time and the robots.txt file management
* The re-visit policy is enabled or disabled by the user and based on the page checksum 
* Many other parameters...

Technically, the Fetch-Server is drivable by Restful api:
```
{
  "message" : "Oxway Fetch Server",
  "version" : "Version ${version}",
  "links" : [ {
    "rel" : "self",
    "href" : "http://localhost:8080"
  }, {
    "rel" : "fetchs.command.test",
    "href" : "http://localhost:8080/fetchs/fetch"
  }, {
    "rel" : "fetchs.command.start",
    "href" : "http://localhost:8080/fetchs/fetch"
  }, {
    "rel" : "fetchs.command.delete",
    "href" : "http://localhost:8080/fetchs/delete/{id}"
  }, {
    "rel" : "fetchs.command.stop",
    "href" : "http://localhost:8080/fetchs/stop/{id}"
  } ]
}
```





