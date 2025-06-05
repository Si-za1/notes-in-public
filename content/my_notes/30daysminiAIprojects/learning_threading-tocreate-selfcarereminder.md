---
title: learning_threading-tocreate-selfcarereminder
draft: false
tags:
  - 30daysai
  - complete
---
The plan is to create a self-care reminder.  
Something simple.  
A tool that generates a reminder at a random time during the day.  
To generate the reminder, I'm using OpenAI.  
Sounds simple.

While building it, I came across a library called `randomtimestamp`. It looked simple at first, but the way it was generating time felt a bit off—too long-winded and a bit confusing.

So I dug a bit deeper and realized `datetime` is what I should actually be using. That helped simplify one part of the problem.

Then I moved on to thinking about how to code the reminder. The idea was: generate a random time, and when that time comes, display the reminder. Maybe repeat every hour or so.

That’s when I realized—if I just set a timer for 1 hour using `time.sleep()`, the entire app would just pause and do nothing else during that time. That didn’t sit right with me.

So I started looking into how other apps manage this. How they keep running while waiting for something to happen in the background.

That’s when I came across `threading`.  
I remembered studying it back in my OS classes during undergrad.  
Didn’t really pay attention to it then.  
Now it made perfect sense.

Threading lets you run parts of your program independently, at the same time.

You’ve got your main program doing its thing—maybe waiting for user input, maybe logging something, maybe just existing. And then you’ve got this separate part that needs to wait… and when the time’s right, it does something—like shows a reminder.

If you don’t use threading, and you try to wait (with `time.sleep()`), your entire program just… freezes. Nothing happens until the sleep is over. That’s a problem. Especially if you want to add more features later, like user interaction, or a live log, or mood tracking.

So threading helps. You give the reminder its own thread.  
It lives in the background.  
It waits on its own.  
It doesn’t block the main thread.

In Python, this is how it might look like and works:


`import threading`  
`def reminder():`       
 `time.sleep(3600)`     
 `print("Reminder: check in with yourself")`  
 `thread = threading.Thread(target=reminder)` 
 `thread.start()`

What happens here is simple:  
The main program moves on immediately.  
Meanwhile, the `reminder()` function does its thing—waiting and then printing—without freezing everything else.

And it’s not just about printing.  
You could later send notifications, write to a file, update a UI, anything.

You also don’t have to stop at one thread.  
You can run multiple threads.  
Each handling their own jobs—maybe hydration reminders, posture checks, breathing exercises—all running independently.

Now, threading isn’t perfect. There’s complexity if threads need to talk to each other or share resources. But for something like a self-care reminder that works mostly in isolation, it’s exactly what you need.

This is the kind of stuff that makes your app feel light.  
Feels like it’s alive.  
Not frozen.  
Just doing its job in the background, quietly.

That’s why threading made sense.  
That’s why I decided using it.

---
Stay tuned.  
I'll drop the code on Day 6.
Reference: [Threading in Python – A Complete Tutorial by DataCamp](https://www.datacamp.com/tutorial/threading-in-python)