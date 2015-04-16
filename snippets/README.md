Snippets
========

Convert line endings
--------------------

### Dos => Unix

```
sudo apt-get install dos2unix
find . -type f -exec dos2unix {} \;
```

Javascript
----------

[From Synbioz blog](http://www.synbioz.com/blog/utilisation_titres_html), a snippets to check headings and heading hierarchy on a page:

```js
var titles = document.querySelectorAll('h1,h2,h3,h4,h5');
for (var i = 0; i < titles.length; i++) {
  var index = titles[i].tagName.split('').pop(),
      tab = [];
  while(tab.length < index-1){ tab.push("--");}
  console.log(tab.join('') + '| ' + titles[i].tagName + ' | ' + titles[i].innerHTML);
}
```
