Bookmarklets
============

Drag the link above into your bookmarks bar

Responsive Bookmarklets
-----------------------

RWD: Responsive Design Bookmarklet: a handy tool for responsive design testing

```js
javascript:void((function(){var d=document;d.write('<!DOCTYPE html><html><head><meta charset=&quot;UTF-8&quot;><title>'+d.title+' - Responsive test</title><link rel=&quot;stylesheet&quot; href=&quot;http://responsive.victorcoulon.fr/assets/css/app.css&quot;><script src=&quot;http://responsive.victorcoulon.fr/assets/js/app.min.js&quot;></script></head><body><header><div class=&quot;close&quot;><a href=&quot;#&quot;>×</a></div><div id=&quot;size&quot;></div><div class=&quot;keyboard&quot;><a href=&quot;#&quot;>I</a></div><div class=&quot;cssrefresh&quot;><a href=&quot;#&quot;>I</a></div><div id=&quot;devices&quot;><a href=&quot;#&quot; class=&quot;tablet-portrait&quot;><span>Tablet Portrait</span></a><a href=&quot;#&quot; class=&quot;tablet-landscape&quot;><span>Tablet Landscape</span></a><a href=&quot;#&quot; class=&quot;smartphone-landscape&quot;><span>iPhone Landscape</span></a><a href=&quot;#&quot; class=&quot;smartphone-portrait&quot;><span>iPhone Portrait</span></a><a href=&quot;#&quot; class=&quot;auto active&quot;><span>Auto</span></a></div></header><section><div id=&quot;wrapper&quot;><iframe src=&quot;'+d.URL+'&quot; onLoad=&quot;resbook.changeUrl(this.contentWindow.location,this.contentDocument.title);&quot;></iframe><span class=&quot;keyboard-bg&quot;></span></div></section></body></html>')})());
```

Source: http://responsive.victorcoulon.fr

Github Print Bookmarklets
-------------------------

Printing Github Markdown with GitPrint

```js
javascript:void((function(){if(document.location.hostname.indexOf('github.com')!==-1){window.open(document.URL.replace('github.com','gitprint.com'),'_blank');}})());
```

Source: [https://gitprint.com/](https://gitprint.com/)

"Pint it", from Pinterest
-------------------------

```js
javascript:void((function(d){var e=d.createElement('script');e.setAttribute('type','text/javascript');e.setAttribute('charset','UTF-8');e.setAttribute('src','//assets.pinterest.com/js/pinmarklet.js?r='+Math.random()*99999999);d.body.appendChild(e)})(document));
```

Source: [http://pinterest.com](http://pinterest.com)


"Add to Delicious", from Delicious
----------------------------------

```js
javascript:(function(e,t){var n=e.document;setTimeout(function(){function a(e){if(e.data==="destroy_bookmarklet"){var r=n.getElementById(t);if(r){n.body.removeChild(r);r=null}}}var t="DELI_bookmarklet_iframe",r=n.getElementById(t);if(r){return}var i="https://delicious.com/save?",s=n.createElement("iframe");s.id=t;s.src=i+"url="+encodeURIComponent(e.location.href)+"&title="+encodeURIComponent(n.title)+"&note="+encodeURIComponent(""+(e.getSelection?e.getSelection():n.getSelection?n.getSelection():n.selection.createRange().text))+"&v=1.1";s.style.position="fixed";s.style.top="0";s.style.left="0";s.style.height="100%25";s.style.width="100%25";s.style.zIndex="16777270";s.style.border="none";s.style.visibility="hidden";s.onload=function(){this.style.visibility="visible"};n.body.appendChild(s);var o=e.addEventListener?"addEventListener":"attachEvent";var u=o=="attachEvent"?"onmessage":"message";e[o](u,a,false)},1)})(window)
```

Source: [https://delicious.com/tools](https://delicious.com/tools)
