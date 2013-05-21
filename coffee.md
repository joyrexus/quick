Coffee
======

In which we list tips, tricks, and reminders.

* [Misc.](#misc)
* [Strings](#string)
* [Words](#words)
* [Arrays](#array)
* [Math](#math)

Links to official docs:

* [Wiki](https://github.com/jashkenas/coffee-script/wiki)
* [Overview](http://coffeescript.org/#overview)
* [Reference](http://coffeescript.org/#language)
* [Helpers](http://coffeescript.org/documentation/docs/helpers.html)
* [Style Guide](https://github.com/polarmobile/coffeescript-style-guide)


Helper methods for testing and whatnot.

```coffeescript
{print, ok, eq, arrayEq} = require 'testy'
```

## <div id="misc">Misc.</div>

List method names of arrays and strings:

```coffeescript
dir = (obj) -> Object.getOwnPropertyNames(obj.constructor.prototype)

print dir []    # last, extend, pop, push, ...
print dir 's'   # upper, length, lower, ...
```

A few numbers for stuff below.

```coffeescript
nums = [1..4]
```

Print each value:

```coffeescript
print x for x in nums                 # 1 2 3 4
```

Print index, value pairs:

```coffeescript
print i, x for x, i in nums
```

Print key, value pairs of object:

```coffeescript
numbers = 
  one: 1
  two: 2
  three: 3

print key, value for key, value of numbers
```

Filter out even values:

```coffeescript
isEven = (x) -> x % 2 == 0
arrayEq [1, 3], 
        (x for x in nums when not isEven x)
```

Generate list of squares:

```coffeescript
square = (x) -> Math.pow(x, 2)

arrayEq [1, 4, 9, 16], 
        nums.map square
```

Equivalent to ...

```coffeescript
arrayEq [1, 4, 9, 16],
        (square x for x in nums)
```

Generate list of squares for values in object:

```coffeescript
numbers = 
  one: 1
  two: 2
  three: 3

arrayEq [1, 4, 9], 
        (square x for word, x of numbers)
```

A simple counter:

```coffeescript
class Counter
  constructor: (@total=0) ->
  inc: (n=1) -> @total += n
```

    counter = (total=0) -> 
      (inc=1) -> total += inc

```coffeescript
count = new Counter(5)
eq count.inc(), 6
eq count.inc(), 7
eq count.total, 7
```

## <div id="string">Strings</div>

Split a string:

```coffeescript
words = "foo bar baz biz buz".split(" ")
arrayEq words, ['foo', 'bar', 'baz', 'biz', 'buz']

words = "foo|bar|baz|biz|buz".split("|")
arrayEq words, ['foo', 'bar', 'baz', 'biz', 'buz']
```

Extend prototype w/ pythonic method names

```coffeescript
String::upper = -> @toUpperCase()
String::lower = -> @toLowerCase()
eq 'FOO', 'foo'.upper()
eq 'foo', 'FOO'.lower()
```

## <div id="words">Words</div>

```coffeescript
wordlist = "foo bar baz biz buz".split(" ")
ok 'foo' in wordlist
ok not ('boo' in wordlist)
```

Make a dict (associative array) for easy lookups:

```coffeescript
dict = {}
for word in wordlist
  dict[word] = 1

ok dict['foo'] and not dict['boo']
ok dict.foo and not dict.boo
```

Pass in a string of words for easy lookups:

```coffeescript
makeDict = (wordlist) -> 
  new class then constructor: ->
    @[word] = 1 for word in wordlist.split(" ")

dict = makeDict "foo bar baz biz buz"
ok dict['foo'] and not dict['boo']
ok dict.foo and not dict.boo
```

Variant version:

```coffeescript
class Dict
  constructor: (wordlist) ->
    @[word] = 1 for word in wordlist.split(" ")

dict = new Dict "foo bar baz biz buz"
ok dict['foo'] and not dict['boo']
ok dict.foo and not dict.boo
```

Filter out non-dict words:

```coffeescript
sent = "I want to foo that bar with biz"
dictwords = (word for word in sent.split(" ") when dict[word])
arrayEq dictwords, ['foo', 'bar', 'biz']
```

## <div id="array">Arrays</div>

We'll use this list of numbers below.

```coffeescript
nums = [1..4]
```

Get length of array:

```coffeescript
eq 4, nums.length
```

## Mutator Methods

Pop last element:

```coffeescript
x = nums.pop()
arrayEq nums, [1..3]
```

Push element to end and return length:

```coffeescript
n = nums.push(x)
arrayEq nums, [1..4]
eq nums.length, n
```

Reverse order:

```coffeescript
arrayEq nums.reverse(), [4..1]
```

Sort elements:

```coffeescript
arrayEq nums.sort(), [1..4]
```

Shift (pop off first element):

```coffeescript
x = nums.shift()
arrayEq nums, [2..4]
```

Unshift (push element to front and return length):

```coffeescript
n = nums.unshift(x)
arrayEq nums, [1..4]
eq n, 4
```

Lexicographic sort (default):

```coffeescript
nums = [9, 10, 100, 20, 200, 3, 1]
arrayEq nums.sort(), [1, 10, 100, 20, 200, 3, 9]
```

Numeric sort:

```coffeescript
numeric = (a, b) -> a - b
arrayEq nums.sort(numeric), [1, 3, 9, 10, 20, 100, 200]
```

Splice first element:

```coffeescript
nums = [1..10]
x = nums.splice(0, 1)     # same as nums.pop()
arrayEq nums, [2..10]
arrayEq x, [1]
```

Splice first two elements:

```coffeescript
nums = [1..10]
x = nums.splice(0, 2)
arrayEq nums, [3..10]
arrayEq x, [1, 2]
```

Splice out second element:

```coffeescript
nums = [1..10]
x = nums.splice(1, 1)
expected = [1].concat [3..10]
arrayEq nums, expected
arrayEq x, [2]
```

Splice out second and third elements:

```coffeescript
nums = [1..10]
arrayEq nums.splice(1, 2), [2, 3]
arrayEq nums, [1].concat [4..10]
```

Note the syntax: `array.splice(index, count)`

Splice in elements at start of array (index 0):

```coffeescript
nums = [1..4]
nums.splice(0, 0, 'a', 'b')
arrayEq nums, ['a', 'b'].concat [1..4]
```

Replace two elements at start of array (index 0):

```coffeescript
nums = [1..4]
nums.splice(0, 2, 'a', 'b')
arrayEq nums, ['a', 'b', 3, 4]
```

Note the syntax: `array.splice(index, count, a, b, ...)`

```coffeescript
nums = [1..4]
nums.splice(0, 2, 'a', 'b', 'c')
arrayEq nums, ['a', 'b', 'c', 3, 4]
```

Concatenate:

```coffeescript
arrayEq [1..10],
        [1..5].concat [6..10]

arrayEq [1..10],
        [1..5].concat 6, 7, 8, 9, 10
```

Join list elements into a string:

```coffeescript
eq '1,2,3,4', [1..4].join()
eq '1|2|3|4', [1..4].join('|')
eq '1234', [1..4].join('')
```

Sum values in a list:

```coffeescript
nums = [1..4]
eq 10, nums.reduce (x, y) -> x + y
```

Test for some true elements:

```coffeescript
some = (list, fn) ->
  for e in list
    return yes if fn e
  no

gtThree = (x) -> x > 3
gtFour = (x) -> x > 4

ok some nums, gtThree
ok not some nums, gtFour
```

Test that all elements are true:

```coffeescript
all = (list, fn) ->
  for e in list
    return no unless fn e
  yes

ltFive = (x) -> x < 5

ok not all nums, gtThree
ok not all nums, gtFour
ok all nums, ltFive
```

## Prototype Extensions

It can be handy to define custom array methods on the `Array` 
prototype so they can be used like the `reduce` method above.

Sum array of numbers:

```coffeescript
Array::sum = (x, y) -> @.reduce (x, y) -> x + y

eq 10, nums.sum()
```

Get the last item:

```coffeescript
Array::last = -> @[@.length - 1]

eq 4, nums.last()
```

Trim out all falsy values from an array

```coffeescript
Array::compact = ->
 item for item in @ when item

arrayEq [1, 2, 3], 
        [1, false, 2, '', 3, null].compact()
```

Flatten a nested array

```coffeescript
Array::flatten = ->
  flat = []
  for e in @
    if Array.isArray e
      flat = flat.concat e.flatten()
    else
      flat.push e
  flat

arrayEq [1..4],
        [1, [2, [3, [4]]]].flatten()
```

Extend an array (as mutator method):

```coffeescript
Array::extend = (other) -> 
  Array::push.apply @, other
  @

letters = ['a', 'b', 'c']
letters.extend ['d', 'e', 'f']
eq letters.length, 6
eq letters.last(), 'f'
```


## Iteration Methods

Collect the doubled value for each number in `nums`:

```coffeescript
nums = [1..4]
doubles = []
double = (x) -> doubles.push (x * 2)
nums.forEach double
arrayEq doubles, [2, 4, 6, 8]
```

Every element meets condition?

```coffeescript
ok doubles.every (x) -> x > 1
ok not doubles.every (x) -> x < 4
```

Some elements meet condition?

```coffeescript
ok doubles.some (x) -> x < 4
ok not doubles.some (x) -> x > 50
```

Filter out elements not meeting condition:

```coffeescript
arrayEq [3, 4], nums.filter (x) -> x > 2
```

Map a function to each element:

```coffeescript
arrayEq [2..5], nums.map (x) -> x + 1
```

Reduce elements to a single value:

```coffeescript
eq 10, nums.reduce (x, y) -> x + y
```

## <div id="math">Math</div>
     
Find min/max in a list:

```coffeescript
nums = [10, -10, 100, 0, 1]
eq 100, Math.max.apply @, nums
eq -10, Math.min.apply @, nums
```

Primality tester:

```coffeescript
isPrime = (x) ->
  p = 2
  while p * p <= x
    return false if x % p == 0
    p += 1
  true
```

Find primes:

```coffeescript
arrayEq [1, 2, 3, 5, 7, 11, 13, 17, 19],
        (x for x in [1..20] when isPrime x)
```

Find factors:

```coffeescript
factors = (n) -> i for i in [1..n] when n % i == 0

arrayEq [1, 11], 
        factors 11
```


