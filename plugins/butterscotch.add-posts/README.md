## butterscotch.add-posts

### Introduction

It is a plugin which adds the core functionality of adding posts to butterscotch section.

### Installation

Instructions for installing any plugin for butterscotch plugin system are explained [here][1] 


### Methods

#### Core

These are the methods that are defined by this plugin. These methods can be extended as well as reused( if public) in another plugin which takes this plugin as a dependency.

##### Public

These are the methods that any plugin's execute method can invoke when that plugin's execute method takes this plugins as a dependency.

| Method Name                          | returns                             | parameters                  |
| ------------------------------------ |:-----------------------------------:|:---------------------------:|
| createAdminUserSchemaDefinition      | [definition Object][2]              | none      |
| modifyAdminUserSchema                | [schema Object][3]                  | [schema Object][3]          |
| getAdminUserSchemaModel              | [mongoose model][4]                 | none                        |
| createUserDataBeforeInsert           | Object                              | src object, dest object     |
| modifyUserDataBeforeInsert           | Object                              | object                      |


###### createAdminUserSchemaDefinition  

**returns:** A object which contains the [definiton][2] of the schema  
```
// Example
{
  Name: String,
  Age: Number,
  Sex: String
}
```
**parameters:** none  
**Description:** This method is called just before passing the schema to the [mongoose.Schema][3] constructor. It gives the definiton and passes the definition to the constructor.  

###### modifyAdminUserSchema  

**parameters:** schema object  
**returns:** modified schema object  
**Description:** This method is called on the schema object which is created using [mongoose.Schema][3] constructor.  

###### getAdminUserSchemaModel  

**parameters:** none  
**returns:** [mongoose model][4]  
**Description:** This method is called whenever one need to call the `adminUser` model to perform queries or any other operation that MongooseJS models support  

###### createUserDataBeforeInsert  

**parameters:** plain [object][5] which contains the user details from the form
```
// Example
{
  username: 'butterscotch',
  age: 22
}
```
**returns:** modified [object][5] which is compatible with `adminUser` schema  
```
// Example
{
  local: {
    username: 'butterscotch'
  },
  age: 22

}
```
**Description:** This method is called every time a new user is inserted in the `adminUser` schema.  

###### modifyUserDataBeforeInsert  

**parameters:** [object][5] which contains the user details which will be passed to `adminUser` Schema
```
// Example
{
  local: {
    username: 'butterscotch'
  },
  age: 22

}
```
**returns:** modified [object][5] which is also compatible with `adminUser` schema  
```
// Example
{
  local: {
    username: 'butterscotchmodified'
  },
  age: 22

}
```
**Description:** This method is called every time a new user is inserted in the `adminUser` schema after createUserDataBeforeInsert.  

##### Private

These are the methods that only this plugin's execute method can invoke and the execute method of the very same plugin has to include self as a plugin's execute method dependency. However, any method's init method can extend it after including this plugin name as a dependency.

#### Extends

These are the methods of another plugins which are extended by this plugin.



[1]: {{ book.url }}#plugin-installation  "Optional Title Here"
[2]: http://mongoosejs.com/docs/schematypes.html  "Optional Title Here"
[3]: http://mongoosejs.com/docs/api.html#schema_Schema
[4]: http://mongoosejs.com/docs/api.html#index_Mongoose-model
[5]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects