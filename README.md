# social_network_system_design
System Design for travel-oriented Social Network

## Functional requirements:
- Ability to publish posts, containing photo carousel, short text description and geographical tag. (CreatePost)
- Ability to comment on user posts (CreateComment)
- Ability to add reactions to other users' posts (like, dislike). (CreateReaction)
- Ability to subscribe to other users' updates. (CreateSubscription)
- Ability to search for popular places and view tagged posts. (Search)
- Ability to browse personal feed. (ViewFeed)

## Non-functional requirements:
- Network is expected to grow linearly from 0 to 10 000 000 DAU first year, further growth is expected, but not outlined.
- Target region is CIS with no plans for global expansion.
- Availability 99,95%
- Target platforms: desktop browsers, mobile apps.
- User behavior (on average):
  - 5 posts per month, each post contains 2 photos and a 10-word description with geographical tag;
  - 5 comments per month;
  - 15 reactions per month;
  - 3 new subscriptions per month;
  - 1 popular place search per month;
  - 10 posts per day viewed on personal feed. One feed request = 5 posts on page.
- Geo distribution not needed (CIS region only).
- Traffic surges expected on seasonal holidays (Christmas, New Year's Eve etc.)

## Basic calculations:
CreatePost:
```
RPS (average) = 10 000 000 / 6 / 86400 = 20
Traffic (average) = 20 RPS * (2 photos * 2 MB + 10 * 5) = 80MB/s
```

CreateComment:
```
RPS (average) = 10 000 000 / 6 / 86400 = 20
Traffic (average) = 20 RPS * 20 byte  = 0.4 KB/s
```

CreateReaction:
```
RPS (average) = 10 000 000 / 2 / 86400 = 60
Traffic (average) = 60 RPS * 4 byte = 0.25 KB/s
```

CreateSubscription:
```
RPS (average) = 10 000 000 / 10 / 86400 = 12
Traffic (average) = 12 RPS * 8 byte = 0.1 KB/s
```

Search:
```
RPS (average) = 10 000 000 / 30 / 86400 = 4
Traffic (average) = 4 RPS * 2 MB (featured photo) * 10 items on page = 80 MB/s
```

ViewFeed:
```
RPS (average) = 10 000 000 * 2 (feed requests) / 86400 = 230
Traffic (average) = 230 RPS * (5 posts * 2 photos * 2 MB) = 4.6 GB/s
```



