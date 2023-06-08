### Set up instructions

1. `npm install`
2. `npm run devStart` <- nodemon will reboot the server every time there is a change
3. Access GraphQL UI via `http://localhost:5000/graphql` (You need to refresh this when you make a change)

### Basic GraphQL Interactions

#### Queries
GraphQL assumes that anything not specified otherwise is a query, so 
`{
 books {
   name
 }
}`  

is the same as 

`query{
 books {
   name
 }
}`

### Mutations
You need to specify the action is a mutation, what mutation method you're calling, it's args, and what it returns once executed (lines 30 and 31 - name and id).

`mutation{
 addBook(name: "Harry Potter and the Half Blood Prince", authorId: 1) {
  name
  id
 }
}`



### Activities
This workshop is based off the tutorial [Learn GraphQL in 40 minutes](https://www.youtube.com/watch?v=ZQL7tL2S0oQ). If you get stuck, most of the solutions can be found at some point in that video.
1. Run a single query to get a list of all books with their id, name, and authorid
2. Discuss the following query do you think it will Run? Why or why not?
`{
  books {
  }
}
`
Run the query, and determine why it exhibited that behavior.

3. Run the following mutation and determine why you get an error:
`mutation{
 addBook(name: "Harry Potter and the Half Blood Prince", authorId: 1) {
 }
}`
4. Fix the above query, execute it, and then run a query to confirm the book has been added
5. Add the ability to get a list of all authors
6. Add the ability to add a new author and execute it (the mutation, but bonus points if you add the ability to execute an author)
7. Write a query to return all the authors names, and the books they have written
8. Write a query that finds the name of the book with the id of 1
From here on out is beyond what the tutorial walks through
9. Add a "publishedYear" field that you are able to query by, and is an optional field when adding a book
10. Add the ability to change the name of a specific book

This section is brought to you by ChatGPT. I haven't tried it, so proceed with caution lol

11. Introduce a new feature that allows books to be associated with one or more genres. Update the GraphQL schema and resolvers to include the new Genre type and create relationships between books and genres. Implement queries to fetch all genres and a single genre, as well as mutations to add genres to books. The goal is to provide a more comprehensive representation of books by incorporating genre information.

Tasks:

1. Define a new GraphQLObjectType called GenreType to represent a genre of a book. Include fields for id (GraphQLNonNull(GraphQLInt)) and name (GraphQLNonNull(GraphQLString)).
2. Add a genres field to the BookType to retrieve the genres associated with a book. The field should return a list of GenreType objects.
3. Implement a books field in the GenreType to fetch all books belonging to a specific genre. The field should return a list of BookType objects.
4. Extend the RootQueryType with a genres field to retrieve a list of all genres. Implement the resolver function to return the genres array.
5. Add a genre field to the RootQueryType to fetch a single genre based on its ID. Implement the resolver function to find and return the genre with the matching ID.
6. Expand the RootMutationType with a new mutation called addBook that allows adding genres to a book. Include the necessary arguments, such as name, authorId, and genreIds (a list of GraphQLNonNull(GraphQLInt)).
7. In the resolver for the addBook mutation, create a new book object with the provided data and push it to the books array. Ensure that the new book is associated with the specified genres.
8. Update the GraphQLSchema to include the GenreType, and assign the RootQueryType and RootMutationType to the corresponding query and mutation fields.
9. Test the new functionality by executing queries to fetch books and genres, as well as mutations to add genres to books. Verify that the associations between books and genres are accurate.