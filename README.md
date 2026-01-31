# CLI E-Commerce Search (Mini Amazon)

A command-line e-commerce prototype built in C++.  
Supports keyword search (AND/OR), shopping cart operations, and checkout with inventory + balance validation.

## Features

### Keyword Search (AND / OR)
- Builds an inverted index: `keyword -> set<Product*>`
- Supports multi-term search:
  - `AND term1 term2 ...` (set intersection)
  - `OR term1 term2 ...` (set union)

### Shopping Cart
- `ADD username hit_index` — add a searched item to a user cart
- `VIEWCART username` — display cart items
- `BUYCART username` — purchase eligible items:
  - item must be in stock
  - user must have enough balance
  - successful purchases deduct balance + decrement qty and remove from cart

### Product Types
- Book (name + author + ISBN)
- Clothing (name + brand + size)
- Movie (name + genre + rating)

## Project Structure
- `amazon.cpp` — main CLI loop and command parsing
- `mydatastore.*` — DataStore implementation (index + users + carts)
- `product.*` + `book.*` `clothing.*` `movie.*` — product polymorphism and keyword extraction
- `util.*` — tokenization + set union/intersection utilities
- `db_parser.*`, `product_parser.*` — database parsing

## Build & Run
```bash
make
./amazon database.txt
```

### Example Commands
```txt
AND harry potter
OR nike shoes
ADD alice 1
VIEWCART alice
BUYCART alice
QUIT outdb.txt
```

