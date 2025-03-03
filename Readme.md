# MongoDB Fundamentals Assignment



## Database and Collection Creation
```javascript
// Connect to MongoDB and create the 'library' database
use library;

// Create the 'books' collection and insert data
db.books.insertMany([
    { title: "The Great Gatsby", author: "F. Scott Fitzgerald", publishedYear: 1925, genre: "Fiction", ISBN: "9780743273565" },
    { title: "To Kill a Mockingbird", author: "Harper Lee", publishedYear: 1960, genre: "Fiction", ISBN: "9780061120084" },
    { title: "1984", author: "George Orwell", publishedYear: 1949, genre: "Dystopian", ISBN: "9780451524935" },
    { title: "The Da Vinci Code", author: "Dan Brown", publishedYear: 2003, genre: "Mystery", ISBN: "9780385504201" },
    { title: "Harry Potter and the Sorcerer's Stone", author: "J.K. Rowling", publishedYear: 1997, genre: "Fantasy", ISBN: "9780439708180" }
]);
```

## Retrieve Data
```javascript
// Retrieve all books
db.books.find();

// Query books by a specific author
db.books.find({ author: "George Orwell" });

// Find books published after 2000
db.books.find({ publishedYear: { $gt: 2000 } });
```

## Update Data
```javascript
// Update the publishedYear of a specific book
db.books.updateOne(
    { ISBN: "9780385504201" },
    { $set: { publishedYear: 2005 } }
);

// Add a new field 'rating' to all books
db.books.updateMany(
    {},
    { $set: { rating: 5 } }
);
```

## Delete Data
```javascript
// Delete a book by ISBN
db.books.deleteOne({ ISBN: "9780451524935" });

// Remove all books of a particular genre
db.books.deleteMany({ genre: "Fiction" });
```

## Data Modeling for E-Commerce Platform
### Collections:
1. **Users**
   ```javascript
   db.users.insertOne({
       userId: 1,
       name: "John Doe",
       email: "john@example.com",
       address: "123 Main St",
       orders: []
   });
   ```
2. **Products**
   ```javascript
   db.products.insertOne({
       productId: 101,
       name: "Laptop",
       price: 999.99,
       stock: 10
   });
   ```
3. **Orders**
   ```javascript
   db.orders.insertOne({
       orderId: 5001,
       userId: 1,
       products: [{ productId: 101, quantity: 1 }],
       status: "Shipped"
   });
   ```

## Aggregation Pipeline
```javascript
// Count books per genre
db.books.aggregate([
    { $group: { _id: "$genre", totalBooks: { $sum: 1 } } }
]);

// Calculate the average published year
db.books.aggregate([
    { $group: { _id: null, avgPublishedYear: { $avg: "$publishedYear" } } }
]);

// Identify the top-rated book
db.books.find().sort({ rating: -1 }).limit(1);
```

## Indexing
```javascript
// Create an index on the 'author' field
db.books.createIndex({ author: 1 });
```