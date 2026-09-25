# Ent Essentials Cheat Sheet

```text
Schema
  ↓
Code Generation
  ↓
Generated Go API
  ↓
Queries / Mutations
  ↓
SQL Database
```

## Core Structure

Basic Ent project:
```text
ent/
├── schema/
│   ├── user.go
│   ├── post.go
│   └── profile.go
├── generate.go
└── entc.go

```

Schema:
```go
type User struct {
    ent.Schema
}

func (User) Fields() []ent.Field {
    return []ent.Field{
        field.String("name"),
        field.Int("age"),
    }
}

func (User) Edges() []ent.Edge {
    return []ent.Edge{}
}
```

Generate:
```bash
go generate ./ent
```

---

# Fields

Common field types:
```go
field.String("name")
field.Int("age")
field.Bool("active")

field.Int64("count")
field.Float64("score")

field.Time("created_at")

field.UUID("id", uuid.UUID{})

field.Bytes("data")

field.JSON("metadata", map[string]any{})
```

## Field Options
```go
field.String("name").Optional()
field.String("name").Unique()
field.String("name").Default("Anonymous")
field.Int("age").Default(0)
field.Time("created_at").Default(time.Now)
```

### Required vs Optional
```go
field.String("name")           // required
field.String("nickname").Optional()
```

Optional fields may be nullable depending on the generated schema/API.

---
# IDs

Ent entities have an ID by default.
Typical generated type:

```go
type User struct {
    ID   int
    Name string
    Age  int
}
```

Custom ID:
```go
field.UUID("id", uuid.UUID{})
```

---

# Edges / Relationships

### One-to-One

```go
edge.To("profile", Profile.Type).Unique()
```

Inverse:
```go
edge.From("user", User.Type).
    Ref("profile").
    Unique()
```

### One-to-Many
```go
edge.To("posts", Post.Type)
```

Inverse:
```go
edge.From("author", User.Type).
    Ref("posts").
    Unique()
```

### Many-to-Many
```go
edge.To("actors", Actor.Type)
```

Inverse:
```go
edge.From("movies", Movie.Type).
    Ref("actors")
```

### Relationship Model
```text
edge.To()
    ↓
defines the forward relationship

edge.From()
    ↓
defines the inverse side

Ref("...")
    ↓
points to the edge being mirrored

Unique()
    ↓
one related entity instead of many
```

---

# Create

Basic create:
```go
user, err := client.User.
    Create().
    SetName("Alice").
    SetAge(25).
    Save(ctx)
```

Multiple fields:
```go
client.User.
    Create().
    SetName("Alice").
    SetAge(25).
    SetActive(true).
    Save(ctx)
```

Create with edge:
```go
client.Post.
    Create().
    SetTitle("Hello").
    SetAuthor(user).
    Save(ctx)
```

---

# Update

Update one:
```go
client.User.
    UpdateOne(user).
    SetName("Bob").
    Save(ctx)
```

Update by ID:
```go
client.User.
    UpdateOneID(id).
    SetName("Bob").
    Save(ctx)
```

Update many:
```go
client.User.
    Update().
    Where(user.AgeGT(18)).
    SetActive(true).
    Save(ctx)
```

---

# Delete

Delete one:
```go
client.User.
    DeleteOne(user).
    Exec(ctx)
```

Delete by ID:
```go
client.User.
    DeleteOneID(id).
    Exec(ctx)
```

Delete many:
```go
client.User.
    Delete().
    Where(user.Active(false)).
    Exec(ctx)
```

---

# Query

Query all:
```go
users, err := client.User.
    Query().
    All(ctx)
```

Get one:
```go
user, err := client.User.
    Query().
    Where(user.ID(id)).
    Only(ctx)
```

First:
```go
user, err := client.User.
    Query().
    First(ctx)
```

Count:
```go
count, err := client.User.
    Query().
    Count(ctx)
```

Existence:
```go
exists, err := client.User.
    Query().
    Exist(ctx)
```

---

# Predicates

Equality:
```go
user.NameEQ("Alice")
user.IDEQ(10)
```

Inequality:
```go
user.AgeNEQ(18)
```

