[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Build](https://github.com/querqy/chorus/actions/workflows/push/badge.svg)]
[![GitHub Actions](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Factions-badge.atrox.dev%chorus%2Fquerqy%2Fbadge&label=build&logo=none)](https://actions-badge.atrox.dev/atrox/sync-dotenv/goto)


<img src="assets/chorus-logo.png" alt="Chorus Logo" title="Chorus: Towards a open stack for ecommerce search" width="200" align="right"/>

Chorus
==========================

*Towards an open source tool stack for e-commerce search*

Chorus makes deploying powerful ecommerce search easier by shifting the buy vs build decision in favour of build, so you can own your search! It deals with three issues:

1. **Our collaboration stinks** Making holistic progress on search requires deep, cross-functional collaboration. Shooting emails or tracking search requirements in spreadsheets won't cut it.

2. ***Search testing is hard*** Search changes are cross-cutting: most changes will cause problems. Testing is difficult: you can't run hundreds of searches after every relevance change.

3. **Iterations are slow** Moving forward seems impossible. To avoid sliding backwards, progress is slow. Many simply give up on search, depriving users of the means to find critical information.


[Explore a demo](https://fivethirtyeight.datasettes.com/fivethirtyeight), watch [a video about the project](https://www.youtube.com/watch?v=aoWx7KJzvCs) or try it out by [running the quickstart.sh script](#5-minutes-to-run-chorus)

Want to stay up-to-date with the project? Subscribe to the [Datasette Weekly newsletter](https://datasette.substack.com/) for tips, tricks and news on what's new in the Datasette ecosystem.

## News

 * 17th June 2021: [Encores? - Going beyond matching and ranking of search results](https://2021.berlinbuzzwords.de/session/encores-going-beyond-matching-and-ranking-search-results) - Chorus is used to demo at BerlinBuzzwords.
 * 15th November 2020: [Chorus Workshop Series Announced](https://plainschwarz.com/ps-salon/) - Learn from the creators of the components of Chorus via six workshops.
 * 17th October 2020: [Chorus featured at ApacheCon @Home](https://www.youtube.com/watch?v=NGtmSbOoFjA) - René and Eric give a talk at ApacheCon on Chorus.
 * 10th June 2020: [Chorus Announced at BerlinBuzzwords](https://2020.berlinbuzzwords.de/session/towards-open-source-tool-stack-e-commerce-search) - First release of Chorus shared with the world at a workshop.



# What Runs Where

* Demo "Chorus Electronics" store runs at http://localhost:4000  |  http://chorus.dev.o19s.com:4000
* Solr runs at http://localhost:8983 |  http://chorus.dev.o19s.com:8983
* SMUI runs at http://localhost:9000 |  http://chorus.dev.o19s.com:9000
* Quepid runs at http://localhost:3000 |  http://chorus.dev.o19s.com:3000
* RRE runs at http://localhost:7979 |  http://chorus.dev.o19s.com:7979
* Prometheus runs at http://localhost:9090 |  http://chorus.dev.o19s.com:9090
* Grafana runs at http://localhost:9091 |  http://chorus.dev.o19s.com:9091

Working with macOS?   Pop open all the tuning related web pages:
> open http://localhost:4000 http://localhost:8983 http://localhost:9000 http://localhost:3000 http://localhost:7979


# 5 Minutes to Run Chorus!

We are trying to strike a balance between making the setup process as easy and fool proof as possible with the need to not _hide_ too much of the interactions between the projects that make up Chorus.

If you are impatient, we have a quick start script, `./quickstart.sh` that sets you up, however I recommend you go through [Kata 0: Setting up Chorus](katas/000_setting_up_chorus.md).   

After that, you can learn about how to use all the tools in Chorus to improve search by following these Katas:

1. First Kata: [Lets Optimize a Query](katas/001_optimize_a_query.md)
1. Second Kata: [How to Sell Search Keywords and Terms](katas/002_how_to_sell_search_keywords.md)
1. Kata 003: [Observability in Chorus](katas/003_observability_in_chorus.md)
1. Fourth Kata: [How to Gather Human Judgements](katas/004_gathering_human_judgements.md)
1. Fifth Kata: [Some days you just KNOW what the right products are for a query!](katas/005_curating_specific_products_for_a_query.md)

There is also a video series that is very closely related called [Meet Pete](https://opensourceconnections.com/blog/2020/07/07/meet-pete-the-e-commerce-search-product-manager/)



# Useful Commands for Chorus

To start your environment, i.e to do each step manually, run:
```
docker-compose up --build -d
```
Otherwise you can just run `./quickstart.sh`.  To include the observability features, run:

```
./quickstart.sh --with-observability
```

To see what is happening in the Chorus stack you can tail the logs for all the components via:
```
docker-compose logs -tf
```

If you want to narrow down to just one component of the Chorus stack do:
```
docker-compose ps                       # list out the names of the components
docker-compose logs -tf solr1 solr2     # tail solr1 and solr2 only
```

To reset your environment (including any volumes created like the mysql db), just run:
```
docker-compose down -v
```

If Docker is giving you a hard time then some options are:
```
docker system prune                     # removes orphaned images, networks, etc.
docker system prune -a --volumes        # removes all images, clears out your Docker diskspace if you full.
```

You may also have to [increase the resources](./assets/increase_docker_resources.gif) given to Docker, up to 4 GB RAM and 2 GB Swap space.


# Chorus Data Details

The Chorus project includes some public datasets.  These datasets let the community learn, experiment, and collaborate in a safe manner and are a key part of demonstrating how to build measurable and tunable ecommerce search with open source components.

The product data is gratefully sourced from [Icecat](https://icecat.biz/) and is licensed under their [Open Content License](https://iceclog.com/open-content-license-opl/).

The version of the Icecat data that Chorus provides has the following changes:
* Data converted to JSON format.
* Products that don't have a 500x500 pixel image listed are removed.
* Prices extracted for ~19,000 products from the https://www.upcitemdb.com/ service using EAN codes to match.

The ratings data (a.k.a explicit judgements) allows you to measure the impact of your changes to relevance.   We are profoundly grateful
to the team at [Supahands](http://www.supahands.com/) for voluntarily generating multiple ratings for the set of 125 representative ecommerce queries and
sharing that data with the Chorus community:
* [Broad_Query_Set_rated.csv](./katas/Broad_Query_Set_rated.csv) - Query/Doc/Rating set suitable for measuring experiments.
* [Broad_Query_Set_individual_ratings.csv](./katas/Broad_Query_Set_individual_ratings.csv) - Raw ratings generated by the three individual SupaAgents per query.

Learn more in [Kata 006: How to Use Explicit Judgements](./katas/something.md) about how you can work with Supahands to generate your human judgements.
