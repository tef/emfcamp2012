..
    draft script for a talk at scottish ruby fringe 2012.
    
    running time 40 minutes
    
    a talk on web-like approach to rpc, for ruby and python.
    
    section titles won't be read out loud, may appear
    on slides.

hypermedia-rpc, or how I learned to love rest
=============================================
..
    introduction: 
    me, learning ruby
    day job, github, travis
    hyperglyph is ducked type web stuff
    worksforme

SLIDE::

    *blank -or- talk title*

.. 
    perhaps put a parody dr-strangelove title,
    perhaps section titles in same style.

hi, my name is tef, and I am a python programmer.

SLIDE::

    @tef

(don't tell anyone, but i've been learning ruby while no-one's been looking)

python is my day job, and my day job involves getting computers to talk to
each other. there are many names and styles for this, but mostly, they suck.

I wrote some code to handle the suck for me, and I got paid for doing it too.

*aside*
    Now when I say rpc, I really mean client-server. RPC is a pretty overloaded term, 
    but I just mean 'I call a function over here, and get a function over there',
    at a very primitive level. 

hyperglyph isn't like other rpc systems - it doesn't require code
generation, it's duck typed, and it plays nicely with http. 
it does this by being a lot more like a web site than a web service. 




Work also have me their blessing to release it, and I'm porting it to ruby for fun.

It's called hyperglyph, and it is on github, and travis runs tests in both ruby and python.

it's made my job suck less, and I hope it can make your job suck less too.

SLIDE::

    http://hyperglyph.net


Before I begin my story, I'd like to take this moment to thank my employer 
for letting me release this code, as well as github and travis. You're all neat.

-1min

nobody knows the trouble i've seen
----------------------------------

..
    day job is terrible
    rpc i.e client-server
    what life wihout rpc looks like
    duck typing is nice

SLIDE::

    *blank*


My day job is writing distributed software, a bit like googlebot, to crawl the web. 

My day job involved writing remote procedure calls. 

My day job sucked.


I had some worker processes across a machine pool, and some process to manage
their tasks. I'm simplifying, but a worker needs to fetch a task, crawl it for links,
report them and move onto the next task.

If *I* was doing it without RPC, all on the same machine, it would probably look a lot like this:

SLIDE::

    def process(queue):
        task = queue.next_task()
        for url in crawl(task.url):
            task.found_link(url)
        task.complete()

If *you* were doing it without RPC, it would probably look a lot more like this:

SLIDE::

    def process(queue)
      task = queue.next_task
      crawl(task.url).each do |url|
        task.found_link(url)
      end
      task.complete
    end

*aside*
    The ruby examples are works in progress. I hope you'll prefer an idea
    of where I'm going in ruby, rather than where I've gone with python.

As you can see we just call methods, get back objects and call more methods. 
It sounded nice in theory, but practice had a lot to answer for.

SLIDE::
    blank

HTTP. It's good for you
-----------------------

..
    ugly truth of POST+json
    other choices and nightmares
    http, and http intermediataries
    still ugly

What we started with with looked a lot more like this:
+3min

SLIDE::

    def process
      
      task = http.POST(@next_task_url, {worker:@worker_id)

      crawl(task['url']).each do |url|
        http.POST(@found_link_url, {worker:@worker_id, id:task['id'], url:url})

      end
      http.POST(@complete_url, {worker:@worker_id, id:task['id']})
    end

Lovely, isnt it? 

As you can see, we picked http, out of a number of other approaches, including zeromq, irc, 
tcp, soap, and amqp. 

Message queues are nice when things work, but we'd had some terrible
experiences with failure handling. We didn't know zeromq, and we didn't
use irc because we aren't writing a botnet.

SOAP on the other hand, 

SOAP, well.

I still get flashbacks.

I still have nightmares.

*aside*
    I recently heard of a SOAP api where the responses were json
    embedded in strings.

    THE S STANDS FOR SIMPLE

This lead to the obvious conclusion, http. our one true love.

+4min

HTTP may not be the best protocol in the world, but it has 
things like load balancers, proxies, and caches.  one of the
defining features of HTTP is that it is a layered system - 
very few protocols offer such a plethora of tools,
let alone enable them

That said, the resulting code wasn't so elegant, but I didn't blame HTTP.


the ugly duckling
-----------------

..
    the trouble with objects, urls, stubs
    moved on, revisited after growth of stubs
    pain of stubs, generating stubs is concrete
    had to be a better way that didn't suck: more http

SLIDE::
    *blank*

This isn't a unique experience - most rpc libraries don't do anything to ease the 
pain. 

URL based apis often have a handful of endpoints with a number of special
ways to construct arguments. Most HTTP based clients suffer from a series
of fixed url templates.

Other libraries let you avoid the mechanics of making a remote call, and give you an
object. However you only get one and it has all the methods on it. Yay objects!

Some will offer generate your stubs for you. If you're lucky
the stubs will be for the right version of the server. If you're *really* lucky
they might even compile.

No matter how I looked at it, writing client code involved hardcoding
assumptions about how requests were made. Ugly, but necessary.

I moved on.

I had more important things to work on, I had to grow the product.
Unfortunately as the product grew, so did the network code. 

And then the stubs came. Thousands of them. Dirty dirty stubs.

SLIDE::

    class Queue 
      attr_accessor :worker_id

      def next_task
        task_id = http.POST(...)
        return Task(@worker_id, task_id)
      end
    end

    class Task 
      attr_accessor :worker_id, :task_id, :url
      def found_link(url)
        http.POST(...)
      end
      def complete 
        http.POST(...)
      end
      ...
    end

I'd just written code just like this server side, too. The stubs were getting everywhere.
At least my client code now looked ok, but stubs came with their own problems.

Adding new methods became copy and paste. The worst sort of code duplication. The nastiest
issue was state between requests - if we needed a new parameter, we had to change almost every
method.

Code generation is less painful in C# or Java, but in more dynamic language,
it adds a build step, can't infer types on its own, and rarely handles the dynamic
nature of the code.

SLIDE::

    *blank*

I was fed up. There had to be a better way.

    without duplicating code, by hand or by generation

    without having to make artisan requests for each method, wrangling state between them

    and without abandoning http, and all of its delights.


Logically, If the answer is not less http, the answer must be more HTTP.


And this is what hyperglyph does. MORE HTTP.


HTTP: Still good for you
------------------------

..
    h in http: web page not web service
    a sample session/mechanized
    client just like objects
    queue page, is rest in links, built from object
    urls are constructors
    similarly for task, & object
    hyperglyph is a serialization format
    rpc alike but hypertext - ducktyping, flexibility

Knowing this, how do we embrace http?

The clue is in the name. Hypertext transfer protocol.

Hypertext. Links and Forms. Web pages.


What if we were to build a *web page* rather than a *web service*? 

..
    possible slide: woah insert.



Perhaps something like this:

    - From the service root
    - Go to the queue page, click on next task.
    - on the new task, open the link in a new window
    - submit any links you find using this form
    - when you are finished, click 'complete'

When we write this down in code, it looks pretty familiar.

SLIDE::

    server = Glyph.get('http://local:219')
    queue = server.Queue('worker-12')
    task = queue.next_task
    crawl(task.url).each do |url|
      task.found_link(url)
    end


The initial get of the client fetches the root page. This root
has one attribute, Queue, which is a form to find a queue.

It submits the form, to get a queue page, and in turn
submits another form to get the next task.

Although to the client, it looks like objects and methods, it's still
a web page and forms underneath.  The client is actually screen scraping web pages.

But a web page for robots, not humans. 

These pages look something like this:

SLIDE::

    Root at /

    <Resource {
        'Queue': <Form('POST', '/Queue', 'worker_id')>,
    }>

    Queue at /Queue/?worker_id=bob

    <Resource {
        'next_task': <Form('POST','/Queue/next_task?worker_id=bob')>,
    }>

I won't get into the encoding now, but if you think of a json like format,
but with links and forms, you're close.

Unlike before where we had to pass parameters into each subsequent request,
the url encapsulates the state of the client.


We can generate the website from objects too - the Queue page
can be built from an object, and the urls can be built too.

SLIDE::

    class Queue < Resource
      attr_accessor :worker_id

      def next_task
        task_id = db.next_task(....)
        return Task(@worker_id, task_id)
      end
    end

When a client is returned a Queue, hyperglyph serializes the object
into a resource, with forms mapping to the methods.

The instance data is smuggled inside the query parameters.

SLIDE::

    Root at /

    <Resource {
        'Queue': <Form('POST', '/Queue', 'worker_id')>,
    }>

    Queue at /Queue/?worker_id=bob

    <Resource {
        'next_task': <Form('POST','/Queue/next_task?worker_id=bob')>,
    }>


We can see the mapping in the url, from the root it links to a class Queue,
and if we have a queue, we can see the next_task url points to a method,
as well as a particular queue.

When the client submits next_task, hyperglyph can construct a Queue object,
with the instance arguments in the query parameters, call queue.next_task, 
and serialize the response.

SLIDE::

    class Queue < Resource
      attr_accessor :worker_id

      def next_task
        task_id = db.next_task(....)
        return Task(@worker_id, task_id)
      end
    end

in this case, it returns a Task, which we turn into a webpage. The client
expects three attributes, url, found_link and complete.


SLIDE::
    
    class Task 
      attr_accessor :worker_id, :task_id, :url
      def found_link(url)
        db.found_link(...)
      end
      def complete 
        db.complete(...)
      end
      ...
    end


SLIDE::

    Task: /Task/?worker_id=bob&id=uuid
    
    <Resource {
        'url': ...
        'found_link': <Form('POST','/Task/found_link?id=uuid&worker_id=bob', 'url')>,
        'complete': <Form('POST','/Task/complete?id=uuid&worker_id=bob')>,
    }>

This page is generated from the class, like before. The instance data, and sometimes method
are embedded in the url, and used in form attributes.

    ~10m

Glyph is really a serialization format and supporting library. It handles turning
objects into web pages and back again.

*aside*
    The serialization is an extension of bencoding from bittorrent. 

    It's documented, ported to ruby, and it supports all of your favourites 
    - booleans, fixnums, utf-8 strings, byte arrays, nil, floats, 
    and iso date times. It also isn't endian specific.

The serialization format is really all you need client side to start using a 
server - and it's start page. Hypertext is what makes hyperglyph different,
and what allows it to map object and methods, dynamically.

SLIDE::

    blank

despite all of the underlying hypertext, at the client
it feels like rpc - you get objects and call methods. 
you get objects from the server without having to write them 
yourself first.

on the server it feels like rpc too, but with more flexibility.
the server can add new instance data - the urls change but the
forms don't. the server can add new methods too without breaking
old clients, and without requiring new stubs on the client.

like with duck typing, the server can return a different
object as long as it has the methods the client is expecting.

the interface is what is important, the names of things,
rather than the urls. the urls are opaque to the client,
and the server is free to change them, or point to other things.

hypertext gives freedom to the developer, to grow the api.

hypermedia is duck typing for apis.
are you on crack?
-----------------

It's also cross platform. The same client code in python is

SLIDE::

    import hyperglyph

    server = hyperglyph.get('http://local:219')

    queue = server.Queue(worker_id='woz')
    task = queue.next_task()
    for url in crawl(task.url):
        task.found_link(url)
    task.complete()

And if you wanted a server, in python is

SLIDE::

r = hyperglyph.Router()
@r.add()
class Queue(hyperglyph.r):
    def __init__(self, worker_id)
        self.worker_id = worker_ id
    def next_task(self):
        return Task(db.next_task(self.worker_id), worker_id)

@r.add()
class Task(hyperglyph.r):
    def __init__(self, uuid, worker_id):
        self.uuid, self.worker_id = uuid, worker_id

    def found_link(self, url):
        db.found_link(uuid, worker_id, url)

    def complete(self):
        db.complete(uuid, worker_id)


SLIDE::

    blank

hyperglyph: good for you?
--------------------

..
    hyperglyph loves http, made things suck less
    caching, sharding, embedding, extending
    fixed our apis, in internal use
    porting it to ruby, my first ruby proggram
    demonstrates utility of hypertext

You don't have to love HTTP to use hyperglyph. Glyph loves HTTP so much
it's going to handle turning your objects into pages and back again for you.

hyperglyph made my life suck less. I could change the server as I pleased
without breaking clients. Growing the software became a lot less painful.

SLIDE::

    caching
    sharding
    embedding
    extending

we're at the stage where we're adding caching to our services.
the client code won't change. the forms will, the urls might, but the
client won't change. the library, like the browser will handle this for 
the client.

..
    todo: mention embedding/ inlining

we're looking at sharding next. we'll add a few instance variables
into the server classes, but the methods won't change. as before,
the urls change, but the client code doesn't.

but when I need to add new behaviour, I don't break the existing
client code, and changing it isn't so hard either.

once we'd embraced hyperglyph, our apis changed dramatically. much 
of the state wrangling disappeared. thinking about web pages
changed how we thought about web services.

Writing network code still sucks, but now it sucks a lot less.

SLIDE::

    blank

The python code is relatively stable, but I've been changing things
as I've been porting it to ruby.


*aside*
    It's actually my first ruby program. I wrote it instead of writing
    this talk. If you think the talk is terrible, wait until you see my
    code. 

    I'm also looking at porting it to javascript and erlang, so if this 
    goes well I might volunteer for an erlang con next.

    I'm consoled by the fact that at least I learned something because
    of this talk.

As much as i've love you to use it - it isn't finished yet and it is still
maturing. If you're curious about what i've done I'd love help and guidance,
especially when it comes to ruby idioms.

Even if you don't use it, I hope i've shown that you can build loosely coupled
apis over http, when you use what http was built for: hypertext. 

It's there in the name.


yes, that's all very good but is it rest?
-----------------------------------------

..
    talked about http et all, but not rest
    rest is about the web not apis
    rpc vs rest is orthogonal - can be complementary
    we've been doing this for years with websites for humans
    is hyperglyph restful?


..
    other questions and answers - authentication,

Before I end, I should really go back to the beginning.

I've talked about HTTP, encodings, Hypertext, and URLS

I've talked about proxies, caches, and load balancers.


but I'm yet to mention REST 


REST isn't about APIS or RPC, it is about the web.
REST is about how all those things fit together, work together. 


Many people argue that RPC and the web are orthogonal, but I hope
with hyperglyph i've shown you that they are complementary.

It shouldn't come as a surprise - we've been mapping code to websites
for years, scraping them for years 




As for REST, well if rest is how the web works, and hyperglyph works like the web, Is hyperglyph RESTful?

No.

Hyperglyph is an encoding format and library. 



On its own, hyperglyph isn't a really a restful api.

but you can build one *using* hyperglyph, 

and it will make your life suck less.

thanks
------

SLIDE::

    @mamund, @steveklabnik, @jon_moore

I'd like to thank @jon_moore, @mamund, @steveklabnik for
writing some very useful things about hypermedia, 
but they're not to blame for this monstrosity.

SLIDE::

    http://github.com/hyperglyph

thank you for your time.

