---
layout: post
title: "A Clojurescript REPL inside your Emacs"
description: "How to load a Clojurescript REPL inside your emacs from a lein project using CIDER."
category: clojurescript
tags: ["how-to repl clojurescript nrepl emacs cider"]
---
{% include JB/setup %}

After trying LightTable and discovering that perhaps the environment of functional programming languages is actually better than object-oriented programming languages because you can eval basically anything, I've wanted to replicate the same thing in my new and shiny editor, the old Emacs.

With **CIDER** (acronym for Clojure Interactive Development that Rocks for Emacs), it is pretty easy to load a REPL for Clojure inside emacs.

But sadly for **Clojurescript**, as your application is usually run in a browser(there are people doing node.js with clojurescript!), the scene changes. It took a while for me to figure it out it's not the same thing as a normal Clojure REPL. __To have a Clojurescript REPL in your terminal, you need [Figwheel](https://github.com/bhauman/lein-figwheel).__

> In the Clojurescript land we don't really need to ever refresh our browser, it even should keep the last state you left. This is different from the conventional approach that other platforms use which watches the filesystem and refreshs the browser using websockets. Well, enough propaganda.

For the sake of having an example, we will start with a clean figwheel project:

{% highlight bash %}
lein figwheel new hello-world
{% endhighlight %}

Now, inside `project.clj` we have a `:figwheel` key with two commented lines, like this:

{% highlight clojure %}
;; Start an nREPL server into the running figwheel process
;; :nrepl-port 7888
{% endhighlight %}

We now will uncomment this nrepl-port line, so it will now start a nREPL server in that port whenever you run `lein figwheel`, like this:

{% highlight clojure %}
;; Start an nREPL server into the running figwheel process
:nrepl-port 7888
{% endhighlight %}

And we are done on the configuration on the project's side. Yes, it's just as easy as uncommenting one line.

Now on the dark, erm, **Emacs side**, you need to install **CIDER**. For instructions please check [this](https://github.com/clojure-emacs/cider#installation).

After Cider is installed, we will connect to a specific nREPL which is the nREPL server we configured in `project.clj` at `localhost:7888` by pressing:

``M-x cider-connect``

Now specify `localhost` as the __Host__ and `7888` as the __port__. You should have a REPL tab now, in case it doesn't open try pressing ``M-x cider-switch-to-repl-buffer``.

At this point, we still won't have the lovely, long-awaited Clojurescript REPL we wanted. For that, just run those two lines inside the REPL buffer we've got:

{% highlight clojure %}
user> (use 'figwheel-sidecar.repl-api)
user> (cljs-repl)
{% endhighlight %}

__(thanks [@yogthos](http://yogthos.net/posts/2015-06-16-Figwheel-nREPL.html))__

And now, you have a working Clojurescript REPL ready to build on amazing things.

![Clojurescript REPL]({{ site.url }}/assets/images/cideremacs.png)

## Having problems with nrepl-refactor?

This is a issue that I've had. When connecting with cider I've got the message `nrepl-refactor middleware not available! Did you remember to install it?`.

To fix that, add to your emacs config:

{% highlight elisp %}
(setq cljr-suppress-middleware-warnings t)
{% endhighlight %}

And it should work fine. More on that in this [Github issue](https://github.com/clojure-emacs/cider/issues/1140)
