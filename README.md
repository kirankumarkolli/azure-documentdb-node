# Node.js SDK for DocumentDB APIs of Azure Cosmos DB

![](https://img.shields.io/npm/v/documentdb.svg)
![](https://img.shields.io/npm/dm/documentdb.svg)
![](https://img.shields.io/github/issues/azure/azure-documentdb-node.svg)

Node.js SDK for DocumentDB APIs for Microsoft Azure Cosmos DB Service.

This project provides a node module that makes it easy to interact with DocumentDB APIs of Azure Cosmos DB (cosmosdb) Service.

For documentation please see the Microsoft Azure [Node.js Developer Center](http://azure.microsoft.com/en-us/develop/nodejs/) and the [ Node.js SDK Documentation](http://azure.github.io/azure-documentdb-node/).

## Installation
### Core Module

The core module uses the callbacks model for responses, exposed through the DocumentClient 

    npm install documentdb


## Prerequisites

To use this SDK to call DocumentDB APIs of Azure Cosmos DB, you need to first [create an account](https://docs.microsoft.com/en-us/azure/cosmos-db/create-documentdb-nodejs).

You can follow this [tutorial](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-nodejs-application) to help you get started.

#### Note:
When connecting to the [emulator](https://docs.microsoft.com/en-us/azure/cosmos-db/local-emulator) from the SDK, SSL verification is disabled. 

Follow these instructions to run the tests locally.

## Tests

### Prerequisites

1. Clone Azure/azure-documentdb-node repository
Please clone the source and tests from [https://github.com/Azure/azure-documentdb-node](https://github.com/Azure/azure-documentdb-node)

2. Install Node.js and npm
[https://docs.npmjs.com/getting-started/installing-node](https://docs.npmjs.com/getting-started/installing-node)

3. Install mocha package globally

        npm install -g mocha

### Running the tests

Using your command-line tool, from the root of your local copy of azure-documentdb-node repository: 
(If you are contributing changes and submitting PR then you need to ensure that you run the tests against your local copy of the source, and not the published npm package.) 

1. Remove documentdb, if previously installed

        npm remove documentdb

2. Install documentdb

        npm install source
        
3. Change to `test` directory

        cd source\test
        
4. Run the tests

        mocha -t 0 -R spec

If you just want to run the tests against the published npm package then skip steps #1 & #2 proceed directly to step #3

## Examples
### Hello World using Callbacks via the Core Module

```js
var DocumentClient = require('documentdb').DocumentClient;

var host = "[hostendpoint]";                     // Add your endpoint
var masterKey = "[database account masterkey]";  // Add the masterkey of the endpoint
var client = new DocumentClient(host, {masterKey: masterKey});

var databaseDefinition = { id: "sample database" };
var collectionDefinition = { id: "sample collection" };
var documentDefinition = { id: "hello world doc", content: "Hello World!" };

client.createDatabase(databaseDefinition, function(err, database) {
    if(err) return console.log(err);
    console.log('created db');

    client.createCollection(database._self, collectionDefinition, function(err, collection) {
        if(err) return console.log(err);
        console.log('created collection');

        client.createDocument(collection._self, documentDefinition, function(err, document) {
            if(err) return console.log(err);
            console.log('Created Document with content: ', document.content);

            cleanup(client, database);
        });
    });
});

function cleanup(client, database) {
    client.deleteDatabase(database._self, function(err) {
        if(err) console.log(err);
    })
}
```

### Youtube Videos

Getting started with DocumentDB Node.js SDK:

[![Azure Demo: Getting started with DocumentDB Node.js SDK](http://img.youtube.com/vi/UAE7h9PCZjA/0.jpg)](http://www.youtube.com/watch?v=UAE7h9PCZjA)

## Need Help?

Be sure to check out the Microsoft Azure [Developer Forums on MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB) or the [Developer Forums on Stack Overflow](https://stackoverflow.com/questions/tagged/azure-cosmosdb) if you have trouble with the provided code.

## Contribute Code or Provide Feedback

If you would like to become an active contributor to this project please follow the instructions provided in [Azure Projects Contribution Guidelines](http://azure.github.io/guidelines.html).

If you encounter any bugs with the library please file an issue in the [Issues](https://github.com/Azure/azure-documentdb-node/issues) section of the project.

## Learn More

* [Azure Developer Center](http://azure.microsoft.com/en-us/develop/nodejs)
* [Node.js SDK Documentation for using DocumentDB APIs of Azure Cosmos DB Service.](http://azure.github.io/azure-documentdb-node/)
* [More information about the Node.js SDK for using DocumentDB APIs of Azure Cosmos DB Service.](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-sdk-node)
* [Azure Cosmos DB Service](https://azure.microsoft.com/en-us/blog/dear-documentdb-customers-welcome-to-azure-cosmos-db/)
* [Azure Cosmos DB Community Page](https://docs.microsoft.com/en-us/azure/cosmos-db/community)
