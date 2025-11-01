---
title: "Coroutines: What are they? How do they work?"
dg-publish: "true"
---
I am super excited for today’s article because we are going to dive into one of my favorite topics in Unity: Coroutines! In this article, we won’t go too in depth as I want to keep this consumable for beginners, but I will _very likely_ dive deeper into Coroutines and how they work under the hood in a future article because I just find them so fun!

We’ll use Coroutines to spawn our enemies infinitely in our game!
![[coroutine_basics_01.gif]]

First, lets create a new GameObject that we’ll call **Spawn_Manager** and create a new script for it called `SpawnManager`. Be sure to add the newly created component to your **Spawn_Manager** game object:
![[Pasted image 20251101121751.png]]
Before we get into code, I want to explain a couple of basic concepts here. First of all, what is a Coroutine?
### Coroutine
A Coroutine is essentially a block of code that gets run over multiple frames in your game. Traditionally when you write code, it will run from top to bottom until it is finished executing and any other code after it will have to wait until it’s finished. Often times, we want code to run over the course of, say, a few seconds before we make something happen while also letting the next block of code run like normal. We achieve this by using Coroutines in Unity.

Let’s go to our `SpawnManager` script and I’ll show you what a basic Coroutine looks like:
![[Pasted image 20251101121814.png]]
So we have a method that we are calling `CO_SpawnRoutine()`, eventually we’ll use this method to spawn our enemies at a specific interval. Something to note is that I like to prefix my coroutines with `CO_`to denote that it’s a Coroutine. You’ll notice a few things about this special-looking method.

The first thing is this weird `IEnumerator` that we are adding to our method signature instead of `void` which we are used to. What this basically means is that our method returns an object of type `IEnumerator` but for our purposes and to keep things simple, assume that methods with `IEnumerator` as their return types are Coroutines. We need that so that Unity knows we want to use a Coroutine.

The next weird thing is this `yield return` line. The `yield` keyword is a C# keyword that you must use whenever you are writing a method that returns an `IEnumerator`. This tells the compiler to let code run after this method is called once it hits the `yield` part of the method’s execution. Its a little tricky to understand, so I wouldn’t let yourself get too caught up with it. For now, just know that the `yield return new WaitForSeconds(5);` line does just what you’d expect. It waits 5 seconds before going on to the next line which is our print statement that says “5 seconds have passed!”.

Finally in our Start method, we have the `StartCoroutine()` method, and in it we pass in our coroutine method. In Unity, you have to tell the engine when you want to run a Coroutine. In this case, we will run it at the start of the game. If we run this then “5 seconds have passed!” will get printed in the console after 5 seconds: