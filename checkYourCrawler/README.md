# Check your Crawler with Neo4j!

## Introduction

Ixxo Web Mining has developped a product called Fetch-Server. This a configurable Web Spider (aka Web Crawler) who can fetch the Web 
to extract data and push it into the Ixxo Indexer like showed in the schema below:

![Fig1. General process](./general_process.png "Fig1. General process")

After downloading the interesting part of a Web page, the Fetch Server sends the data to the Ixxo Indexer, able to extract entities from data (like Organizations, Countries, etc.).

Neo4j helped us to rule our Crawler by checking page traversal of it. 
 

## How a Web Spider works ?

A Web Spider is a component able to recursively download pages and extract URLs from them. Then the extracted pages are downloaded and so on.



