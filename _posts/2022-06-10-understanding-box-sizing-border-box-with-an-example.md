---
layout: post
title: "Understanding box-sizing: border-box with an example"
excerpt_separator: <!-- excerpt_separator -->
---

Let's say we've a container with a box inside of it:

```
 <div class="container">
    <div class="box">I'm a box.</div>
 </div>
```

<!-- excerpt_separator -->

Let's give a `width` of 1000px for the container and 800px for the box. And let's give some `padding`
and a `border` for the box as well.

```
 .container {
    width: 1000px;
    margin: 0 auto;
    background-color: steelblue;
 }

.box {
    width: 800px;
    border: solid 5px;
    padding: 20px;
 }
```

Here's what we've got so far:
<br><br>
![](/assets/1.png)
<br><br>
Now what if we want to horizontally center the box inside the container?

We could give the box an equal `margin` on either side like so:

```
 .box {
    width: 800px;
    border: solid 5px;
    padding: 20px;
    margin-left: 10%;
    margin-right: 10%;
 }
```

We've given a `margin-left` and `margin-right` of 100px (10% of 1000px).

So now we've a 1000px wide container, with a 800px wide box inside of it, and a `margin` of
100px on either side of the box.

That should center the box, right?

Here's what the result looks like:
<br><br>
![](/assets/2.png)
<br><br>
Uh-oh! Instead of being centered, it looks like our box is positioned more towards the right.

So what happened?

Well, it turns out that the width of the box isn't 800px even though we had mentioned it as such
in our CSS, because the `box-sizing` property for the box element has a value of `content-box` by
default. What that means is that the 800px width that we had specified is just the width of the
text content inside the box, and does not include the `padding` and `border`.

So the actual width of the box = 800px (text content width) + 40px (20px padding on either side) +
10px (5px border on either side) = 850px

And the total width of content inside the parent container = 850px (box width) + 200px (100px margin
on either side) = 1050px
<br><br>
![](/assets/3.png)
<br><br>
As you can see, the content inside the container (box + margin) overflows its parent by 50px.

One way to solve this problem would be to simply reduce the `margin` from 10% to 7.5%.

```
 .box {
    width: 800px;
    border: solid 5px;
    padding: 20px;
    margin-left: 7.5%;
    margin-right: 7.5%;
 }
```

So now the width of the content inside the container = 850px (box width) + 150px (75px margin on
either side) = 1000px.

The box is now centered inside the container.
<br><br>
![](/assets/4.png)
<br><br>
But the problem here is that if we change the width of the container, this will no longer work.

So the solution really is to tell the browser that when we specify a certain width for an element
in our CSS, we want the `padding` and `border` to be included in the total width of that element. We
can do that by setting the `box-sizing` property to `border-box` like so:

```
.box {
    box-sizing: border-box;
}
```

Now we can set the `margin-left` and `margin-right` property of the box to any value and it'll
remain centered, irrespective of the width of the container.
