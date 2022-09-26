---
title: "357[0] = \"The idea 💡\" "
date: 2022-09-26T10:22:25+02:00
draft: false
---

## Intro

Back in the days - believe it or not - there was no YouTube, Spotify, Shazam, etc. 

Your only chance to find out "What's that great song you've just heard  on the radio was?" was:
- host said it's name after it was played, 
- you remembered the name when host it before it was played,
- you were with a friend that knew this song title and author

It was in the end of 80's, when tuners with digital screens become available on the market and radio stations started to transmit song authors and titles via radio waves. Since then, it became sort of a standard to publish such info. 

When internet audio streams started to be a thing, a bunch of smart people came up with an idea to add metadata to the stream. This is called ICY (I see why - I wonder if this was intended, but it actually is an acronim for `I Can Yell`) and you can learn more from this [doc site](https://cast.readme.io/docs/icy) or read this [ICT TL;DR]({{< ref "00-the-idea.md#icy-tldr" >}}). 

## Idea

Two years ago, I came up with an idea for a project: create a piece of software that would collect data about songs played in internet radio station called [Radio 357](https://radio357.pl/).

Back then, the site would only display the current song within it's player. Later on, some of the hosts or even listeners would create playlist on Spotify with songs that were played on air.

Having in mind that being first doesn't always determine who is gonna win the market and that the best product can win, I decided to work on the project again. And this actually means: **I'm starting from scratch.**

## The Goal

There are a few of them and they are on different levels ranging from those that are targeted at users to those that are target towards self development. It's gonna be challenging, but here is a list (checkboxes will be checked once the goal will be reached):

### Collecting the data
- [x] stream parser that would extract author and title
- [x] saving played song to the database
- [x] saving info when the song was played
- [ ] scraping program plan for the next day
- [ ] finding played songs on platforms:
  - [ ] Spotify
  - [ ] YouTube
  - [ ] Apple Music
  - [ ] Tidal

### Playlists
- [ ] creating playlist for different parts of the day: night, morning, afternoon and evening on platforms:
  - [x] Spotify
  - [ ] YouTube
  - [ ] Apple Music
  - [ ] Tidal
- [ ] creating playlist for each program based on scraped data
- [ ] adding songs that were played to the correct playlist

### UI
- [ ] publicly available site that would display:
  - [ ] recently played songs
  - [ ] links to them on various platforms
- [ ] analytics:
  - [ ] create report about the authors and songs played
  - [ ] live metrics of songs and authors popularity within the given period of time

### API
- [ ] allow users to filter songs by play date, time, datetime, program it was played on, authors, titles
- [ ] allow users to filter playlists with specific authors, titles or programs they're linked to

### Non functional goals
- [ ] learn asyncio - async programming
- [ ] learn Azure
  - [ ] CosmosDB
  - [ ] Azure Service Bus
  - [ ] Azure Functions with bindings
  - [ ] Azure Durable Functions
- [ ] learn APIs
  - [ ] Spotify
  - [ ] YouTube
  - [ ] Apple Music
  - [ ] Tidal
- [ ] learn CloudEvents schema
- [ ] migrate to DAPR


## Roadmap

This is the most difficult part. I think I can tell you what is the order of my focus, but because of the day-tp-day job and uni during the weekend, I can't even predict the time frame. This part of the article will be like a journal with two informations: what's done and what's next.

### [2022-09-26]
The most important thing is working already and that is data parser and song saver. I'm collecting the data since `2022-09-22T13:59:01.210309` to be exact and the first saved song was [`Colin James - Leave This House`](https://open.spotify.com/track/3EXwHbECDsXgl0M9iZcfhP?si=f98f997b30384366). Not a bad start, huh?

Next steps:


## The next next steps

I can't predict where this project will lead me, but I can imagine adding support for other radio stations and analytics on cumulative data. Maybe one day, someone will perform a real analytics on this data to see what were the sentiments during specific period of time. 

That's the thing - if you have the data you can try to diagnose current state of something or predict what could happen, but without the data it's all just assumptions. 

Someone has to do the work and collect it. Unfortunetly, that's me! 

---
### ICY TL;DR

Stream is sent via HTTP protocol. When sending a `GET` request to connect to the stream, you just have to include `Icy-MetaData: 1` in your request headers. What you'll receive in response is a header `icy-metaint` which will tell you how much bytes does metadata take and - of course - the actual data that will be later transformed into sound. All you have to do is to collect all the meta data, do a simple regex to find something that would match `StreamTitle='<something here>';` and voila: here is your author and song title.