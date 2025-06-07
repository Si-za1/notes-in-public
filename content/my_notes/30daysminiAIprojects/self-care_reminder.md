---
title: self-care_reminder
draft: false
tags: []
---
 

## Self-Care Reminder – Threading and Timed Motivation

The goal was simple—build a self-care reminder app that shows motivational quotes at random times throughout the day. I wanted something minimal that stays running in the background and reminds me to take a breath, slow down, and reflect for a moment.

While experimenting with this idea, I discovered some interesting concepts, hit a few snags, and found surprisingly elegant solutions using built-in Python tools and the OpenAI API.

---

### Step 1: Random Timing

Initially, I found a library called `randomtimestamp`, thinking it would help me generate a future random time within a day. While the library does its job, it was returning long-form timestamps and I didn’t need that much detail or complexity. I only needed a delay—some amount of time in seconds or minutes—before the reminder shows up.

This is where Python’s `random.randint` and `time.sleep()` came into the picture. They turned out to be all I needed. I defined a function that picks a random delay between two values (in minutes), then converted that to seconds:

```python
def alert_time(min_minutes=1, max_minutes=1):
    return random.randint(min_minutes * 60, max_minutes * 60)
```

If both `min_minutes` and `max_minutes` are set to 1, the reminder will pop up exactly after 1 minute every time.

---

### Step 2: The Problem of Sleep

Once I had the timing figured out, the next problem was obvious. If I use `time.sleep()` for 60 minutes (or even a few), the whole script would be blocked. That meant I wouldn’t be able to run anything else or quit the app easily. The script would be stuck waiting.

This is when I recalled something from my Operating Systems class back in my bachelor's—**threading**.

Threading lets you run a function in the background while keeping your main program responsive. It's like having a side-task running silently without freezing your main application.

So I created a thread that waits and sends reminders independently. Here’s how the loop works:

```python
def loop_time():
    while True:
        delay = alert_time(1, 1)
        print(f"⏳ Waiting {delay // 60} minute(s)...")
        time.sleep(delay)
        reminder_generation()
```

And the thread that runs it:

```python
reminder_thread = threading.Thread(target=loop_time)
reminder_thread.daemon = True
reminder_thread.start()
```

---

### Step 3: Generating the Reminder

The quotes themselves are generated using OpenAI’s API. I used the `gpt-4o` model and asked it to behave like a short motivational quote generator based on a genre or vibe. For now, I’ve set it to “emotionally intelligent,” but it can be anything—calm, kind, powerful, spiritual, funny.

Here’s the function that takes care of that:

```python
def reminder_generation():
    response = openai.ChatCompletion.create(
        model="gpt-4o",
        messages=[
            {"role": "system", "content": f"You are a motivational and inspirational quote generator. Generate a quote that is {user_choice}, under 50 words."},
            {"role": "user", "content": "Give me a unique quote based on the theme."}
        ]
    )
    quote = response.choices[0].message["content"]
    print(f"\n💬 Reminder: {quote}")
```

This ensures every reminder feels personalized, fresh, and encouraging.

---

### Reference

Threading was the game-changer here. For a solid understanding of how it works and when to use it, I recommend reading this [Threading in Python tutorial on DataCamp](https://www.datacamp.com/tutorial/threading-in-python).

---

### Conclusion

This project started as a small idea—to remind myself to pause during the day. But it helped me revisit core programming concepts like time handling, concurrency, and API integration. I now have a minimal, functional self-care reminder that runs silently in the background and occasionally nudges me with thoughtful affirmations. No UI, no distractions—just simple, clean motivation delivered on time.

Next steps might include adding desktop notifications or logging the quotes to a file for reflection. But for now, this works, and that’s enough.

Stay tuned. More to come.

Code: [Self care reminder](https://github.com/Si-za1/python_for_beginners/blob/30daysai/30daysAI/day3.py) 