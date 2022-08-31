# Poke API Tech Demo

I wrote this application as a small demonstration for an interview for Radius Payment Solutions to act as a brief showcase of some of the skills I have. Naturally it doesn't cover everything, but I've aimed to tick a few things of the job requirements list. Namely:

- .Net 4.7 (Although this is written in 4.8).
- C#.
- SQL Knowledge.
	- Knowledge of relational databases.
- REST.


# What does this application do?
This application takes the search text you use and makes a web request to the PokeAPI (https://pokeapi.co/). Strictly speaking this only makes GET requests, but it's a fun little tool nonetheless. Read on for some of the ins and outs.

It's written in .NET Framework 4.8, for the simple reason that I *love* Rider by JetBrains, and they've not given us Winforms previewing for .NET Core (6.0). This could however, be rewritten in Core by using WPF

## Data Access
This application has a small SQLite cache built in, the idea being we can prevent calls to the web API if you've already retrieved the data recently. In this case if the data is in cache, and it's less than 10 minutes old, it'll display that data instead

In this example all the data access is provided using raw SQL. This is to demonstrate an ability to put together queries in a concise and safe manner. Every query uses a **prepared statement** making the queries safe in that it protects against injection, but also: easy to locate and edit! (Amazing if another developer needs to change the query).

The data logic is stored in a repository class, this means I can implement an interface here and easily unit test the business logic in the service class higher up if necessary. It also means I could go a little further and look to implement the repository pattern, but as this is a single data table for a small cache, it's not strictly needed here.

## Improvements

No application is perfect, especially this one as it was written fairly quickly to highlight a skillset. Here's some ways it can be improved further:

- For persistent data I'd like to use Postgres. Primarily because postgres has baked in datetime and JSON blob support.
	- Let's go further! Postgres could handle a larger scale cache to exist more of an audit and then a Redis layer could be implemented on top to allow super fast cache retrieval.
- SPA - This could easily be implemented as an SPA, currently as a windows application it's rather limited but rewriting it as an SPA would make the application work on any number of platforms. It could even be wrapped with an electron shell and run on the desktop that way.