Comparisons:
```go
user.AgeGT(18)
user.AgeGTE(18)
user.AgeLT(18)
user.AgeLTE(18)
```

String matching:
```go
user.NameContains("ali")
user.NameHasPrefix("Al")
user.NameHasSuffix("ce")
```

Negation:
```go
user.Not(user.ActiveEQ(false))
```

Multiple predicates:
```go
client.User.
    Query().
    Where(
        user.AgeGT(18),
        user.ActiveEQ(true),
    ).
    All(ctx)
```

Conceptually:
```text
multiple Where predicates
        ↓
       AND
```

OR:
```go
user.Or(
    user.AgeLT(18),
    user.AgeGT(65),
)
```

---

# Query Through Relationships

Users with posts:
```go
client.User.
    Query().
    Where(
        user.HasPosts(),
    ).
    All(ctx)
```

Users with a specific related entity:
```go
user.HasPostsWith(
    post.TitleEQ("Hello"),
)
```

Posts belonging to an author:
```go
client.Post.
    Query().
    Where(
        post.HasAuthorWith(
            user.NameEQ("Alice"),
        ),
    ).
    All(ctx)
```

---

# Traversing Edges

From User → Posts:
```go
posts, err := user.
    QueryPosts().
    All(ctx)
```

From Post → Author:
```go
author, err := post.
    QueryAuthor().
    Only(ctx)
```

From Movie → Actors:
```go
actors, err := movie.
    QueryActors().
    All(ctx)
```

---

# Eager Loading

Load relationships together with the entity:
```go
users, err := client.User.
    Query().
    WithPosts().
    All(ctx)
```

Nested eager loading:
```go
client.User.
    Query().
    WithPosts(func(q *ent.PostQuery) {
        q.WithAuthor()
    }).
    All(ctx)
```

model:
```text
Query User
   │
   ├── User data
   │
   └── Posts
        │
        └── Author
```

Useful for avoiding repeated relationship queries.

---

# Select Specific Fields
```go
client.User.
    Query().
    Select(
        user.FieldID,
        user.FieldName,
    ).
    All(ctx)
```

---

# Ordering

Ascending:
```go
user.ByName()
```

Descending:
```go
user.ByAge(sql.OrderDesc())
```

Multiple ordering expressions:
```go
user.ByName(),
user.ByAge(),
```

---

# Pagination

Offset:
```go
client.User.
    Query().
    Offset(20).
    Limit(10).
    All(ctx)
```

Conceptually:
```text
Offset(20)
    ↓
skip first 20

Limit(10)
    ↓
return next 10
```

---

#  Limit
```go
client.User.
    Query().
    Limit(10).
    All(ctx)
```

---

#  Unique Queries

Exactly one expected:
```go
user, err := client.User.
    Query().
    Where(user.IDEQ(id)).
    Only(ctx)
```

Possible errors include:
```text
NotFound
MultipleObjects
```

First matching entity:
```go
First(ctx)
```

---

# Aggregation

Count:
```go
client.User.
    Query().
    Count(ctx)
```

Common SQL-style operations can be expressed through Ent's query/aggregation APIs.
Conceptually:
```text
COUNT
SUM
AVG
MIN
MAX
GROUP BY
```

---

#  Upsert / Conflict Handling

Create with conflict handling:
```go
client.User.
    Create().
    SetName("Alice").
    OnConflict().
    UpdateNewValues().
    Save(ctx)
```

Useful for:
```text
INSERT
    ↓
conflict?
    ├── no  → insert
    └── yes → update
```

---

# Edge Mutations

Add related entities:
```go
client.User.
    UpdateOne(user).
    AddPosts(post1, post2).
    Save(ctx)
```

Set one-to-one:
```go
client.User.
    UpdateOne(user).
    SetProfile(profile).
    Save(ctx)
```

Remove:
```go
client.User.
    UpdateOne(user).
    RemovePosts(post).
    Save(ctx)
```

Clear:
```go
client.User.
    UpdateOne(user).
    ClearPosts().
    Save(ctx)
```

---

#  Query Builder Model

Ent queries are composable:
```go
users, err := client.User.
    Query().
    Where(
        user.AgeGTE(18),
        user.ActiveEQ(true),
    ).
    WithPosts().
    Order(
        user.ByName(),
    ).
    Limit(20).
    All(ctx)
```

