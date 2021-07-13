# Queries For the Mongo Section

- Demonstrate the usage of $match, $group, aggregate pipelines.

```
1. $match

 > db.moviedb.aggregate([{$match:{imdbrating:8.7,Genre:'Action'}}]).pretty()
  
2. $Group 

 > db.moviedb.aggregate([{$group: { _id: "$Genre", Rating: {$sum:"$imdbrating"}} } ])
  
3. Aggregate Pipeline 

 > db.moviedb.aggregate([{$match :{Referable:true}},{$group :{_id :"$Genre",Average_Rating : {$avg: "$imdbrating"} }}])
  
```
- Demonstrate the Map-Reduce aggregate function on this Dataset.

```
> var mapper =function(){emit(this.Genre,this["imdbrating"])};
> var reduce =function(Genre,imdb){return Array.sum(imdb)};
> db.moviedb.mapReduce(mapper, reduce, {out:"imdbout"});
> db.imdbout.find().pretty();
```
- Count the number of Movies which belong to the Thriller category and find out the total number of Positive Reviews in that Category.
```
> db.moviedb.aggregate([{$match: { Genre: "Thriller"} }, {$group: { _id: "$Genre", SumofFeedbacks: {$sum:"$positivefeedback"}, NoofThrillers: {$sum:1}}} ])
```
- Group all the Records by Genre and find out the Total Number of Positive Feedbacks by Genre.
```
> db.moviedb.aggregate([{$group: { _id: "$Genre", Sumoffeedbacks: {$sum:"$positivefeedback"}, Noofrecordsinthegenre: {$sum:1}} } ])
```
<hr>
