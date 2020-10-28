
Latent functions
===========================
This page will explain what is a latent function, why would you use a latent function and how to use them.

What is a latent function
-------------------------
Latent function are functions whose execution time can occur over many frames. To quote the UnrealEngine documentation of latent functions:
*Latent functions let you manage complex chains of events that include the passage of time*. Because with latent function you cait wait for any amount of time before
doing what you want, and you don't have to worry too much about your function being too slow because it won't freeze the game and instead execute over many frames/seconds.

The only downside of such functions is that only an entry function or a latent function can call another latent function. But we'll see later how to work around this and adapt
the way we write our code to use the full power of latent functions.

**Technical explanation**: You can skip this part if you do not want to understand exactly how the latent functions work.

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
-------------------------
When inside latent functions you can call other latent functions and the engine offers two interesting functions you can use when developping your mods:

- ``Sleep(seconds: float)``
- ``SleepOneFrame()``

These two functions allow you to control the game over the time. You can tell to do one action, wait 10 seconds and do the same action again. You should also prefer
doing the heavy work in latent function to avoid freezing the game.

So my advice would be to use latent functions whenever possible. But the amount of code you have to write to be able to use a latent function may sometimes be not worth the effort, if you're writing a small and supposedly fast function you may not need to write twice the amount of code for it. It's up to you at this point.

How to use a latent function
----------------------------

In order to be able to use call a latent function you must either be in an entry function or another latent function. So in short you must know how to create entry functions to
be able to use latent functions.

So what's an entry function. An entry function can only be inside a state of a statemachine class. Imagine the following statemachine class:
::
 // statemachines should extend CEntity to gain access to useful methods
 statemachine class StateMachineExample extends CEntity {
  public var delay: int;
  default delay = 10;
  
  public function start() {
   this.GotoState("ExampleState");
  }
 }
::

Once you're in a statemachine you can tell your class to enter in a ``state``, in the example we can see the class enters the ``ExampleState`` state.
Once you've done that you can write your state like so:
::
 state ExampleState in StateMachineExample {
  event OnEnterState(previous_state_name: name) {
   this.entryFunctionExample();
  }
  
  entry function entryFunctionExample() {
   this.latentFunctionExample();
  }
  
  latent function latentFunctionExample() {
   Sleep(parent.delay); // access the parent's variable
  }
 }
::

A state is declared like a class, but with the ``state`` keyword instead. It acts almost like a class, meaning you can add attributes to the state and you can even extends another state.

In a state everything starts from the event ``OnEnterState`` that is called everytime the statemachine enters this specific state. And from this event you can call the entry functions you declared, and then the latent functions.

As you can see it is not **that** complicated to use latent functions. But the overhead of writing a statemachine and using states simply to use a latent function may not be worth the hassle. Note that many latent functions available in the scripts come in the synchronous version too, but these function will cause the game to freeze while they
execute. A good example are the two functions ``function LoadResource`` and ``latent function LoadResourceAsync``, both do the same thing but one is synchronous and freezes
the game while the game loads the resource from the disk (a good second depending your disk speed) while the other is latent and doesn't cause any hiccup. 