---

# Database Connection

Typical client:
```go
client, err := ent.Open(
    "sqlite3",
    "file:ent.db?cache=shared&_fk=1",
)
```

Other database drivers commonly used with Ent include:
```text
SQLite
PostgreSQL
MySQL
Gremlin
```

Close:
```go
defer client.Close()
```

---

# 🏗️ Schema Migration

Development migration:
```go
client.Schema.Create(ctx)
```

Schema migration:
```text
Go Schema
    ↓
Ent Migration
    ↓
Database Schema
```

Ent can also generate migration files for version-controlled migration workflows.

---

# 🔄 Transactions

Start:
```go
tx, err := client.Tx(ctx)
```

Use transactional client:
```go
user, err := tx.User.
    Create().
    SetName("Alice").
    Save(ctx)
```

Commit:
```go
tx.Commit()
```

Rollback:
```go
tx.Rollback()
```

Mental model:
```text
Begin
  ↓
operation 1
  ↓
operation 2
  ↓
operation 3
  ↓
Commit
```

If something fails:
```text
Begin
  ↓
operation
  ↓
ERROR
  ↓
Rollback
```

---

# Debugging SQL

Enable query logging when debugging:
```go
client = client.Debug()
```

Useful for seeing the SQL generated by Ent.

---

# Generated API Mental Model

If you define:
```go
type User struct {
    ent.Schema
}
```

Ent generates a family of APIs around it:
```text
User
│
├── UserClient
│
├── UserQuery
│
├── UserCreate
│
├── UserUpdate
│
├── UserDelete
│
├── UserMutation
│
└── UserWhereInput / predicates
```

So:
```go
client.User.Query()
```

means:

> build a User query.

```go
client.User.Create()
```

means:

> build a User insertion.

```go
client.User.Update()
```

means:

> build a User update.

```go
client.User.Delete()
```

means:

> build a User deletion.

---

# Ent Vocabulary

|Term|Meaning|
|---|---|
|**Schema**|Go definition of an entity|
|**Entity**|A modeled database object|
|**Field**|Column/property of an entity|
|**Edge**|Relationship between entities|
|**Predicate**|Query condition|
|**Query Builder**|API for constructing queries|
|**Mutation**|Insert/update/delete operation|
|**Eager Loading**|Loading related entities with the query|
|**Traversal**|Querying through relationships|
|**Generated Code**|Go API produced from schemas|
|**Migration**|Synchronizing database structure with schema|
|**Transaction**|Group of database operations committed atomically|

---

# 80/20

The APIs you'll reach for constantly:

```go
// Create
client.User.Create().
    SetName("Alice").
    Save(ctx)

// Query
client.User.Query().
    Where(user.NameEQ("Alice")).
    All(ctx)

// Update
client.User.UpdateOne(user).
    SetName("Bob").
    Save(ctx)

// Delete
client.User.DeleteOne(user).
    Exec(ctx)

// Relationships
user.QueryPosts().All(ctx)

// Eager loading
client.User.Query().
    WithPosts().
    All(ctx)

// Relationship filtering
client.User.Query().
    Where(user.HasPostsWith(
        post.TitleContains("Go"),
    )).
    All(ctx)

// Transaction
tx, err := client.Tx(ctx)
```

## 🕸️ The Ent Mental Model

```text
                  ENT
                   │
             ┌─────┴─────┐
             │   Schema  │
             └─────┬─────┘
                   │
            code generation
                   │
                   ▼
        ┌─────────────────────┐
        │    Generated API    │
        └──────────┬──────────┘
                   │
       ┌───────────┼───────────┐
       ▼           ▼           ▼
     Query       Create      Update
       │           │           │
       └───────────┼───────────┘
                   ▼
              Relationships
                   │
                   ▼
               Database
```

### The shortest version

```text
Schema  → define data
Field   → define columns
Edge    → define relationships
Query   → read
Create  → insert
Update  → modify
Delete  → remove
Where   → filter
With    → eager load
QueryX  → traverse relationship
Tx      → transaction
Migrate → database schema
```