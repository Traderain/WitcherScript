Latent functions
===========================
This page will explain what is a latent function, why would you use a latent function and how to use them.

What is a latent function
-------
Latent function are functions whose execution time can occur over many frames. To quote the UnrealEngine documentation of latent functions:
*Latent functions let you manage complex chains of events that include the passage of time*. Because with latent function you cait wait for any amount of time before
doing what you want, and you don't have to worry too much about your function being too slow because it won't freeze the game and instead execute over many frames/seconds.

The only downside of such functions is that only an entry function or a latent function can call another latent function. But we'll see later how to work around this and adapt
the way we write our code to use the full power of latent functions.

**Technical explanation**

You can skip this part if you do not want to understand exactly how the latent functions work.

Most game engines use two or more threads for their games to keep everything smooth. The first thread, often called the *rendering thread* has one job: send the frames
data to the gpu as frequently as possible. While the other threads to the heavy lifting, they do all the calculation needed for the game and update the data used by the rendering thread.

This technique was created to keep a high framerate even when there are lots of moving parts in the game. Even if a function is slow it won't delay the next frame or even worse freeze the game,
instead the rendering thread will continue updating the images while the other threads take their time to update the data. This way the users keep their 60 frames per seconds even
in complicated scenes.

So what is a latent function? It is a function that comes with his own thread. Because when you call a simple function that is not latent, high are the chances it will be
executed in the rendering thread. And doing things in the rendering thread is not a good idea, unless you want to impact your users' framerates. Of course not each latent function
comes with one thread, whenever you call a latent a function from another latent function both will use the same thread.

Obviously we can't know exactly how the red engine works, but after seeing functions like 
::
 // Kill internal state thread ( LATENT and ENTRY only )
 import latent function KillThread();
::
we can deduce it works like any other game engine in the world.

Why use a latent function
-------
When inside latent functions you can call other latent functions and the engine offers two interesting functions you can use when developping your mods:

- `Sleep(seconds: float)`
- `SleepOneFrame()`

These two functions allow you to control the game over the time. You can tell to do one action, wait 10 seconds and do the same action again. You should also prefer
doing the heavy work in latent function to avoid freezing the game.

So my advice would be to use latent functions whenever possible.

How to use a latent function
-------
