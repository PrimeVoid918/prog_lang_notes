| Relationship Type                  | Side A Schema (The Owner)                   | Side B Schema (The Mirror / Inverse)                      | Database Impact (SQL Layer)                         |
| ---------------------------------- | ------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------- |
| **1:1 Unidirectional** _(One-way)_ | `edge.To("profile", Profile.Type).Unique()` | _None (Side B doesn't know about Side A)_                 | Foreign Key column added to the `Profile` table.    |
| **1:1 Bidirectional** _(Two-way)_  | `edge.To("profile", Profile.Type).Unique()` | `edge.From("user", User.Type).Ref("profile").Unique()`    | Foreign Key column added to the `Profile` table.    |
| **1:Many Unidirectional**          | `edge.To("comments", Comment.Type)`         | _None (Side B doesn't know about Side A)_                 | Foreign Key column added to the `Comment` table.    |
| **1:Many Bidirectional**           | `edge.To("comments", Comment.Type)`         | `edge.From("author", User.Type).Ref("comments").Unique()` | Foreign Key column added to the `Comment` table.    |
| **Many:Many Unidirectional**       | `edge.To("tags", Tag.Type)`                 | _None (Side B doesn't know about Side A)_                 | A hidden join table is created (e.g., `post_tags`). |
| **Many:Many Bidirectional**        | `edge.To("tags", Tag.Type)`                 | `edge.From("posts", Post.Type).Ref("tags")`               | A hidden join table is created (e.g., `post_tags`). |

---
### One-to-One (1:1) Bidirectional
Scenario: A User has one Profile; a Profile belongs to one User.
```go
// ent/schema/user.go
func (User) Edges() []ent.Edge {
    return []ent.Edge{
        edge.To("profile", Profile.Type).Unique(),
    }
}

// ent/schema/profile.go
func (Profile) Edges() []ent.Edge {
    return []ent.Edge{
        edge.From("user", User.Type).Ref("profile").Unique(),
    }
}

```
**Generated Go Methods Available:**
- **Mutation**: `client.User.Create().SetProfile(p).Save(ctx)` or `client.Profile.Create().SetUser(u).Save(ctx)`
- **Eager Load**: `client.User.Query().WithProfile().All(ctx)`
- **Traverse**: `u.QueryProfile().Only(ctx)` or `p.QueryUser().Only(ctx)`

### One-to-Many (1:M) Bidirectional
Scenario: A User can write many Posts; a Post belongs to exactly one Author.
```go
// ent/schema/user.go
func (User) Edges() []ent.Edge {
    return []ent.Edge{
        edge.To("posts", Post.Type), // Plural, no .Unique()
    }
}

// ent/schema/post.go
func (Post) Edges() []ent.Edge {
    return []ent.Edge{
        edge.From("author", User.Type).Ref("posts").Unique(), // Singular, has .Unique()
    }
}

```
**Generated Go Methods Available:**
- **Mutation**: `client.User.UpdateOne(u).AddPosts(p1, p2).Save(ctx)` or `client.Post.Create().SetAuthor(u).Save(ctx)`
- **Eager Load**: `client.User.Query().WithPosts().All(ctx)`
- **Traverse**: `u.QueryPosts().All(ctx)` or `p.QueryAuthor().Only(ctx)`

### Many-to-Many (M:M) Bidirectional
Scenario: A Movie can have many Actors; an Actor can star in many Movies.
```go
// ent/schema/movie.go
func (Movie) Edges() []ent.Edge {
    return []ent.Edge{
        edge.To("actors", Actor.Type), // Plural, no .Unique()
    }
}

// ent/schema/actor.go
func (Actor) Edges() []ent.Edge {
    return []ent.Edge{
        edge.From("movies", Movie.Type).Ref("actors"), // Plural, no .Unique()
    }
}
```
**Generated Go Methods Available:**
- **Mutation**: `client.Movie.UpdateOne(m).AddActors(a1, a2).Save(ctx)` or `client.Movie.UpdateOne(m).RemoveActors(a1).Save(ctx)`
- **Eager Load**: `client.Movie.Query().WithActors().All(ctx)`
- **Traverse**: `m.QueryActors().All(ctx)` or `a.QueryMovies().All(ctx)`