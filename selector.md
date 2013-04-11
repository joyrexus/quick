Simple Selections
=================


## Selecting (without jquery)

Return *first* element matching css selector pattern (on a node).

```coffeescript
$ = (p, node) ->
  node ?= document
  node.querySelector p
```
Return *all* matching elements.

```coffeescript
$$ = (p, node) ->
  node ?= document
  node.querySelectorAll p
```
Return array of *all* matches.

```coffeescript
$$ = (p, node) ->
  node ?= document
  selection = node.querySelectorAll p
  Array::slice.call selection
```
Use this just like you would jquery.

```coffeescript
$("div")
$("#id")
$(".class")
$$('#container li')
$$("#large:nth-child(even)")
```

## Get element attributes

```coffeescript
$("#id").getAttribute 'data-fruit'
$('input').getAttribute 'name'
```

## Modifying elements

```coffeescript
$('#box').classList.add 'wrap'
$('#box').classList.remove 'wrap'
$('#box').classList.toggle 'wrap'
```

## Animate a modal dialog into or out of view

```coffeescript
notice = $("#notice")
notice.classList.add "modal-visible"
notice.classList.remove "modal-visible"
notice.classList.toggle "modal-visible"
```

