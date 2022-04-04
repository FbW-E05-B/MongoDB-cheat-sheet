# MongoDB-cheat-sheet


### Show All Databases
```js
show dbs
```
### Show Current Database
```js
db
```
 ### Create Or Switch Database
 ```js
use acme
```
# Drop
```js
db.dropDatabase()
```
### Create Collection
```js
db.createCollection('posts')
```
### Show Collections
```js
show collections
```
### Insert Row

```js
db.posts.insert({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})
```

### Insert Multiple Rows
```js
db.posts.insertMany([
  {
    title: 'Post Two',
    body: 'Body of post two',
    category: 'Technology',
    date: Date()
  },
  {
    title: 'Post Three',
    body: 'Body of post three',
    category: 'News',
    date: Date()
  },
  {
    title: 'Post Four',
    body: 'Body of post three',
    category: 'Entertainment',
    date: Date()
  }
])
```
### Get All Rows
```js
db.posts.find()
```
### Get All Rows Formatted
```js
db.posts.find().pretty()
```
### Find Rows
```js
db.posts.find({ category: 'News' })
```
### Sort Rows
# asc
```js
db.posts.find().sort({ title: 1 }).pretty()
```
# desc
```js
db.posts.find().sort({ title: -1 }).pretty()
```
### Count Rows
```js
db.posts.find().count()
db.posts.find({ category: 'news' }).count()
```
### Limit Rows
```js
db.posts.find().limit(2).pretty()
```
### Chaining
```js
db.posts.find().limit(2).sort({ title: 1 }).pretty()
```
### Foreach
```js
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})
```
### Find One Row
db.posts.findOne({ category: 'News' })
### Find Specific Fields
```js
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})
```
### Update Row
```js
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})
```
### Update Specific Field
```js
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})
```
### Increment Field ($inc)
```js
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})
```
### Rename Field
```js
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})
```
### Delete Row
```js
db.posts.remove({ title: 'Post Four' })
```
### Sub-Documents
```js
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})
```
### Find By Element in Array ($elemMatch)
```js
db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)
```
## Add Index
```js
db.posts.createIndex({ title: 'text' })
```
### Text Search
```js
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})
```
### Greater & Less Than
```js
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })
```
