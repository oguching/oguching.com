The fact that I'm writing this post means I really need this service.

I've been wanting a place/tool/service/whatever that is like tumblr 
where I can post random stuff and have each item reachable from a url.
It has to be as easy to use as possible, if not I just won't use it. 
So going from idea to actual post should take as 
little steps as possible and should be pain-free.

* Posts will be written in markdown
* Posts have no title, no tags, no likes/hearts/favourites, no upvote/downvote
* Posts are displayed in reverse-chronological order
* slug will be something like blabber.ninja/posts/88888

It makes sense to store data in json. However, as I want to be lean I'm thinking,
why not just use json? For everything. No markdown, just json? So a new post would 
look something like 

```
    {
      "88888": {
        "post": "hello world"
      }        
    }
```

This can work can't it? 
But what if I want to include links in a post? Or a list?

I could just use harp for this since I have some experience with it but I don't want to.
I like harp a lot but I want something more barebones as much as possible.

All this is me just thinking out loud. 

Naturally it will be written in JavaScript, I'm not sure whether to go
client-side or server side for this yet but it will be one or the other.

You might ask why not just use tumblr or twitter?
Well, I want to build it myself. I want to host it. It's for me.