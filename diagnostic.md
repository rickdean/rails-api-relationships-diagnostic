# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

```sh
Join tables are essential in linking two tables in the database together.
```

1.  Provide a database table structure and explain the Entity Relationship that
describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
(Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
`Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
join table with references to `Movies` and `Profiles`.

```sh
Table: Profiles
given_name:string
surname:string
email:string

Table: Movies
title:string
release_date:datec
length:string

Table: Favorites
movie_id
profile_id
```

1.  For the above example, what needs to be added to the Model files?

```rb
class Profile < ActiveRecord::Base
has_many :movies, through: :favorites
end
```

```rb
class Movie < ActiveRecord::Base
has_many :profiles, through: :favorites
end
```

```rb
class Favorite < ActiveRecord::Base
belongs_to :movie, inverse_of: :favorites
belongs_to :profile, inverse_of: :favorites
end
```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

```sh
The serializer indicates what fiels will be passed through to the front end.
```

```rb
class ProfileSerializer < ActiveModel::Serializer
attributes :id, :given_name, :surname, :email
end
```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

```sh
I do not believe you would  be able to scaffold a many to many relationship table. 
```

1.  What is `Dependent: Destroy` and where/why would we use it?

```sh
Dependant: Destroy is used to ensure that related records are destroyed.  One
example would be a book table and a related author table.  You may wish to
destroy all books from the book table that are related to an author when the author
is destroyed.  You would indicate this in the model.
```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

```sh
An example of one to many could be in the case of an application that has a 'movies'
and 'directors' table.  There is typically one director per movie but a director can be
associated with many movies.  In the same application you could have a 'producers' table.
This could link to the 'movies' table as a many to many relationship.
```
