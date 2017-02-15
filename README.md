# Breaking the Monolith by using hapi 
## Background
Let me get the disclaimer out of the way: I am not an expert on Hapi
I started looking into Hapi's ability to break components out.
This is my attempt to follow other tutorials from a hello world to a true component system.
I have broken this down into the following steps

| Project  | Description | Link |
|---|---|---|
|hapi-tut-monolith-01|A simple hello world hapi project| [https://github.com/quapaw/hapi-tut-monolith-01](github)|
|hapi-tut-monolith-02a|Add services - customers and products| [https://github.com/quapaw/hapi-tut-monolith-02a](github)|
|hapi-tut-monolith-02b|Adding Glue and externalizing config| [https://github.com/quapaw/hapi-tut-monolith-02b](github)|
|**hapi-tut-monolith-02c**|Moving services into their own folders| [https://github.com/quapaw/hapi-tut-monolith-02c](github)|
|hapi-tut-monolith-03-main|Moved service into own project.  This pulls the services in| [https://github.com/quapaw/hapi-tut-monolith-03-master](github)|
|hapi-tut-monolith-03-customer|Just the customer service| [https://github.com/quapaw/hapi-tut-monolith-03-customers](github)|
|hapi-tut-monolith-03-products|Just the produce service| [https://github.com/quapaw/hapi-tut-monolith-03-products](github)|

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

