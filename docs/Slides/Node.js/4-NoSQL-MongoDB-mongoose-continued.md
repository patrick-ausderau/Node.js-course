# NoSQL MongoDB database and mongoose continued
  * [Previous week: NoSQL](../Week1/W2-2-NoSQL-MongoDB-mongoose.html)
  * [Previous week: db auth and deploy on Jelastic](../Week1/W2-4-Deploy_on_jelastic.md)
  * [Searching (by Mozilla)](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/mongoose#Searching_for_records)
  * [Updating](http://mongoosejs.com/docs/documents.html)
  * [Deleting](http://mongoosejs.com/docs/api.html#model_Model.findByIdAndRemove)
  
#### Exercises
  * continue Cats-exercise from last week (you can get it from [here](https://github.com/patrick-ausderau/testdb))
  * Add full CRUD functionality to the app
    * Create by using POST-method
        * this was done last week
    * Read by using GET-method
        * create a form to change the properties (like weight, age and gender) that cats are queried by
    * Update by using PATCH-method
        * create a form to update a selected cat (form is basically the same as when adding cats)
    * Delete by using DELETE-method
        * delete selected cat (you can add delete-link next to each cat)
  * Separate your app into [modules](https://nodejs.org/api/modules.html) 
    * One module for connecting the database and creating the model out of a schema (check example in oma: Documents / exercise examples / w2_thursday)
    * Consider having the schema in a separate file? And specific functions associated with it (e.g. find by schema attributes,...)?
