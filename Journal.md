# Journal 
**Homework Tuesday, 3 February 2026**

## Revisiting the project from ~2 years ago

I wasn’t present when the Scene Shop was open to closely inspect how components were arranged. Because of this, my understanding is based on general observation rather than direct inspection of the physical setup. This makes it difficult to know how the project was intended to behave at every stage.

From what I can tell, from afar, the project looks like its perfectly fine but a closer look would say otherwise; Some behaviors are hard to classify as broken or intentional, largely because the wiring, component placement, and expected timing are not clearly visible, which is a plus on the students' end. When something appears unresponsive or unclear, it’s difficult to tell whether the issue comes from hardware reliability, software logic, or simply subtle design choices.

If I were to begin debugging this project, I would start by testing each output element in isolation to confirm that it activates consistently and at the correct time. I would then trace the full sequence step by step, adding temporary indicators such as LEDs or serial messages to show which stage is currently active. This would help narrow down where failures or inconsistencies occur. Debugging is made harder by the fact that everything is embedded into one continuous sequence, so a failure early on can affect everything that follows. Clear state separation and better documentation of expected behavior would make the process much easier.

In some cases, the project may actually be functioning as designed but still feel confusing to a participant. If the sequence progresses slowly or with minimal feedback, users may assume something is wrong even when it is not. In that sense, some of the issues seem less like malfunctions and more like design problems related to feedback, pacing, and clarity.

## New project exploration — early ideas

This section is a very early and rough exploration rather than a final commitment. I’m interested in building a "The Last of Us" module.

One idea draws inspiration from *The Last of Us*, focusing on atmosphere rather than direct gameplay mechanics. The project would feel slow, tense, and deliberate, using light, sound, and timing to suggest movement through a hostile or decayed environment. The sequence would unfold gradually, layering sensory elements to create a sense of anticipation and emotional weight. Instead of rewarding speed or precision, the experience would emphasize waiting, listening, and feeling the passage of time.

Another idea I’m considering is a DDR-inspired physical game. Where when the button is pushed, Arrows would randomly rize up and maybe we could add a fun easter egg where if the player pushed the button when the arrows hit their target, a sound would play along with a "+100 pts!" sign would pop up. Pretty simple but I think it would depend on what the entire class would go for. I think "The Last of Us" would be great if everyone's doing an action game, otherwise DDR is fun enough for me.
