# Interactive Programs

In this lesson we are going to design interactive programs. Here's a
demo of what we will be building:

It will be a program that is animated and it responses to our key or
mouse inputs.

## Behind the Scenes

First off, before we start building, we need to talk about what an
interactive program or interactive world is. Let's look at this
animation of a landing rocket.

![rocket](http://i.imgur.com/QoH63U1.gif)

What's happening behind the scenes is that there's two things causing
things to change in the world.

### Clock Ticks and State

| tick | state |
|------|-------|
|  0   |   0   |
|  1   |   3   |
|  2   |   6   |
|  3   |   9   |
|  4   |  12   |
|  5   |  15   |

The clock tick and the state are what the animation is reacting
to. For simplicity, let's imagine that a tick is a second. At the
first tick, we see that the rocket's state is 0. This 0 represents the
y coordinate of the rocket. That's because the rocket has to start
from the top of the scene.

### The Coordinate System

You might be wondering why does 0 represent the position at the top of
the scene. Well, that's because the coordinate system starts from the
top left hand corner of the scene.

### Animating a Picture

At the next tick, we see that the rocket has advanced (or descended) 3
pixels downwards. And this happens for the next and subsequent ticks
as well, until the rocket has landed.

If you observe the animation, you will notice that the rocket isn't
actually descending at the rate of 3 pixels per second. In fact, it's
actually descending much faster than that. That's because the default
rate at which DrRacket advances each tick is 28 ticks per second.

What you see is like a cartoon, an animation is simply a series of
images that flashes before you rapidly to bring about the illusion
that the rocket is moving.

## Let's Draw!

Now, let's look at how we can draw the image of a rocket on the
scene.

First, we will need the image of the rocket. You can get one from
google or you may use this
![rocket](https://raw.githubusercontent.com/0nse/Hangouts-Emojis/master/Hangouts-Emojis/1f680.png)
that I have choosen.

![rocket-rotate](http://i.imgur.com/Pk06Pkm.png)

Don't forget to rotate the rocket 45 degrees clockwise to get make it
upright.

To place the image of the rocket on the screen, we will need the
`place-image` function. This function will place an image on top of
another image at the position that you have specified. The place-image
function takes an image, the x and y coordinate of the image, and
another image. Now, let's place the rocket at the (300, 300) position
of the screen.

```
(define (render-rocket)
  (place-image ROCKET 150 150
               (empty-scene 300 300)))
```

Notice that we have chosen a size of 600 by 600 size for the
screen. This size is arbitrary, you can use any size you want but I
use this size for simplicity.

## Landing It Step By Step

Great! You should have a rocket drawn on the screen, but wait a
minute, the rocket isn't landing! Well, that's because we are not
changing its state, which in this case, the y position of the
rocket. Since the coordinate system starts from the top left hand
corner, larger y values will be at the bottom of the
screen. Therefore, we will need to increase the y positon of the
rocket. To increase its y position by 3 we will need this function:

```
(define (next-rocket y-posn)
  (+ y-posn 3))
```

## Putting It Together

Now that we have the function to change its state and the function to
draw, let's try to put this all together. First, we need to tweak our
`render-rocket` function to take in the y position of the book and
pass it to the `place-image` function so that rocket is placed at the
next rocket's position.

```
(define (render-rocket y-posn)
  (place-image ROCKET 150 y-posn
               (empty-scene 300 300)))
```

Let's call `render-rocket` with an initial value of 150.

```
(define initial 150)

(render-rocket initial)
```

You should see a rocket in the middle of the screen, but wait, it's
still not moving. That's because we are not changing the state at
all. Now, let's call `render-rocket` with `next-rocket` like so:

```
(render-rocket (next-rocket initial))
```

You should notice that the rocket has moved slightly and to actually
land the rocket, we will need to repeat this process of calling
render-rocket with next-rocket several times.

```
initial -> render-rocket -> next-rocket -> render-rocket
  -> next-rocket -> render-rocket -> next-rocket -> render-rocket
    -> next-rocket -> render-rocket -> ...
```

Hence, we need the `big-bang` function. The `big-bang` function
introduces the notion of clock ticks as we have discussed
previously. At each clock tick, it calls next-rocket on the current
state and calls render-rocket to draw the rocket on the screen. Let's
look at how to call the `big-bang` function:

```
(big-bang 150 ;; initial state
          ;; how do you want to change the state on each tick
          (on-tick next-rocket)
          ;; how do you want to draw onto the world
          (to-draw render-rocket))
```

The first argument is the initial state, and the second and their
argument are functions that takes in the next-rockt and render-rocket
functions. The next-rocket is your state changing function where it
takes the current state of the world and returns the new state of the
world. Which in our case, it takes in the y position and increases it
by 3. The render-rocket is the drawing function, which simply takes in
the state of the world and draws the world accordingly.

Put all the functions you have defined in the interactions panel and
you should see your animation once you run it!
