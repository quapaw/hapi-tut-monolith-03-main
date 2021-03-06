# Breaking the Monolith by using hapi 
## Background
Let me get the disclaimer out of the way: I am not an expert on Hapi
I started looking into Hapi's ability to break components out.
This is my attempt to follow other tutorials from a hello world to a true component system.
I have broken this down into the following steps

| Project  | Description | Link |
|---|---|---|
|hapi-tut-monolith-01|A simple hello world hapi project| [01](https://github.com/quapaw/hapi-tut-monolith-01)|
|hapi-tut-monolith-02a|Add services - customers and products| [02A](https://github.com/quapaw/hapi-tut-monolith-02a)|
|hapi-tut-monolith-02b|Adding Glue and externalizing config| [02B](https://github.com/quapaw/hapi-tut-monolith-02b)|
|hapi-tut-monolith-02c|Moving services into their own folders| [02C](https://github.com/quapaw/hapi-tut-monolith-02c)|
|**hapi-tut-monolith-03-main**|**Moved service into own project. Instructions here**|**[03-main](https://github.com/quapaw/hapi-tut-monolith-03-main)**|
|hapi-tut-monolith-03-customer|Just the customer service| [03-customers](https://github.com/quapaw/hapi-tut-monolith-03-customers)|
|hapi-tut-monolith-03-products|Just the produce service| [03-products](https://github.com/quapaw/hapi-tut-monolith-03-products)|
|hapi-tut-monolith-04a-customer|Movement of some files| [04a-customers](https://github.com/quapaw/hapi-tut-monolith-04a-customers)|
|hapi-tut-monolith-04b-customer|New methods| [04b-customers](https://github.com/quapaw/hapi-tut-monolith-04b-customers)|
|hapi-tut-monolith-04c-customer|Validation and Error Handling|[04c-customers](https://github.com/quapaw/hapi-tut-monolith-04c-customers)|
|hapi-tut-monolith-04d-customer|Unit Testing|[04d-customers](https://github.com/quapaw/hapi-tut-monolith-04d-customers)|
|hapi-tut-monolith-04e-customer|Add Mongo and API Doc|[04e-customers](https://github.com/quapaw/hapi-tut-monolith-04e-customers)|
|hapi-tut-monolith-05-customer|Combine work with products for full deployment|[05-customers](https://github.com/quapaw/hapi-tut-monolith-05-customers)|
|hapi-tut-monolith-05-product|Combine work with products for full deployment|[05-products](https://github.com/quapaw/hapi-tut-monolith-05-product)|
|hapi-tut-monolith-05-main|Combine work with products for full deployment|[05-main](https://github.com/quapaw/hapi-tut-monolith-05-main)|
|hapi-tut-monolith-06-customer|Move from npm to yarn|[06-customers](https://github.com/quapaw/hapi-tut-monolith-06-customers)|
|hapi-tut-monolith-07-customer|Customer project to go with 07-main|[07-customers](https://github.com/quapaw/hapi-tut-monolith-07-customers)|
|hapi-tut-monolith-07-product|Product project to go with 07-main|[07-products](https://github.com/quapaw/hapi-tut-monolith-07-products)|
|hapi-tut-monolith-07a-main|Catch up with 06 changes|[07a-main](https://github.com/quapaw/hapi-tut-monolith-07a-main)|
|hapi-tut-monolith-07b-main|Change in configuration|[07b-main](https://github.com/quapaw/hapi-tut-monolith-07b-main)|


#HAPI Tutorial - Monolith - 3 - main
This step moves the services customers and products into their own repository.
You will need access to create your own repository.  You can utilize github to do this.
Again, I used this [Tutorial](https://medium.com/@dstevensio/manifests-plugins-and-schemas-organizing-your-hapi-application-68cf316730ef#.2nve7u2r0) for the pattern of breaking the monolith.

## Move customers service into its owm repository
* Create a new project folder for the customers api service
* Move the customer files from the main project to the new customers project

Folder structure

```
-- index.js
-- package.json
-- customers.js
-- api-doc
---- |
---- | - customers.json
-- samples
---- |
---- | - customers.json

```

* Check this structure into a new repository in git.  For this example I have done that https://github.com/quapaw/hapi-tut-monolith-03-customers
* Add the dependencies to package.json in the main project to the customers repository.  NOTE: I have put the url to my git repository because I have not published this to npm
```
  "dependencies": {
    "glue": "^4.1.0",
    "hapi": "^16.1.0",
    "customers": "git+https://github.com/quapaw/hapi-tut-monolith-03-customers.git#master"
  }
```

* Change manifest.json
Take the relative path out of the register statement.  This will pull it from node_modules and not from path
```
{
  "plugin": {
    "register": "customers"
  }
}
```
## Do the same steps for the products api items

## Run Server and Test
###Start the server
```
node index.js
```
You should see a message stating your code is running
```
Server running at: http://localhost:3000
```
###Test the services
* Go to the following link [http://localhost:3000/customers](http://localhost:3000/customers)
* Go to the following link [http://localhost:3000/products](http://localhost:3000/products)

