Exec functions
===========================

Exec functions are the simplest way to introduce custom code into Witcher 3. As handy as they are, it is important to remember their limitations:


**An exec function cannot:**

- Be called from code
- Be latent (have any execution time or delays)
- Loop (as they cannot be called from code)


Creating custom exec function
-------

Go to your Witcher 3 installation folder, inside "Mods" folder, create new folder called "modExecFunctionTest", 
inside that folder create another folder called "content", go into it and create another folder called "scripts" and inside that folder create a folder called "local".
Inside that folder create file called "latentfunction.ws" (make sure it's .ws not .ws.txt).

In short, your folder hierarchy should look as following:
::
 The Witcher 3 Wild Hunt GOTY\Mods\modExecFunctionTest\content\scripts\local\latentfunction.ws

Open the file with text editor of your preference (Notepad++ is strongly recommended)
and add following code inside:
::
 exec function printmystring(var : String)
 {
  GetWitcherPlayer().DisplayHudMessage(var);
 }
::

save the file and run the game, once you open console using "~"(tilde) key, you can write:
::
 printmystring("Praise Kek!")

To see your string printed using game's default HUD message module.

Of course this is one of most simple examples imaginable. Exec functions are good for any kind of instantaneous work that needs
to be done manually and single time (or not that often) which makes it naturally good for things like:

- Spawning entities
- Removing entities
- Getting some data from the game
- Setting some variables within other classes
