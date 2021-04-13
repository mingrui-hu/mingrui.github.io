---

layout: default 

title: Blog 
---

# Latest Posts

<ul>  {% for post in site.posts %}    
  <li>      
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>      
    {{ post.excerpt }}    </li>  {% endfor %} </ul>

## try a markdown equivalent of listing all posts
{% for post in site.posts %}    
[{{ post.title }}]({{ post.url }})      
First paragraph of the post
> {{ post.excerpt }}

{% endfor %}
