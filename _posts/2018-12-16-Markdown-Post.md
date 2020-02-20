---
toc: true
---
# Parallelizing Python, Simplified (2)

## General Description

So you have some serial task that takes forever, and you're thinking it should be parallelizable, but you find
the documentation on this to be obtuse?  Yea.

Usually I'm interested in either *creating* lots of data in parallel, or *inputting* lots of data in parallel, and it's
often something that I first implemented as a loop but got tired of how slow it runs.  These involve [embarrassingly parallel](https://en.wikipedia.org/wiki/Embarrassingly_parallel) tasks in that they don't depend on one another.

There's a simple prescription for parallelizing most of these kinds of tasks in Python.  It goes as follows:
1. Have some kind of task performed in a for loop.
1. Write a function that does what you want for one "instance."  For example, take what's inside one of your for loops,
put all that in a separate function.
1. As a check, keep your loop but use only the function call. Make sure it produces the same results as the original version of your code.
1. Use functools.partial to create a wrapper for your function.
1. Replace the loop with a call to Pool.map().


In the following, we'll cover 3 examples for parallel tasks:
1. Generate a bunch of files
1. Read a bunch of files into a list
1. Filling a numpy array


## Example 1: Generate a bunch of files
Let's say you have some important synthetic data that you want to generate lots of instances of.
For now, for simplicity, we're just going to generate images of, let's say, random noise.  And to make it interesting
we'll generate 2000 of them.

Here's the serial for-loop version:

```python
import numpy as np
import cv2

n_images = 2000
size_x, size_y = 100, 100
for i in range(n_images):
    arr = 255*np.random.rand(size_x,size_y)
    filename = 'image_'+str(i)+'.png'
    print("writing file ",filename)
    cv2.imwrite(filename,arr)
```



## Lists

Here's a list:

- item 1
- item 2

And a numbered list:

1. item 1
1. item 2

## Boxes and stuff

> This is a quotation

{% include alert.html text="You can include alert boxes" %}

...and...

{% include info.html text="You can include info boxes" %}

## Images

![]({{ site.baseurl }}/images/logo.png "fast.ai's logo")

## Code

General preformatted text:

    # Do a thing
    do_thing()

Python code and output:

```python
# Prints '2'
print(1+1)
```

    2


More code:

```python
import numpy as np
import cv2

n_images = 2000
size_x, size_y = 100, 100
for i in range(n_images):
    arr = 255*np.random.rand(size_x,size_y)
    filename = 'image_'+str(i)+'.png'
    print("writing file ",filename)
    cv2.imwrite(filename,arr)
```

## Tables

| Column 1 | Column 2 |
|-|-|
| A thing | Another thing |


## Tweetcards

{% twitter https://twitter.com/jakevdp/status/1204765621767901185?s=20 %}


## Footnotes



[^1]: This is the footnote.
