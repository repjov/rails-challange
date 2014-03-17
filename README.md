# Ruby on Rails Challenge
In order to be considered for the Ruby on Rails position, you must complete the task below. This challenge will demonstrate your abilities with the framework, testing, APIs, and frontend design.

*Note: This task should take no longer than 6-8hours at most to complete.*

## Description

Your task is to scaffold a Ruby on Rails 4 application. This application will have users, books, publishers.
App can crawl for and create books from [GOOGLE BOOK API](https://developers.google.com/books/docs/v1/using?hl=ru)'s and  display them, users will able to choose and mark books as favorite.


## Tasks

To begin, fork this repository.

### 1. Setup

Fork this repository and create a `source` directory. Within the `source` directory, create a new Rails 4 application. Please use SQLite as the database technology.

### 2. Scaffold Models

The `Book` model should mimic the JSON data structure below:

```json
{
"id": 1,
"publisher_id": 2,
"title": "Beginning Ruby on Rails",
"description": "Ruby on Rails is the revolutionary online programming tool that makes creating functional e-commerce web...",
"url": "http://books.google.ru/books?id=BaWayIR0CvkC&hl=&source=gbs_api",
"published_date": "2006-11-29",
"image_link": "http://bks9.books.google.ru/books?id=BaWayIR0CvkC&printsec=frontcover&img=1&zoom=1&edge=curl&imgtk=AFLRE726J7ch0lrziOh1Q_cFWCTXww4MjI0jjlQLdAu39_4Y2Xl2rI1xBol8R6kkhnuFqR3cgKaWcmr0X9iFlIEzX9FqVw4Rifm0Ibp4pNnhT60lsJRLn4w&source=gbs_api",
"page_count": 306,
"authors": "Steve Holzner, Ph.D.",
"language": "EN",
"rating": 3.5
}
```

while for the `Publisher` model:

```json
{
"id": 2,
"name": "John Wiley & Sons"
}
```

in which an `Book` belongs to a `Publisher`. You are free to add any additional attributes that you need.

### 3. Crawl API for Books

Implement a rake task within the `Book` model to crawl for and create books. The API endpoint and request parameters you will be using is:

```
https://www.googleapis.com/books/v1/volumes?q=ruby%20on%20rails&maxResults=40
```

Use your best judgement to translate the API fields into `Book` fields. For example, the API field `averageRating` is probably best for `rating`. The `Publisher` association should be created from the API fields `publisher`. Also, crawling should be idempotent. That is, crawling the API multiple times should **not** create duplicate books.


### 4. Users Types
There will be 3 types of users

1. Admin can add/edit/delete and populate books from API
2. Logged users can mark books as favorite
3. Not logged users can only see books


### 5. Build Interface

You can use Bootstrap(http://getbootstrap.com/) as main style.

1) Sign Up `/signup` *(available for all users)*

Fields:
 - first Name
 - last Name
 - email
 - password
 - confirm password

Fields must be validate. First name, Last name, Emails, password must be required, password and confirm password must be the same, password should contain letters and numbers and should be at least 6 symbols.


2) Sign In pages `/signin` *(available for all users)*

Fields:
 - email
 - password
 
Sing Up and Sign In should not be avilable for logged user.


3) Books `/books` *(available for all users)*

Here will be a List of books:

*image, title, description, published date, publisher, page count*

Logged users will able mark/unmark any book as favorite and they will be available on `/favorite` page.  Favorite page will be available only for logged user.


***Other all needed page(such as admin side where admin can add/edit/remove books and etc.) you should do yourself, you can use standard rails scaffolding***


### 6. Write RSpec Tests

**Unit Tests**

1. It should crawl the API and create books in the database.
2. It should be able to crawl the API multiple times and not create duplicate books.
3. It should check routers for logged and not logged users
4. It should check regisration
5. it should check auth metods
6. it should check favorite book stuff

**Integration Tests**

1. It should Regisrate new user, login as new user, go to books page, click on 'make favorite' button, and should added new favorite book on favorite page. Remove from favorite should remove from list of favorite books.

## Submission

Commit and push code to your forked repository and then send us a pull request with your name in the title. We'll then review your code and get back to you!


### Gems which can be useful
- http://rubygems.org/gems/devise
- http://rubygems.org/gems/rspec
- http://rubygems.org/gems/capybara
- http://rubygems.org/gems/database_cleaner
