---
{"tags":["Games/Design","Creative"],"publish":true,"PassFrontmatter":true}
---



<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/1-Rough-Notes/Pong-in-Godot#Information" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



# Information

## Godot Nodes
As it turns out Godot has the entire functionality of its engine working inside of a series of nodes working all the way to a god node. Then I make scripts within it that can be controlled.

The node system works like this:
- Scene
	- Player (Script can be attached directly like this)
		- Collision
		- Sprite
	- Enemy
		- Collision
		- Sprite

Each bullet point would represent a node and each node has the ability to have its own script.
## Controlling a sprite
Before I can do anything, I need to be able to control a sprite in Godot. So, how do I do that?

> [!INFO]
> I realized that this isn't the first thing I should have thought of, as you can [see](#Godot%20Nodes) I backtracked a bit.

What I gathered is that from the top toolbar going from:
Projects > Project Settings > Input Map
I can add controls that the scripts in the nodes can pull from to be activated at that particular part of the node.

For example:
I have a Player node structured like so:
- Player
	- Sprite
	- Collider

In the player, I added a script that says this:
```gdscript
extends Actor

func _physics_process(delta):
	Input.get_action_strength("move_up")

```

>[!INFO]- extends Actor
>This makes this piece of code have the functionality of another script too.

>[!INFO]- func _physics_process(delta):
>This is what reruns the code over and over again somewhere between 30-60 times per second depending on what the framerate it set to

The important part of this is the: **Input.get_action_strength("move_up")**
What this does is it grabs the input we got from the input map from earlier and gives us a number between 0 and 1 depending on how much that particular input is being activated. With a key, it's straight up 0 or 1, but an analog stick would give us something in between usually.

### Constraints
When it comes to movement sometimes you want to lock down a particular sprite's position when moving around. To do that you would use "clamp" to make it so that it can't move out of a range you clamp it around which appears like so:
```gdscript
position.x = clamp(position.x, 0, 100)
//This would stop the position from moving outside of the range of 0 and 100 on the x axis.
```
Clamp can also be used with any other variable, it's not just limited to position or movement. You could make it with just a simple Int variable.

## Collisions
To make a piece a code respond to certain objects you need to identify all the objects colliding with it then you can use that array to pull out what data you want from it and have your code respond accordingly an example of this is demonstrated here:
```gdscript
for index in get_slide_count():
	var collision = get_slide_collision(index)
	if collision.collider.is_in_group("players"):
		print("Players was collided with!")
	if collision.collider.name.begins_with("Name")
		print("Name was collided with!")
	if collision.collider is RigidBody2D:
		print("A type was collided with!")	
```
Another way is by adding an area2D node and a CollisionShape2D node to that area 2D node so that it has an actual shape. Then on the top right of Godot click on Node>Signals>body_entered and then connect it to the script that you want, anything inside this function will run whenever something hits the shape you fitted with your CollisionShape2D:
```gdscript
func _on_Area2D_body_entered(body):
pass
```

>[!INFO]- body
>Body refers to the object that the Area2D node interacted with

## Signals
Sometimes you want to be able to have your code interact with other pieces of code without needing to rely on using the specific node you're working on all the time. That's where signals come in. They allow you to fire a message out into the open, and you can set up another node to look for that message, to then respond to that message if it sends it out. The way to make your own custom message to fire is by first:

```gdscript
signal messageName(extraOptionalDataToPass, anotherOptionalPieceOfData)
```
It acts just like a method, but to send that signal out in the open, you would then do:
```gdscript
emit_signal("messageName", extraOptionalDataToPass, anotherOptionalPieceOfData)
```

> [!NOTE] messageName
> What's in quotes in "emit_signal" must be the signal name that matches what you created when you made the "signal messagename" from the first section of code above if that is the message you want sent out into the ether.

To then receive that signal by another script, there are two ways to connect the messages. The easiest way is to select the node that script is attached to and click: 
Node>Signals>The signal you want to connect to another script>Connect
Then a function will be autopopulated inside of the new script you connected it to that will be called whenever the message from the signal sender sends it.

If you want to connect a signal through code, you can do so by using the `_ready()` function to grab and connect the desired node:
```gdscript
func _ready():
    var desiredNodeToConnectTo = get_node("DesiredNode")
    desiredNodeToConnectTo.connect("signalName", self, "_name_Of_Signal_Function")
```

</div></div>


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/1-Rough-Notes/Solitaire-in-Godot#Information" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



# Information

## The Mouse
The mouse has multiple qualities that can be controlled for inputs and outputs. 

The inputs include:
- The buttons
- The mouse sensor
The outputs include:
- The button states
- The mouse position


</div></div>

