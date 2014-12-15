---
layout: post
title:  "Discovering AngularJS - A Journey"
date:   2014-12-12 10:28:46
categories: 
---

Avoidance
------
First of all, let me say that for a long time, I've **hated, avoided, and shunned** [AngularJS](http://angularjs.org).  It was a bit irrational but whenever I am exploring a new technology, I have to get that "AH-HA" moment before I can truely internalize it and consider it viable.  I've tried in the past to get there with AngularJS, but I never really did.  I got bogged down by the fact there seems to be so many concepts and words that don't map to the non-AngularJS world.  Every example I found was trivial and it was hard to figure out how I could map it to the real-world apps I've done with BackboneJS.  

Desire and Curiosity
-----
I've honestly grown a bit tired of my old [Backbone.js](http://backbonejs.org) stack.  There are some things I love about the framework,  such as the fact it is code based rather than convention, it is light weight, it has rich model support.  The other big seller for me is that there are exactly 4 major concepts to learn:  Models, Collections, Views, and Routers.  

A big problem for me was always the fact that Views are almost an afterthought with very little lifecycle management.  I also found that [EpoxyJS](http://epoxyjs.org) was a good addition to help with 2 way data binding.  So my peferred stack of BackboneJS  + Epoxy + [RequireJS](http://requirejs.org) was plenty capable, but there was a bit of boilerplate code I kept around to assist with the View lifecycle and garbage collection.  I tried [Marionette.js](http://marionettejs.com) on one project to assist with the view lifecycle and the boilerplate code, but I also wanted to consider a completely different alternative mostly due to mental fatique.  

A Brief Love Affair
-----
While looking at alternatives I feel in love with [Polymer](http://polymer-project.org) and love the potential glimpse into the future of building apps with web components.  There are some big ideas represented here, and it is worth a look. Polymer leverages some concepts such as the proposed HTML web components, shadow-dom and HTML imports. These aren't really available in any major browser outside of Chrome, so Polymer provides a set of polyfils to make it possible to leverage those concepts. Between versions there have been significant breaking changes and there are some clear performance challenges, which rules it out for production use at this time.

What I wanted
------
 For whatever I did in my next project, I wanted to get the same component based feel as Polymer.  I wanted to be able to write custom elements that encapsulate funcionality and behaviors within them, and I wanted my HTML to be expressive of functionality, not just structure.

 For example, if I was building a site similar to Amazon:

{% highlight html %}
<site-shell>
	<left-panel>
		<site-menu></site-menu>
	</left-panel>
	<right-panel>
		<main-content>
			<featured-productcarousel></featured-productcarousel>
			<product-categories></product-categories>
			<recommended-productsbyhistory></recommended-productsbyhistory>
		</main-content>
		<site-footer></site-footer>
	</right-panel>
</site-shell>
{% endhighlight %}

Finally the AH-HA moment
----
So I started with the AngularJS documentation, and I reviewed mutiple tutorials and videos. I still just didn't get it.  I finally found a [course](http://campus.codeschool.com/courses/shaping-up-with-angular-js) at CodeSchool that really got me started.  I highly recommend you to take this course, it should only take a couple of hours.  I also found a great 
[blog post](http://teropa.info/blog/2014/10/24/how-ive-improved-my-angular-apps-by-banning-ng-controller.html) that discusses eliminating ng-controller from your app, this really clicked for me and got me where I wanted to go.  

The Concepts
-----
AngularJS is **BIG**.  There are a lot of concepts that slap you in the face when you are first looking into it.  The **reality** though, is that there aren't that many you really should care about.  You can build an app that is well structured and elegant with just a few of them: 

 * Modules
 * Directives
 * Expressions and Filters
 * Services and Factories
 * Routes

Know the rest exist, but don't concern yourself too much with the other things in my opinion. 


Modules
========
An application module is a "namespace" for your code.  Using multiple modules allows you to organize your code into functional areas either by objects of the same type, i.e. "technical slice" or by objects that provides related user facing functionality, i.e "functional slice".  My preference is to organize your app code by functional slice, but it is not common to have some items that are cross function or utility in nature, so doing those in a technical slice organization isn't a bad option.

{% highlight javascript %}
var app = angular.module("moduleName", ["arrayOfModuleDepencies", "secondDependency"]);
{% endhighlight %}


Directives 
=========
Directives are what allows those cool custom HTML elements I discussed earlier.  A directive is the primary building block that everything else enables and services.  Directives can be for custom elements or custom attributes in other HTML elements.  You can even use a custom attribute on a custom element to compose things together.  

Expressions and Filters
=========

Services and Factories
=========
Services and Factories are the "Model" of your application, or more accurately how you interact with your model.  At first, I was a bit 
concerned that this was anemic, and not quite workable.  My philosophy shifted a little and I realized that the Angular way was a bit freeing
over the Backbone.js way.  You can allow your model to live on the server, or you can build a richer model in about anything you want (including Backbone.js) and wrap it with a service or a factory so the rest of you Angular app can interact with it without much problem.  

-----
What's the difference between a service and factory?

One thing to remember about AngularJS is that it provides [Dependency Injection](http://en.wikipedia.org/wiki/Dependency_injection) to assist with unit testing.  Therefore, all Factories and Services are singleton objects.  With that knowledge it is easy to understand the difference. 

 **Service:** This is a function provided to your consumer.  Think of these as global functions in a way, but injected into your code so they can be mocked.  <br />
 **Factory:** This is an object provided to your consumer, it will be instantiated (by using the new keyword) by the framework prior to injecting it into your code.  This is similar to the factory pattern in any other environment. 


Routes
=========

AngularJS 2.0 and the future
-----

Conclusion
-----




