Spine
=====
August 2014

For a while now I have been working on a silly little thing that I call [Spine](https://github.com/varl/spine). It is
really nothing special, just another static site generator(TM). It takes markdown files and converts them to HTML that 
it combines with one (or more) templates, any static content that is needed and plops out a JAR-file that can be run
with `java -jar spine-app.jar` on any platform. Voilá.

It does of course have some quirks; it wants Java 8 to run, which feels obvious considering I wrote the core to learn
about the new-fangled stuff introduced in Java 8 like streams and lambdas.

My original plan was to use no libraries and just roll everything myself. I rather quickly backtracked on this decision 
when I became bored out of my mind trying to reinvent the wheel smarter people had built better a long time ago.
Case in point: the Guava library. So much for that philosophy.

Spine at the moment does pretty much what I want it to with no fuss.

- It's built by `mvn clean install` and produces a single JAR-file with all the dependencies
- It runs anywhere with just `java -jar spine-app.jar` thanks to embedded Jetty
- It takes `something.md` and combines it with either `default.vm` or `something.vm` to make it prettier
- If I need multiple content blocks on one page it can do that to, by naming the content files `something_1.md` and so
forth. In the `something.vm` template the content can be placed by `${something_1}`, for example in multi-column 
layouts
- It serves its own static files if necessary
- No configuration, unless ... you might want to put a reverse proxy and maybe some caching in front of it, but you 
 do not have to.