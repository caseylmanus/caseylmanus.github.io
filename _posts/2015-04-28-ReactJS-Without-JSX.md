---
layout: post
title:  "ReactJS without JSX - Suprisingly Elegant"
date:   2015-04-18 10:28:46
categories: ReactJS, JavaScript, SPA
---

I was working on a small hybrid mobile project yesterday and wanted to use [ReactJS](https://facebook.github.io/react/) and the Flux architecture pattern to power the user interface.  I didn't want to use JSX becuase I wanted it to fit into the existing build system without any modifications, so adding the React tools wasn't an option.  

Typically, when you use ReactJS without JSX the resulting render code looks something like this:

{% highlight JavaScript %}
render: function(){
	return React.createElement('ul', {}, React.createElement('li', {}, null, 'First Element'));
}
{% endhighlight %}
OR:
{% highlight JavaScript %}
render: function(){
	return React.DOM.ul({}, React.DOM.li({}, null, 'First Element'));
}
{% endhighlight %}

And that would create the following html:

{%  highlight html %}
<ul>
	<li><span>First Element</span></li>
</ul>
{% endhighlight %}

For anyone that has looked at the output from the JSX compiler, then the first should be fairly familiar to you,
and the second is taking advantage of the "React.DOM" helpers provided by the framework.

This is ok, but I find it a little verbose to write without machine assistance (ie, JSX compiling).  So I set out 
to simplifiy it for my own purpose.  What I quickly realized is that the method "React.createElement" takes the following arguments:

* type:  the type of element to create, either a string for an html element, or a ReactJS class.
* properties:  an object that represents properties of the html element for example "{id: 'contentDiv'}" 
* an array of children to the element

That meant that any React Element could be represented in a simple JSON data structure.  For the example above, the JSON would look 
like this:

{% highlight JavaScript %}
var element  = {
	type: 'ul',
	props: {},
	children: [{
		type: 'li',
		props {},
		children: ['First Element']
	}]
};
{% endhighlight %}

Given that data representation, it was a simple matter to write a method to iterate recursively over the tree of element meta data
and then use it in your render method:

{% highlight JavaScript %}
renderTree : function(tree){
    var children = [];
    var self = this;
    tree.children.forEach(function(child){
        if(typeof child === 'string'){
            children.push(child)
        } else {
            children.push(self.renderTree(child));
        }
    });
    return React.createElement(tree.type, tree.props, children);
},
render: function(){
	var tree = this.getTree();
	return this.renderTree(tree);
}
{% endhighlight %}

I don't think this concept is unique or even complete at this point, but I hope it does reveal a path
to elegantly working with ReactJS without JSX which others might find useful.  It also gave me really
good insight into how the JSX compiler works, and how ReactJS works.    

To complete the concept, I would create a ReactJS mixin for the "renderTree" function, and create a 
DSL to make it easy to build and manage the JSON data structure. 

For most use cases, I still feel like JSX is superior.  
