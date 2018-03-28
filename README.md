# top_1000_imdb_movies_search
Simple Search for the Top 1000 imdb movies using an in-memory graph data store.

Search movies with any number of Actors, Directors, Writers, Production Co's and/or Genre's. (eg. Brad Pitt & crime).

Scraper class crawls the Top 1000 movies listings (http://www.imdb.com/search/title?groups=top_1000&sort=user_rating&view=simple&page=1&ref_=adv_nxt) and each movie details pages. 

The crawled data is stored in Graph instance as (movie_detail, movie_title) in defaultdict(set) to easily access the movies by their movie detail.

Search launches shell to lookup movies by movie details.

Simplifying Assumptions:
- Search for the exact value. To quickly lookup data in the graph (hash implementation), the search requires you type in the exact name of the actor, genre, director, etc.
- Each movie detail in search query must be separated with a '&'. This allows us to easily search through multiple movie details as opposed to if we were to separate each detail with a space.
- The underlying graph datastore allows us to connect movie details (genres, actors, etc.) to a specific movie while allowing us to grab multiple movies via simple set operations.

Future Improvements:
- Support asynchronous requests. Currently all the requests arer synchronous, so that is about 20 requests for the top 1000 movies listings and then another 1000 requests, one for each movie detail page. To speed this up, I would use something like 'aiohttp' and 'asyncio' to allow for asynchronous request calls.
- Possibly utilize backend data store to handle even more movies.
- If we were to rank by relevance, we can also crawl movie details and concatenate every detail to a document for each page. Use TF-IDF or similar to index and rank page based on search query.
