Reactivemongo Demo
========================

Based on
- https://github.com/zenexity/Play-ReactiveMongo/tree/master/samples/Play-ReactiveMongo-Sample

Utilizing Reactivemongo driver and Play Plugin
- http://reactivemongo.org/
- https://github.com/zenexity/Play-ReactiveMongo

Prerequisites 
==============
### Mongo and Data setup

- http://www.mongodb.org/
- http://docs.mongodb.org/manual/tutorial/getting-started/

We're using the default "test" database and a "people" collection

	$ mongod
	$ mongo
	> db
	test
	> a = {name : "mongo", age : "23"}
	{ "name" : "mongo", "age" : "23" }
	> db.people.insert(a)
	> db.people.find()
	{ "_id" : ObjectId("50ea023705bdb365a2d7a24d"), "name" : "mongo", "age" : "23" }

### Key elements of application setup

project/Build.scala 
- Add reactve resolver and dependencies

	val appDependencies = Seq(
		// Add your project dependencies here,
		jdbc,
		anorm,
		"reactivemongo" %% "reactivemongo" % "0.1-SNAPSHOT" cross CrossVersion.full,
		"play.modules.reactivemongo" %% "play2-reactivemongo" % "0.1-SNAPSHOT" cross CrossVersion.full
	)

	val main = play.Project(appName, appVersion, appDependencies).settings(
	    // Add your own project settings here      
	    resolvers += "sgodbillon" at "https://bitbucket.org/sgodbillon/repository/raw/master/snapshots/"
	)

conf/play.plugins
- Create this file and add ReactiveMongo plugin

	400:play.modules.reactivemongo.ReactiveMongoPlugin

conf/application.conf
- add mongodb settings

	
	mongodb.servers = ["localhost:27017"]
	mongodb.db = "test"


The rest of the routes and app files can be found where expected. 

### Test it
- http://localhost:9000/
- http://localhost:9000/persons/mongo