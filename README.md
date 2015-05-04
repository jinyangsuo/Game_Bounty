# Game_Bounty
Text-Based Adventure Game
For this project you will be implementing an agent to play a simple text-based adventure game. The agent is required to move around a rectangular environment, collecting tools and avoiding (or removing) obstacles along the way. The obstacles and tools within the environment are represented as follows:

Obstacles  Tools
T 	tree      	a 	axe
*	wall	d	dynamite
~	water	B	boat
g	gold
The agent will be represented by one of the characters ^, v, <  or  >, depending on which direction it is pointing. The agent is capable of the following instructions:

L   turn left
R   turn right
F   (try to) move forward
C   (try to) chop down a tree, using an axe
B   (try to) blast a wall, door or tree, using dynamite

When it executes an L or R instruction, the agent remains in the same location and only its direction changes. When it executes an F instruction, the agent attempts to move a single step in whichever direction it is pointing. The F instruction will fail (have no effect) if there is a wall or tree directly in front of the agent.

When the agent moves to a location occupied by a tool, it automatically picks up the tool. The agent may use a C or B instruction to remove an obstacle immediately in front of it, if it is carrying the appropriate tool. A tree may be removed with a C (chop) instruction, if an axe is held. A wall or tree may be removed with a B (blast) instruction, if dynamite is held.

If the agent moves forward into the water, it will drown unless it is in a boat. Boats behave a bit differently from the other tools, because they always remain in the water. When the agent moves from the water back to the land, it automatically drops the boat. The boat will then remain where it was dropped, ready to be picked up again at a later time.

If the agent attempts to move off the edge of the environment, it dies.

To win the game, the agent must pick up the gold and then return to its initial location.

Running as a Single Process

Copy the archive src.zip into your own filespace and unzip it. Then type

cd src
javac *.java
java Bounty -i s0.in
You should then see something like this:
~~~~~~~~~~~~~~~~~~~
~~~~~~~~~~~~~~~~~~~
~~ a T T     T T B~
~~   ***     ****~~
~~***     v     *~~
~~  **         **~~
~~ g **   d   **~~~
~~    **     **~~~~
~~~~~~~~~~~~~~~~~~~
~~~~~~~~~~~~~~~~~~~

Enter Action(s): 
This allows you to play the role of the agent by typing commands at the keyboard (followed by <Enter>). Note:
an axe can be used multiple times, but each dynamite can be used only once.
C or B instructions will fail (have no effect) if the appropriate tool is not held, or if the location immediately in front of the agent does not contain an appropriate obstacle.
Running in Network Mode

Follow these instructions to see how the game runs in network mode:

open two windows, and cd to the src directory in both of them.
choose a port number between 1025 and 65535 - let's suppose you choose 31415.
type this in one window:
java Bounty -p 31415 -i s0.in
type this in the other window:
java Agent -p 31415
In network mode, the agent runs as a separate process and communicates with the game engine through a TCPIP socket. Notice that the agent cannot see the whole environment, but only a 5-by-5 "window" around its current location, appropriately rotated. From the agent's point of view, locations off the edge of the environment appear as a dot.
We have also provided a C version of the agent, which you can run by typing

make
./agent -p 31415
Writing an Agent

At each time step, the environment will send a series of 24 characters to the agent, constituting a scan of the 5-by-5 window it is currently seeing; the agent must send back a single character to indicate the action it has chosen.

You are free to write the agent in any language you choose. If you are writing in Java, your main file should be called Agent.java (you are free to use the supplied file Agent.java as a starting point). If you are writing in C, you are free to use the files agent.c, pipe.c and pipe.h as a starting point. In other languages, you will have to write the socket code for yourself. You must include a Makefile with your submission, producing an executable called agent.

You may assume that the specified environment is no larger than 80 by 80, but the agent can begin anywhere inside it.

