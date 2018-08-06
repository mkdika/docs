# Crecto::Repo::Query

The Query class provides building robust composable query builder for retrieving and manipulate data.  

Generally \(but not necessary\), its easiest to define a shortcut variable at the top level of your application.

```ruby
Query = Crecto::Repo::Query
```

The query object can be composed and manipulated before being used.

```ruby
query = Query.new
query = query.where(is_admin: true) if role === "admin"
query = query.where(is_user: true) if role === "user"
Repo.all(User, query)
```

## Query methods

### `where`

```ruby
Query.where(name: "Aaliyah").where(is_admin: false)
```

### `or_where`

```ruby
Query.where(role: "admin").or_where(role: "user")
```

### `select`

```ruby
Query.select(["id", "name"])
```

### `limit`

```ruby
Query.where(name: "Usher").limit(10)
```

### `offset`

```ruby
Query.where(name: "Aretha").limit(10).offset(10)
```

### `order_by`

```ruby
Query.order_by("created_at DESC")
```

### `join`

```ruby
# SELECT * FROM users INNER JOIN user_tags ON user_tags.user_id = users.id
# WHERE user_tags.tag_name = ?
query = Query.join(:images).where("user_tags.tag_name = ?", "crystal")
Repo.all(User, query)
```

### `distinct`

```ruby
Query.distinct("users.name")
```

### `group_by`

```ruby
Query.where(name: "Charlize").join(:posts).group_by("users.id")
```

### `preload`

```ruby
Query.preload(:images)
```
