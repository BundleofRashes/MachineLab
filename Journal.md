# Journal 
**Homework Tuesday, 16thFebruary 2026**

### Ideas for Mechanisms

We have a shared google doc that we wrote down potential ideas for our final project which had very strong and very much doable concepts and ideas. However, for this specific assignment, we had to focus on two (or more) mechanisms. Sara came up with the ideas:

We'd do four main ideas that we'd hopefully build on for our final:
- 1. An updated minecart rail that speeds up when it reaches a certain rail.
- 2. A TNT block that shakes/vibrates, like it is about to explode
- 3. A Furnace that lights up, indicating that something is cooking.
- 4. A chest that closes and opens repeatedly.

 ## Mechanisms:

### Minecart

Sara had already built the minecart and she wanted to fix, debug and add something to her older mechanism in order for it to speed up when it reaches the special rail. What she ended up doing was adding a light sensor to the trail the minecart was spinning on, specifically on the special rail so that when the minecart does hover over it, The light sensor would detect that it is darker which would tell the motor to speed up.


### TNT
 
For the TNT part, Stefania built it and attached a servo motor on the bottom of it and wrote the code for it to viberate. She had to leave early and she couldn't figure out the debuging part before leaving. I figured out that the issue was not in the code but it's in the jumper wires (I understand the hate towards them now), I did have too tweak a bit of the code for it to look like it was vibrating; The premise of the code was that the motor would add then subtract -5 degrees which was too slow for the illusion of vibration so I simply changed the -5 to a -2 and +2 and it worked. Although I still think it needs a better motor but thats a problem for future Rashed :)

### Chest

For the chest part, I struggled with figuring out how to DIY a hinge because I could not get an idea on how i'd make the chest open AND close without a hinge. After much thinking and waiting for my singular brain cell to work, I realized that I don't necessarly need a HINGE hinge, I can make the servo motor act like one for now! I attached the servo motor to the back of the chest and coded the motor to start from 90 degrees and more to 0 degrees, pause for two seconds, go to it's intial position of 90 degrees, wait for another two seconds and repeat! I (surprisingly) didn't face any issues with my arduino which is always a pleasure since all arduinos have done is be evil and possessed by demons from evil town.


### Furnace

I was not present when this was built, but it looks cool!


















**Homework Thursday, 5 February 2026**

## Motor Exercise

### What I Built
I wired the DC motor to the L298N motor driver and connected:
- Enable pin (enA) to PWM pin 9
- IN1 to pin 8
- IN2 to pin 7
- Push button to pin 4
- Potentiometer to A0

The potentiometer smoothly controls speed from 0–255 using PWM.  
The push button toggles the motor’s direction each time it is pressed.

## Demo Video

[![Motor Demo](https://img.youtube.com/vi/jU8DkR8hZ6A/0.jpg)](https://youtube.com/shorts/jU8DkR8hZ6A)


## Issues I Encountered
At first, the motor did not change direction consistently. I realized the issue was with how the button press was being read. Without proper debounce handling, the state would sometimes flip multiple times.

I fixed this by:
- Adding a toggle variable (`pressed`)
- Waiting until the button was released using a `while` loop
- Adding a small delay to debounce

After that, the direction switching worked :p


## Arduino Code


// --- Define your pins here ---
const int enA = 9;      // PWM pin for speed control
const int in1 = 8;      // Direction pin 1
const int in2 = 7;      // Direction pin 2
const int button = 4;   // Push button pin
const int potPin = A0;  // Potentiometer pin

int rotDirection = 0;
int pressed = false;

void setup() {
  pinMode(enA, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(button, INPUT);

  // Set initial rotation direction
  digitalWrite(in1, LOW);
  digitalWrite(in2, HIGH);
}

void loop() {
  int potValue = analogRead(A0); // Read potentiometer value
  int pwmOutput = map(potValue, 0, 1023, 0 , 255); // Map to 0–255
  analogWrite(enA, pwmOutput); // Send PWM signal

  // Read button - Debounce
  if (digitalRead(button) == true) {
    pressed = !pressed;
  }

  while (digitalRead(button) == true);
  delay(20);

  // Change rotation direction
  if (pressed == true && rotDirection == 0) {
    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    rotDirection = 1;
    delay(20);
  }

  if (pressed == false && rotDirection == 1) {
    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    rotDirection = 0;
    delay(20);
  }
}

**Homework Thursday, 5 February 2026**

## Sketching Idea

I chose two games and I will explain the main component for Each Below:

*The Last of Us:

One thing that is very prominant in the Series, game, and comics is the cordyceps and how they grow (They're the main virus that, when started spreading, turned everyone into clockers, zombies, etc..) But, a visual that is used in all of these is when it grows. [see the show opening credits for reference](https://www.youtube.com/watch?v=8SWhBsbxmpk)
What I was thinking is to have a thin line of wood that acts like a branch in a tree and when you'd press the button, it'd make vines slowly apprear from the back and they start at the bottom but add more and more. These are attached to motors that slowly move and reveal the cordyceps.

*Dance Dance Revolution (Project D1va)

This one's pretty simple, __Four belt-and-roller system__ and each one would have an arrow attached to it like in the game and they'd move according to the music that's played.

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
