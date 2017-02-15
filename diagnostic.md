# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

  ```md
    It enables tables to have many to many relationship
  ```

1.  Provide a database table structure and explain the Entity Relationship that
  describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
  (Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
  `Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
  join table with references to `Movies` and `Profiles`.

  ```md
  Profile => one-to-many => Favorites <= many-to-one <= Movie
  A profile will have many favorites in which making a movie having many favorites.
  ```

1.  For the above example, what needs to be added to the Model files?

  ```rb
  class Profile < ActiveRecord::Base
    has_many :movies, through: :favorites
    has_many :favorites
  end
  ```

  ```rb
  class Movie < ActiveRecord::Base
    has_many :profiles, through: :favorites
    has_many :favorites
  end
  ```

  ```rb
  class Favorite < ActiveRecord::Base
    belongs_to :movie
    belongs_to :profile
  end
  ```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

  ```md
    The purpose of the serializer is to make the view outputted in the way
    one wants.
  ```

  ```rb
  class ProfileSerializer < ActiveModel::Serializer
    attributes :movie_id

    def movie_id
      object.movie_id
    end
  end
  ```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

  ```sh
    bin/rails generate scaffold favorite movie:references profile:references
  ```

1.  What is `Dependent: Destroy` and where/why would we use it?

  ```md
    it will destroy the main object and the associating objects to the main object. One would use it when parent instance have child instances.
  ```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

  ```md
    The game settler of Catan would have an one-to-many and as well as a many-to-many relationship.
    Many-to-Many => the resources you have on hand verse the resources table
    One-to-Many => the skill cards you have on hand verse the skill card table.
  ```
