# Curio One FTC Programming: Zero to Hero

*A course for new team members. Based on `curiooneftc/FtcRobotController` (FTC SDK 11.1) and `curiooneftc/CurioControl` (our framework).*

## 0. How this course works

The course has seven parts. Do them in order; each one builds on the last.

| Part | You will learn | Time |
| --- | --- | --- |
| 1 | Android Studio: install, clone, build, deploy | 1 evening |
| 2 | Java basics, only what a robot needs | 2 sessions |
| 3 | The FTC SDK: OpModes, gamepads, motors, telemetry | 2 sessions |
| 4 | Autonomous and sensors: encoders, IMU, servos | 2 sessions |
| 5 | CurioControl: our framework (subsystems, PID, commands) | 3 sessions |
| 6 | Practice plan, debugging checklist, team rules | ongoing |
| 7 | Using AI to learn faster without switching your brain off | 1 session, then ongoing |

**Rule of the course:** never copy code you do not understand. Type it, run it, change one thing, and see what happens.

### The two repositories

- **FtcRobotController** is our copy of FIRST's official SDK app. The `TeamCode` folder is empty on purpose; that is where robot code goes. Everything outside `TeamCode` belongs to FIRST, so do not edit it.
- **CurioControl** is a library that sits on top of the SDK. It removes the repetitive code every season (motor setup, drive math, PID, command scheduling). Parts 1 to 4 do not need it. Part 5 does.

---

## Part 1. Android Studio

Android Studio is the program we write, build, and deploy robot code from. It looks big, but you will use about ten percent of it.

### 1.1 Install

1. Install **Android Studio Ladybug (2024.2) or newer**. Our repo's own readme requires this.
2. Install **Git** (and optionally GitHub Desktop if you prefer clicking to typing).
3. Make a GitHub account and ask a lead to add you to the `curiooneftc` organization.
4. Let Android Studio install its recommended SDK components on first launch.

### 1.2 Get the code

1. Open Android Studio, choose **Get from VCS** (or File > New > Project from Version Control).
2. URL: `https://github.com/curiooneftc/FtcRobotController.git`
3. Pick a folder with no spaces in the path, then click **Clone**.
4. Wait. The first **Gradle sync** downloads a lot and can take several minutes. The progress bar is at the bottom right. Do not click around until it finishes.

### 1.3 Find your way around

Switch the left panel from "Project" to **Android** view (dropdown at the top of the panel).

| Folder | What it is | Edit it? |
| --- | --- | --- |
| `FtcRobotController` | FIRST's app plus sample OpModes | No (read samples, copy from them) |
| `TeamCode` | **Our robot code** | Yes |
| `Gradle Scripts` | Build configuration | Only a lead, and only on purpose |

Our code lives in `TeamCode/java/org.firstinspires.ftc.teamcode`. The samples live in `FtcRobotController/java/org.firstinspires.ftc.robotcontroller/external/samples`. They are the best free textbook you have; names start with `Basic`, `Sensor`, `Concept`, or `Robot`.

### 1.4 Make your first class

1. Right-click the `teamcode` package > **New > Java Class**.
2. Name it `HelloTeleOp` (class names start with a capital letter, no spaces).
3. Paste in the program from Part 3.1.

### 1.5 Build and deploy to the robot

**Option A: USB.** Plug the Control Hub into your computer with USB-C. It should appear in the device dropdown next to the green Run button.

**Option B: Wi-Fi.**

1. Power the Control Hub. Join its Wi-Fi network (named `FTC-xxxx`) from your computer.
2. Open the Terminal tab at the bottom of Android Studio and run `adb connect 192.168.43.1:5555`.
3. The Control Hub should now appear in the device dropdown.

Then:

1. Make sure the run configuration (dropdown left of the device) says **TeamCode**.
2. Click the green **Run** triangle.
3. Watch the **Build** tab. When it says success, the app installs on the Control Hub.
4. On the Driver Hub, pick your OpMode from the list and press INIT, then the Play button.

### 1.6 Shortcuts worth learning today

(On Mac use Cmd instead of Ctrl.)

| Shortcut | What it does |
| --- | --- |
| `Alt+Enter` | **Quick fix.** Red underline? Press this first. It adds missing imports and fixes many errors. |
| `Ctrl+Space` | Autocomplete (shows what methods exist) |
| `Ctrl+Click` on a name | Jump to where it is defined |
| `Shift` twice | Search everywhere (files, classes, settings) |
| `Ctrl+Alt+L` | Auto-format your code |
| `Ctrl+/` | Comment or uncomment lines |
| `Ctrl+Q` | Show documentation for what the cursor is on |

### 1.7 When things go wrong

- **Red underline in the code:** hover over it to read the error, then try `Alt+Enter`.
- **Build fails:** open the **Build** tab and read the *first* error, not the last. The rest are usually fallout.
- **Everything is red after pulling:** File > **Sync Project with Gradle Files**.
- **Still weird:** File > Invalidate Caches > Invalidate and Restart. (Slow, but it fixes a surprising number of ghosts.)
- **Robot code crashes at runtime:** open the **Logcat** tab, filter by `RobotCore`, and look for the red line with the exception name.

### 1.8 Git rules for the team

Two people editing the same file is how code gets lost. Follow these:

1. **Pull before you start** (Git > Pull).
2. **Work on your own branch** named for the job, such as `intake-pid`. Never commit straight to `master`.
3. **Commit small and often** with a message that says what changed, like "Add arm preset positions".
4. **Push** at the end of every session so the work is not stuck on one laptop.
5. Ask a lead to review before merging to `master`.
6. **Never commit passwords or tokens.** If GitHub Packages needs a token, it goes in your personal `~/.gradle/gradle.properties`, never in the repo.

### Git for total beginners

**What Git and GitHub are**

Imagine your code folder is a video game. **Git** is the save system: whenever you like, you make a save point, you can go back to any earlier one, and you can see exactly what changed between two of them. **GitHub** is a website that keeps a shared copy of those saves so the whole team can use them. Git runs on your computer. GitHub lives online. They are different things that work together.

Why a team needs this: without it, three people edit the same file, email zip files around, and someone's work gets overwritten. With Git, everyone works on their own copy, and Git helps combine the copies afterwards.

**Words you will hear**

| Word | Plain meaning |
| --- | --- |
| **Repository (repo)** | The project folder plus its whole history of saves. We have two: FtcRobotController and CurioControl |
| **Clone** | Download a repo from GitHub to your computer for the first time |
| **Commit** | One save point, with a short message saying what changed |
| **Branch** | Your own parallel line of saves. Your changes stay on your branch and cannot disturb anyone else until you choose to combine them |
| **Push** | Upload your commits from your computer to GitHub |
| **Pull** | Download other people's new commits from GitHub to your computer |
| **Remote / origin** | The copy on GitHub. `origin` is just its nickname |
| **Pull request (PR)** | A request on GitHub saying: please review my branch and add it to the main code |
| **Merge** | Combine one branch into another |
| **Conflict** | Two people changed the same lines and Git cannot decide whose version wins, so it asks you |
| **Main branch** | The official, working version. It is called `master` in FtcRobotController and `main` in CurioControl |

**The four places your code lives**

```
  Your files  --stage-->  Staging area  --commit-->  Your computer's  --push-->  GitHub
  (you edit)              (changes you               history                     (shared)
                           picked)                                  <------ pull ------
```

You edit files. You pick which changes belong in the next save (**stage**). You save them with a message (**commit**). You upload the saves (**push**). Android Studio's Commit window combines staging and committing: you tick the files you want, write a message, and click Commit.

**A day of work, step by step**

Menu names change a little between Android Studio versions. If you cannot find something, press `Shift` twice and type its name.

1. **Pull first.** Menu: Git > Pull. (Terminal: `git pull`.) This gets everyone else's latest work so you start from the newest code.
2. **Make your own branch.** Menu: Git > New Branch, and name it after the job, like `intake-pid`. (Terminal: `git checkout -b intake-pid`.) Look at the bottom-right of the Android Studio window: it shows the branch you are on. **Check it before every commit.**
3. **Edit and test.** Write code, run it, fix it.
4. **Commit.** Open the Commit window (`Ctrl+K`, or the Commit icon on the left bar). Click a file to see the changes: green lines were added and red lines were removed. Read them. Tick the files you want, type a message, click **Commit**. (Terminal: `git status`, then `git add <file>`, then `git commit -m "message"`.)
5. **Push.** Menu: Git > Push (`Ctrl+Shift+K`). The first time, it creates your branch on GitHub. (Terminal: `git push -u origin intake-pid`.)
6. **Open a pull request.** Go to the repo on GitHub. A banner offers *Compare & pull request*. Write what you changed and why, and ask a lead to review. After approval, a lead (or you, if allowed) clicks **Merge**.
7. **Reset for next time.** Switch back to the main branch (Git > Branches) and pull again. Start the next job from step 2.

**Good commit messages**

A commit message is a note to your future self at 11 pm before a competition. Say what changed in plain words.

| Bad | Good |
| --- | --- |
| `stuff` | `Add arm preset positions to RobotConfig` |
| `fixed it` | `Negate right stick X so the robot turns the right way` |
| `final version 2 REAL` | `Tune lift PID: kP 0.012, kD 0.001` |

**What to commit, and what never to**

Commit your source code: the Java files and configuration you wrote. Never commit build output (the `build` and `.gradle` folders), your personal `local.properties`, large files, or any password or token. The repo's ignore file usually keeps most of these out, but always look at the list in the Commit window. If a file there looks strange, stop and ask.

**Merge conflicts without panic**

A conflict is not an error and you did nothing wrong. It means two people changed the same lines, and Git is asking a human to choose. Git marks the file like this:

```
<<<<<<< HEAD
double kP = 0.012;
=======
double kP = 0.015;
>>>>>>> intake-pid
```

The first version (above `=======`) is from the branch you are on. The second is the incoming one. You keep one, or combine them, and delete the three marker lines.

Android Studio makes this visual:

1. When a conflict appears, a dialog lists the files. Click **Merge**.
2. You see three panels. Left is your version, right is theirs, middle is the result you are building.
3. For each highlighted block, click the arrows to accept left, accept right, or both. You can also type directly in the middle panel.
4. When no conflicts remain, click **Apply**, rebuild the project, test it, then commit.

If you are not sure whose version is right, ask the other person. That conversation is the real fix.

**I made a mistake. What now?**

| Situation | What to do |
| --- | --- |
| I edited a file and want to throw my changes away | Right-click the file > Git > Rollback. This cannot be undone, so be sure |
| I want to see an older version of a file | Right-click the file > Git > Show History |
| Who changed this line, and why? | Right-click the line numbers > Annotate with Git Blame |
| I committed but have not pushed, and the message is wrong | Git tool window > Log > right-click the commit > Edit Commit Message |
| I pushed something bad | Do not erase history. Git > Log > right-click the commit > Revert Commit. That makes a new commit that undoes it |
| I committed on the main branch by accident | Stop. Do not push. Ask a lead |

Two rules: never run `git push --force`, and never run `git reset --hard` unless a lead has told you to. Both can destroy teammates' work.

**Terminal cheat sheet**

| Command | What it does |
| --- | --- |
| `git status` | Which files changed, and which branch am I on? |
| `git pull` | Get the latest from GitHub |
| `git checkout -b name` | Make a new branch and switch to it |
| `git add file` | Stage a file for the next commit |
| `git commit -m "message"` | Save a commit |
| `git push` | Upload my commits |
| `git log --oneline` | Show a short list of recent commits |
| `git diff` | Show exactly what I have changed |

**Practice: your first safe run**

1. Pull, then make a branch called `yourname-practice`.
2. Add a comment line to `HelloTeleOp` saying who you are. Commit it with a clear message.
3. Push, then open a pull request on GitHub. Do **not** merge it. Ask a mentor to look at it.
4. Conflict drill with a partner: both of you change the *same line* of a practice file on different branches. One merges first. The other pulls, gets the conflict, and resolves it in the Merge dialog.
5. Delete your practice branch when you are done.

### Checkpoint 1

- [ ] The project builds with no red errors.
- [ ] You have run a sample OpMode on a real Control Hub, or at least built it successfully.
- [ ] You made a branch, committed a change, and pushed it.

---

## Part 2. Java basics for robots

You do not need all of Java. You need these ideas.

**Start here if you have never programmed before**

A program is a list of instructions. The computer follows them from top to bottom, exactly as written, and it never guesses what you meant. Imagine giving directions to someone who does precisely what you say and nothing else. If you say "go to the corner", they stand still, because you did not say which way or how far. Programming is learning to be that precise.

Java is the language we write those instructions in. You type text, called **source code**. A program called the **compiler** reads it, checks it, and turns it into something the Control Hub can run. Android Studio and Gradle do this for you when you press Run.

There are three kinds of mistake, and knowing which one you have tells you where to look:

| Kind | When it shows up | What it looks like | Where to look |
| --- | --- | --- | --- |
| Compile error | Before the program runs | Red underline; the build fails | The Build tab, which names the file and line |
| Runtime error | While the robot program runs | The app crashes or stops | Logcat |
| Logic error | The program runs fine | It does the wrong thing, such as driving backward | Telemetry: print the numbers and look |

**How to read a line of code**

```java
motor.setPower(0.5);
```

Read it out loud as: *take the thing called `motor` and run its `setPower` action, handing it the number 0.5.* The part before the dot is the thing, the part after the dot is what to make it do, the brackets hold what you hand over, and the semicolon ends the instruction.

Symbols you will see everywhere:

| Symbol | Meaning | Example |
| --- | --- | --- |
| `;` | End of an instruction, like a full stop | `power = 1.0;` |
| `=` | Store the right side into the name on the left. It does **not** mean 'equals' | `int ticks = 537;` |
| `==` | Ask the question 'are these equal?' | `if (a == b)` |
| `( )` | Information handed to an action | `setPower(0.5)` |
| `{ }` | A group of instructions that belong together | the body of a method |
| `.` | 'belonging to' | `gamepad1.a` is the `a` button of `gamepad1` |
| `//` | A comment: ignored by the computer, written for humans | `// flip the stick` |
| `" "` | Text | `"frontLeft"` |

**Capital letters matter.** `Motor` and `motor` are different words to Java, and `frontLeft` is not `frontleft`.

**How to read an error message.** Do not panic and do not read the whole wall of text. Find the *first* error, the file name, and the line number:

```
error: cannot find symbol
  symbol:   variable motr
  location: class HelloTeleOp
```

Translation: 'on that line you used a name I do not know.' Here it is a typo of `motor`. Fix the first error, rebuild, and many of the others disappear on their own.

### 2.1 Variables and types

A variable is a named box that holds a value. You must say what *type* of value.

```java
int ticks = 537;            // whole numbers
double power = 0.75;        // decimals (motor power, distances)
boolean isPressed = true;   // true or false
String name = "frontLeft";  // text
```

Use `final` for values that must never change: `final double WHEEL_DIAMETER_MM = 96.0;`

### 2.2 Decisions

```java
if (gamepad1.a) {
    power = 1.0;
} else if (gamepad1.b) {
    power = -1.0;
} else {
    power = 0.0;
}
```

Compare with `==`, `!=`, `<`, `>`, `<=`, `>=`. Combine with `&&` (and), `||` (or), `!` (not).

### 2.3 Loops

A loop repeats code. Robot programs are mostly one big loop:

```java
while (opModeIsActive()) {
    // runs again and again until the match ends
}
```

### 2.4 Methods

A method is a named chunk of code you can reuse. It can take inputs and return an output.

```java
double clamp(double value, double min, double max) {
    if (value < min) return min;
    if (value > max) return max;
    return value;
}
```

Split big programs into small methods with clear names. `raiseArm()` beats twenty mystery lines.

### 2.5 Classes and objects

A **class** is a blueprint. An **object** is one thing built from it. A robot mechanism is a natural class:

```java
public class Claw {
    private boolean open = false;   // state the claw remembers

    public void toggle() {
        open = !open;
    }

    public boolean isOpen() {
        return open;
    }
}
```

`private` means "only this class can touch it". `public` means anyone can call it. Keeping details private is called **encapsulation**, and it is why big robot code stays manageable.

### 2.6 Inheritance and `@Override`

`extends` means "is a kind of", and it inherits everything from the parent. Every OpMode you write extends one the SDK gave you. `@Override` tells Java you are replacing a method from the parent:

```java
public class MyOpMode extends OpMode {
    @Override
    public void loop() {
        // your version of loop()
    }
}
```

### 2.7 Imports

Classes live in packages. `import com.qualcomm.robotcore.hardware.DcMotor;` tells Java where to find `DcMotor`. In Android Studio, `Alt+Enter` on a red class name adds the import for you.

### 2.8 Reading a whole OpMode, line by line

```java
package org.firstinspires.ftc.teamcode;   // which folder this file lives in

import com.qualcomm.robotcore.eventloop.opmode.OpMode;   // bring in the class we build on
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;   // bring in the menu label

@TeleOp(name = "Hello TeleOp", group = "Training")   // the name shown in the Driver Hub menu
public class HelloTeleOp extends OpMode {            // our class, built on the SDK's OpMode

    @Override                                        // I am replacing the parent's version
    public void init() {                             // runs once when you press INIT
        telemetry.addData("Status", "Ready");        // queue a line for the Driver Hub screen
    }

    @Override
    public void loop() {                             // runs about 50 times a second
        telemetry.addData("A pressed", gamepad1.a);
    }
}
```

- `public void init()` reads as: `public` means anyone can call it, `void` means it hands nothing back, `init` is its name, and the empty brackets mean it needs no information.
- **Where do `telemetry` and `gamepad1` come from?** We never created them. We got them for free by writing `extends OpMode`. The parent class already has them, and our class inherits everything its parent has. This is the most important idea in Part 2: you rarely build from nothing. You extend something that already works and replace only the parts you care about.
- **We never call `init()` or `loop()` ourselves.** The SDK calls them: `init()` once when you press INIT, then `loop()` over and over after Play. You fill in the *what*, and the SDK decides the *when*.

### 2.9 Where a variable lives (scope)

A variable only exists inside the curly braces where you created it.

```java
@Override
public void init() {
    DcMotor arm = hardwareMap.get(DcMotor.class, "arm");   // exists only inside init()
}

@Override
public void loop() {
    arm.setPower(1.0);   // ERROR: cannot find symbol 'arm'. loop() cannot see it.
}
```

The fix is to declare the variable at the top of the class, outside every method. That is called a **field**, and every method in the class can use it:

```java
private DcMotor arm;   // a field: lives as long as the OpMode

@Override
public void init() {
    arm = hardwareMap.get(DcMotor.class, "arm");   // no DcMotor in front: fill the existing field
}
```

**The trap:** if you write `DcMotor arm = ...` inside `init()` while a field called `arm` also exists, Java quietly makes a second, local `arm`. The field stays empty, and `loop()` crashes with a `NullPointerException`. `null` means 'points at nothing', and asking nothing to do something crashes the program.

### 2.10 Mistakes every beginner makes

| Mistake | What happens | Fix |
| --- | --- | --- |
| Forgetting a `;` | Compile error on that line or the next | Add it |
| A `{` with no matching `}` | A huge pile of errors | Click a brace to see its partner highlighted; `Ctrl+Alt+L` shows bad indentation |
| `=` where you meant `==` in an `if` | Error or wrong behaviour | Use `==` to compare |
| Whole-number division | `1 / 2` gives 0, not 0.5 | Make one side a decimal: `1.0 / 2` |
| Comparing text with `==` | Unreliable | Use `name.equals("arm")` |
| `int x = 0.5;` | Error: decimals do not fit in an `int` | Use `double` |
| Wrong capital letters | `cannot find symbol` | Match the name exactly |
| A field you never assigned | `NullPointerException` | Assign it in `init()` |
| Name in code differs from the Robot Configuration | Crash: cannot find device | Make them match exactly |

**Whole-number division, in detail.** When both numbers are whole, Java throws away the remainder. `537 / 2` is `268`, not `268.5`. Worse, `double half = 1 / 2;` gives `0.0`, because the division happens first and only then is the result stored. Write `1.0 / 2` instead.

### 2.11 Repeating a set number of times

A `while` loop repeats until something changes. A `for` loop repeats a counted number of times:

```java
int sum = 0;
for (int i = 0; i < 3; i++) {   // start i at 0; keep going while i < 3; add 1 each time
    sum += i;                   // same as: sum = sum + i
}
// sum is now 3, because 0 + 1 + 2 = 3
```

`i++` means 'add one to i'. Programmers start counting at 0, so a loop that runs three times uses 0, 1 and 2.

### 2.12 Java you will meet in Part 5

CurioControl uses a few ideas you have not seen yet. Here is a translation table so they are not a shock.

| Word | Plain meaning | Example |
| --- | --- | --- |
| `interface` / `implements` | A contract. A class that says `implements Command` promises to provide the methods `Command` lists | `class MoveLiftCommand implements Command` |
| `enum` | A fixed list of named choices | `enum IntakeState { IDLE, INTAKING, HOLDING }` |
| `<Something>` (generics) | Says what a container or tool works with. Read `StateMachine<IntakeState>` as 'a state machine of IntakeStates' | `Set<Subsystem>` |
| `() -> ...` (lambda) | A tiny nameless action to run later. `()` means no inputs and `->` means 'do this' | `() -> intakeMotor.setPower(1.0)` |
| `new` | Build a new object from a class | `new PIDController(0.01, 0.0, 0.001)` |
| `this` | The object this code is running inside | `this.lift = lift;` |
| `final` | Cannot be changed after it is set | `private final Motor motor;` |
| `static` | Belongs to the class itself, not to one object | `Commands.sequence(...)` |
| `return` | Hand an answer back from a method | `return lift.atTarget();` |

In `this.lift = lift;`, the left `lift` is the field that belongs to the object, and the right `lift` is the value that was passed in. They share a name, so `this.` says which one you mean.

### 2.13 Practice: predict the output

Write your answer **before** you run anything. Then check the answers below.

1. `int a = 7; int b = 2; double r = a / b;` What is `r`?
2. `double r = 7 / 2.0;` What is `r`?
3. The `for` loop from 2.11, but with `i < 4`. What is `sum`?
4. `double power = 1.7; if (power > 1.0) { power = 1.0; }` What is `power`?
5. `boolean open = false; open = !open; open = !open; open = !open;` What is `open`?

**Answers:** 1) `3.0`, because whole-number division happens first and the result is then widened. 2) `3.5`. 3) `6`, because 0 + 1 + 2 + 3. 4) `1.0`. 5) `true`, because it flipped three times.

If you got four or five right, you are ready for Part 3. If not, reread 2.9 and 2.10, which cover the mistakes that cost beginners the most time.

### 2.14 Methods in depth: inputs, outputs and `void`

A method is a named recipe. Every method has the same four parts:

```java
double ticksToInches(int ticks) {          // return type, name, (inputs)
    return ticks / TICKS_PER_INCH;         // the body: what it does, and what it hands back
}
```

| Part | Meaning here |
| --- | --- |
| `double` (return type) | The kind of answer it hands back. `void` means it hands back nothing |
| `ticksToInches` (name) | What you call it by. Make it a verb or a clear question |
| `int ticks` (parameter) | An input. It is a variable that exists only inside this method |
| `return ...;` | Sends the answer back to whoever called the method and stops the method |

There are three common shapes. Seeing all three makes most robot code readable:

```java
void stopAll() {                       // no inputs, no output: just does something
    fl.setPower(0); fr.setPower(0); bl.setPower(0); br.setPower(0);
}

void setDrivePower(double p) {         // input, no output
    fl.setPower(p); fr.setPower(p); bl.setPower(p); br.setPower(p);
}

boolean isNearTarget(int ticks, int target) {   // inputs AND an output
    return Math.abs(target - ticks) < 10;
}
```

**Defining is not calling.** Writing the method does nothing by itself. It runs only when something *calls* it: `stopAll();` or `double inches = ticksToInches(906);`. If `TICKS_PER_INCH` is `45.3`, that call gives back `20.0`, and you can use the answer straight away, for example `telemetry.addData("Inches", ticksToInches(906));`.

**Why bother?** Three reasons: you stop repeating yourself (fix a bug once, not in five places), the name explains the intent (`isNearTarget` beats a mystery comparison), and you can test small pieces separately.

### 2.15 Classes in depth: build a `Claw` from nothing

A class bundles **data** (fields) with the **actions** that use it (methods). Build one in five steps.

**Step 1: decide what it remembers.** A claw has a servo and knows whether it is open.

**Step 2: write a constructor.** A constructor is a special method with the class's name and no return type. It runs once, at the moment you write `new Claw(...)`, and sets everything up.

**Step 3: write the actions.** Keep the positions as named constants so there is no mystery number.

```java
import com.qualcomm.robotcore.hardware.HardwareMap;
import com.qualcomm.robotcore.hardware.Servo;

public class Claw {
    private static final double OPEN_POS   = 0.8;   // find your real values by testing, unloaded
    private static final double CLOSED_POS = 0.2;

    private final Servo servo;   // the hardware this class owns
    private boolean open;        // what the claw remembers

    public Claw(HardwareMap hardwareMap) {           // constructor
        servo = hardwareMap.get(Servo.class, "claw");
        close();                                     // start in a known state
    }

    public void open()   { servo.setPosition(OPEN_POS);   open = true;  }
    public void close()  { servo.setPosition(CLOSED_POS); open = false; }
    public void toggle() { if (open) { close(); } else { open(); } }
    public boolean isOpen() { return open; }
}
```

**Step 4: use it.** The OpMode no longer knows anything about servos:

```java
private Claw claw;
private boolean lastA = false;

@Override
public void init() {
    claw = new Claw(hardwareMap);   // build it HERE, not where the field is declared
}

@Override
public void loop() {
    if (gamepad1.a && !lastA) {     // button just pressed
        claw.toggle();
    }
    lastA = gamepad1.a;
    telemetry.addData("Claw open", claw.isOpen());
}
```

**Step 5: notice what you gained.** If the servo is replaced, or the positions change, you edit *one file*. The OpMode still reads as a plain description: press A, toggle the claw. This habit, one class per mechanism with the hardware hidden inside, is exactly what CurioControl's `Subsystem` formalises in Part 5.

Why build in `init()` and not on the field line (`private Claw claw = new Claw(hardwareMap);`)? Because `hardwareMap` is empty until the SDK sets it up, and using it too early crashes with a `NullPointerException`.

**Words you have now met:** *field* (data in a class), *constructor* (setup code), *method* (an action), *object* (one built instance), *encapsulation* (hiding the details behind a few simple methods).

### 2.16 Arrays and lists: handling several things at once

An **array** is a fixed-size row of values of the same type. The four mecanum powers fit naturally:

```java
double[] powers = { flPower, frPower, blPower, brPower };

double max = 1.0;
for (double p : powers) {               // read as: for each p in powers
    max = Math.max(max, Math.abs(p));
}
```

This replaces the long nested `Math.max` in section 3.5 with something you can read in one go. The first item is `powers[0]`, because counting starts at 0, and `powers.length` is how many there are.

A **list** is like an array that can grow:

```java
List<String> log = new ArrayList<>();   // a list that holds Strings
log.add("Started");
log.add("Arm raised");
log.size();      // 2
log.get(0);      // "Started"
```

You need `import java.util.List;` and `import java.util.ArrayList;`. The `<String>` says what the list holds, which is the same idea you will see in `Set<Subsystem>` in Part 5.

### 2.17 Many options: `else if` and `switch`

When a decision has more than two outcomes, chain `else if`:

```java
if (gamepad1.a)      { target = LOW;  }
else if (gamepad1.b) { target = MID;  }
else if (gamepad1.y) { target = HIGH; }
```

When you are choosing by one value, such as the current step of an autonomous, a `switch` over an `enum` is cleaner:

```java
enum AutoStep { DRIVE_OUT, RAISE_LIFT, RELEASE, DONE }
private AutoStep step = AutoStep.DRIVE_OUT;

@Override
public void loop() {
    switch (step) {
        case DRIVE_OUT:
            driveForward();
            if (atDistance()) { step = AutoStep.RAISE_LIFT; }
            break;                       // do not forget this
        case RAISE_LIFT:
            lift.moveTo(HIGH);
            if (lift.atTarget()) { step = AutoStep.RELEASE; }
            break;
        case RELEASE:
            claw.open();
            step = AutoStep.DONE;
            break;
        case DONE:
            stopAll();
            break;
    }
}
```

Without `break`, Java keeps running into the next `case`. That is a classic bug. This hand-built pattern is what `StateMachine` in CurioControl does for you, with transitions and timeouts included.

### 2.18 Reading a crash (stack traces)

When the robot app crashes, Logcat prints a **stack trace**. It looks scary but you only need two lines:

```
java.lang.NullPointerException: Attempt to invoke virtual method
    'void ...Servo.setPosition(double)' on a null object reference
    at org.firstinspires.ftc.teamcode.HelloTeleOp.loop(HelloTeleOp.java:27)
```

1. **The first line says what went wrong.** `NullPointerException` means you used something that points at nothing.
2. **The first line that mentions *our* package** (`org.firstinspires.ftc.teamcode`) says where: file `HelloTeleOp.java`, line 27. Open it and look at that line.

Ignore the dozens of `com.qualcomm` lines below. They are the SDK's own machinery calling your code.

Two more you will meet: `IllegalArgumentException` (you passed a value a method will not accept) and `IllegalStateException` (you called something at the wrong time). CurioControl throws these *on purpose*, with a message explaining what to fix.

### 2.19 How to read code you did not write

You will spend more time reading code than writing it. Use this method:

1. **Find the entry point.** In an OpMode, start at `init()` and `loop()`. In CurioControl, start at the class's Javadoc comment at the top of the file.
2. **Read top to bottom once without stopping**, just to get the shape.
3. **`Ctrl+Click` any name you do not know** to jump to its definition. `Ctrl+Q` shows its documentation.
4. **Follow one value.** Pick `power` and trace where it is set, changed and used.
5. **Add telemetry** for the value you are unsure about and run it.
6. **Say it in plain words**, out loud or in a comment, such as 'this flips the stick so up is positive'. If you cannot, you have not understood that line yet.

**Try it:** open `BasicOmniOpMode_Linear` in the samples folder and write one plain-English sentence above every block.

### 2.20 A study method that works

- **Type it, do not paste it.** Your fingers learn the shapes.
- **Predict, then run.** Guess what a piece of code will do before you test it. A wrong guess is the fastest teacher.
- **Change one thing at a time**, then run again.
- **Explain it out loud** to a teammate or even to a rubber duck. Stuck explanations show exactly where the gap is.
- **Little and often.** Twenty minutes a day beats three hours once a week.
- **Keep a bug diary.** Every bug you fix is a lesson you will otherwise relearn:

| Date | What broke | Why | How I found it | The fix |
| --- | --- | --- | --- | --- |
| (example) | Arm crashed in `loop()` | Local `arm` hid the field | Stack trace line 27 | Removed `DcMotor` in front of `arm = ...` |

### 2.21 Exercises, easiest to hardest

Attempt each before asking for help. Hints are in brackets.

1. Write `double inchesToTicks(double inches)` and use it to print 24 inches. \[Multiply by ticks per inch.\]
2. Write `boolean isEven(int n)`. \[`n % 2 == 0`; `%` gives the remainder.\]
3. Write a loop that adds the numbers 1 to 10. \[Start a `sum` at 0.\]
4. Make a `Counter` class with `increment()`, `reset()` and `get()`, then use it to count button presses in an OpMode. \[Needs edge detection.\]
5. Write `double max(double[] values)` that returns the biggest number in an array. \[Start with the first element.\]
6. Add `isOpen` toggling and a *second* servo to `Claw` so it has a left and right finger. \[Two fields, one constructor.\]
7. Write an `enum DriveMode { NORMAL, SLOW }` and use it to switch speed with a button. \[A field of that enum type plus an `if`.\]
8. Write a `Stopwatch` class using `System.currentTimeMillis()` with `start()` and `seconds()`. \[Store the start time in a field.\]

When you can do 1 to 5 without help, you can read most FTC code. After 8, you are ready for CurioControl.

### Checkpoint 2

Write, without looking, a class `Counter` with a private `int count`, a method `increment()`, and a method `get()` that returns it. Then explain to a teammate why `count` is private.

---

## Part 3. The FTC SDK

### 3.1 Your first OpMode

An **OpMode** is one program the Driver Hub can run. The annotation (`@TeleOp`) is what makes it show up in the menu.

```java
package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.eventloop.opmode.OpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;

@TeleOp(name = "Hello TeleOp", group = "Training")
public class HelloTeleOp extends OpMode {

    @Override
    public void init() {
        telemetry.addData("Status", "Ready");
    }

    @Override
    public void loop() {
        telemetry.addData("Left stick Y", gamepad1.left_stick_y);
        telemetry.addData("A pressed", gamepad1.a);
    }
}
```

Run it and wiggle the sticks. **Telemetry** is how the robot talks back to you on the Driver Hub. It is your main debugging tool, so use it constantly.

### 3.2 The OpMode lifecycle

| Method | When it runs |
| --- | --- |
| `init()` | Once, when you press INIT |
| `init_loop()` | Repeats between INIT and Play |
| `start()` | Once, when you press Play |
| `loop()` | Repeats about 50 times a second until Stop |
| `stop()` | Once, when the OpMode ends |

There is also `LinearOpMode`, written top to bottom with `waitForStart()` and `while (opModeIsActive())`. Beginners often find it easier for autonomous. The samples `BasicOpMode_Iterative` and `BasicOpMode_Linear` show both styles. CurioControl is built on the iterative style.

### 3.3 Configuring hardware

Before code can find a motor, the **Robot Configuration** on the Driver Hub must name it. Do this on the Driver Hub: Configure Robot > pick or create a config > assign names to ports.

The name in the config and the name in your code must match *exactly*, including capitals. This is the number one cause of the "could not find device" crash.

Our standard names for a four-wheel drive:

`frontLeft`, `frontRight`, `backLeft`, `backRight`

### 3.4 Driving a motor

```java
DcMotor arm;

@Override
public void init() {
    arm = hardwareMap.get(DcMotor.class, "arm");
    arm.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
}

@Override
public void loop() {
    arm.setPower(-gamepad1.right_stick_y);   // minus sign explained below
}
```

**Why the minus sign?** On an FTC gamepad, pushing a stick **up** gives **negative** Y. We flip it so up means forward. Remember this one; it bites everybody.

Power runs from `-1.0` to `1.0`. **BRAKE** makes the motor resist when power is zero; **FLOAT** lets it coast.

### 3.5 Mecanum drive, step by step

A mecanum robot can drive forward, strafe sideways, and spin, all at once. Each wheel gets a mix of the three commands:

```java
@TeleOp(name = "Mecanum Basic", group = "Training")
public class MecanumBasic extends OpMode {
    private DcMotor fl, fr, bl, br;

    @Override
    public void init() {
        fl = hardwareMap.get(DcMotor.class, "frontLeft");
        fr = hardwareMap.get(DcMotor.class, "frontRight");
        bl = hardwareMap.get(DcMotor.class, "backLeft");
        br = hardwareMap.get(DcMotor.class, "backRight");

        // One side is mounted mirrored, so flip it. Which side depends on your robot.
        fl.setDirection(DcMotor.Direction.REVERSE);
        bl.setDirection(DcMotor.Direction.REVERSE);
    }

    @Override
    public void loop() {
        double forward = -gamepad1.left_stick_y;
        double strafe  =  gamepad1.left_stick_x;
        double turn    =  gamepad1.right_stick_x;

        double flPower = forward + strafe + turn;
        double frPower = forward - strafe - turn;
        double blPower = forward - strafe + turn;
        double brPower = forward + strafe - turn;

        // If any power is above 1, scale all four down together so the ratios stay correct.
        double max = Math.max(1.0, Math.max(Math.abs(flPower),
                     Math.max(Math.abs(frPower),
                     Math.max(Math.abs(blPower), Math.abs(brPower)))));

        fl.setPower(flPower / max);
        fr.setPower(frPower / max);
        bl.setPower(blPower / max);
        br.setPower(brPower / max);
    }
}
```

**Test with the robot on blocks first (wheels off the floor).** Push forward: all four wheels should spin forward. If one spins the wrong way, flip *that* motor's direction. Then test strafe, then turn.

**How mecanum drive works (the physics)**

Each mecanum wheel has small rollers set at 45 degrees around its rim. When the wheel turns, the floor pushes back along a *diagonal*, not straight ahead. One wheel alone would make the robot slide diagonally. With four wheels, two with rollers angled one way and two the other way, the sideways parts of the pushes either cancel out or add up, depending on which wheels you spin in which direction. You choose the combination, and that is the whole trick.

In the table, `+` means the wheel spins so that it would push the robot forward, and `-` means the opposite.

| Motion | Front left | Front right | Back left | Back right |
| --- | --- | --- | --- | --- |
| Forward | + | + | + | + |
| Backward | - | - | - | - |
| Strafe right | + | - | - | + |
| Strafe left | - | + | + | - |
| Turn clockwise | + | - | + | - |
| Turn counter-clockwise | - | + | - | + |

Learn this table. Every mecanum bug you will ever debug is a row of it that does not match what the robot does.

**Reading the code, line by line**

1. `forward`, `strafe` and `turn` are three numbers between -1 and 1, read from the sticks. The minus on `left_stick_y` is the flip from section 3.4.
2. Each wheel's power is the **sum of the three commands**, with the signs from the table. `frontLeft` has a `+` in the forward, strafe-right and turn-clockwise rows, so its power is `forward + strafe + turn`. `frontRight` has `-` in the strafe-right and turn-clockwise rows, so it is `forward - strafe - turn`.
3. Adding three commands can give a power bigger than 1, and a motor cannot do more than 1. So we find the largest absolute power, but never let it drop below 1 (`Math.max(1.0, ...)`), which means we only ever scale down, never up.
4. Every wheel is divided by that same number. All four shrink together, so the *mix* between them stays the same.

**Why we scale instead of clamping each wheel**

The obvious fix for "power above 1" is to cut each wheel off at 1. That quietly breaks the driving. Here is full forward, full strafe and full turn at once:

```
raw powers:      FL =  3.00   FR = -1.00   BL =  1.00   BR =  1.00
scaled (ours):   FL =  1.00   FR = -0.33   BL =  0.33   BR =  0.33
clamped each:    FL =  1.00   FR = -1.00   BL =  1.00   BR =  1.00   (wrong mix)
```

The scaled version keeps the ratios, so the robot goes where you pointed it, just slower. The clamped version changes the ratios, so the robot goes somewhere else. This is the most common reason a mecanum robot "feels off" at full stick.

**Test one wheel at a time**

Before trusting the full formula, prove each motor on its own. Put the robot on blocks and add this temporary code:

```java
// TEMPORARY: hold one button, spin ONE wheel forward at low power
fl.setPower(gamepad1.x ? 0.3 : 0.0);
fr.setPower(gamepad1.y ? 0.3 : 0.0);
bl.setPower(gamepad1.a ? 0.3 : 0.0);
br.setPower(gamepad1.b ? 0.3 : 0.0);
```

Each wheel must spin so that it would push the robot **forward**. Any wheel that spins backward gets `setDirection(REVERSE)` in `init()`. Delete the test code when all four are right, then test the table rows one by one: forward, strafe right, turn clockwise.

**Common problems**

| Symptom | Likely cause | What to do |
| --- | --- | --- |
| Robot spins when you try to strafe | One or more wheels reversed | Do the one-wheel test; fix the direction |
| Pushing forward drifts to one side | One motor reversed, weak, or unplugged | One-wheel test; check cables and the configuration |
| Forward is right, strafe goes the wrong way | Strafe sign flipped | Negate `strafe` |
| Turns the wrong way | Turn sign flipped | Negate `turn` |
| Strafing is slower than driving forward | Normal for mecanum; the rollers waste some force | Nothing to fix; account for it in autonomous |
| Wheels look right but it still crabs | Wheels mounted in the wrong pattern | Compare with your wheel vendor's diagram; left and right wheels must be opposite handedness |

**Making it nicer to drive**

Two small additions make a big difference to drivers:

```java
// Sticks never rest at exactly 0, so ignore tiny values. Otherwise the robot creeps.
private double deadband(double v) {
    return Math.abs(v) < 0.05 ? 0.0 : v;
}

// In loop(): hold the left bumper for precision mode at 40 percent speed.
double slow = gamepad1.left_bumper ? 0.4 : 1.0;

double forward = deadband(-gamepad1.left_stick_y) * slow;
double strafe  = deadband( gamepad1.left_stick_x) * slow;
double turn    = deadband( gamepad1.right_stick_x) * slow;
```

CurioControl's `MathUtil.applyDeadband` does the same thing but also rescales the remaining range, so full stick still means full power. Compare the two in Part 5.

**Try it yourself**

1. Add the telemetry lines for all four wheel powers and drive in a circle. Watch which numbers change.
2. Push the left stick diagonally and predict, before you run it, which two wheels will be zero. (From the table: only two wheels spin for a pure diagonal.)
3. Add precision mode, then add a second button for a *boost* mode and decide what happens if both are held.

### 3.6 Servos

```java
Servo claw = hardwareMap.get(Servo.class, "claw");
claw.setPosition(0.0);   // one end of travel
claw.setPosition(1.0);   // the other end
```

Positions run from `0.0` to `1.0`. Find your real open and closed values by trial with the claw **unloaded**, and write them down as named constants.

### 3.7 Gamepad buttons: held vs pressed

`gamepad1.a` is true the *whole time* the button is down, about 50 times a second. If you toggle something with it, it will flicker. You need to detect the moment of the press:

```java
private boolean lastA = false;

@Override
public void loop() {
    boolean a = gamepad1.a;
    if (a && !lastA) {
        claw.toggle();     // runs once per press
    }
    lastA = a;
}
```

This "was it up last loop, down now" idea is called **edge detection**. CurioControl ships an `EdgeDetector` that does it for you.

### Checkpoint 3

- [ ] Mecanum drive works on blocks, then on the floor.
- [ ] A toggle button opens and closes a servo exactly once per press.
- [ ] Telemetry shows the four motor powers live.

---

## Part 4. Autonomous and sensors

In autonomous the robot drives itself for 30 seconds. To do that it must *know* what it has done, which is what sensors are for.

### 4.1 Why "drive for 1 second" is a bad idea

```java
motor.setPower(0.5);
sleep(1000);          // LinearOpMode only
motor.setPower(0.0);
```

This works on the practice field and fails at competition, because the distance depends on battery voltage, floor friction, and what the robot is carrying. It is fine for a first test. Replace it with **encoders** as soon as you can.

### 4.2 Encoders

An **encoder** counts how far a motor shaft has turned. The count is in **ticks**. Our goBILDA-style drive motors give 537.7 ticks per wheel revolution (check your own motor's datasheet).

To convert ticks to distance you need the wheel size:

```
ticks per inch = TICKS_PER_REV / (pi x wheel diameter in inches)

Example: 96 mm wheel = 3.78 in
         537.7 / (3.14159 x 3.78) = about 45.3 ticks per inch
```

Moving to a position with the built-in controller:

```java
motor.setMode(DcMotor.RunMode.STOP_AND_RESET_ENCODER);  // zero the count
motor.setTargetPosition(1000);                          // set target FIRST
motor.setMode(DcMotor.RunMode.RUN_TO_POSITION);         // then switch mode
motor.setPower(0.5);                                    // speed limit on the way there

while (opModeIsActive() && motor.isBusy()) {
    telemetry.addData("Position", motor.getCurrentPosition());
    telemetry.update();
}
motor.setPower(0.0);
```

The order matters. Setting `RUN_TO_POSITION` before a target throws an error.

See the samples `RobotAutoDriveByEncoder_Linear` and `ConceptMotorBulkRead`.

### 4.3 The IMU (gyro)

The **IMU** inside the Control Hub tells you which way the robot is facing. You must tell it how the hub is mounted:

```java
IMU imu = hardwareMap.get(IMU.class, "imu");
IMU.Parameters params = new IMU.Parameters(
    new RevHubOrientationOnRobot(
        RevHubOrientationOnRobot.LogoFacingDirection.UP,
        RevHubOrientationOnRobot.UsbFacingDirection.FORWARD));
imu.initialize(params);

imu.resetYaw();   // call at the start of autonomous
double heading = imu.getRobotYawPitchRollAngles().getYaw(AngleUnit.DEGREES);
```

Change `UP` and `FORWARD` to match how *your* hub is really mounted. A wrong orientation gives headings that look random. See `ConceptExploringIMUOrientation` and `SensorIMUOrthogonal`.

### 4.4 Other sensors

| Sensor | Sample to read | Watch out for |
| --- | --- | --- |
| Touch / limit switch | `SensorDigitalTouch` | `getState()` is often **true when NOT pressed** |
| Distance (REV 2m) | `SensorREV2mDistance` | Returns bad values at very short range |
| Color | `SensorColor` | Lighting changes the readings. Calibrate at the venue. |
| Odometry pods | `SensorGoBildaPinpoint`, `SensorOctoQuad` | Mount rigidly and measure offsets carefully |
| Cameras (AprilTag) | `ConceptAprilTagEasy` | Later, after the basics are solid |

### Checkpoint 4

- [ ] Autonomous drives forward 24 inches using encoders and stops within one inch, three runs in a row.
- [ ] Autonomous turns 90 degrees using the IMU.
- [ ] You can explain why a time-based autonomous is unreliable.

---

## Part 5. CurioControl, our framework

By now you have written drive code by hand. You have also felt the pain: every OpMode repeats the same motor setup, the same drive math, the same button handling. CurioControl packages those solutions so an OpMode can say *what the robot does* rather than *how motors work*.

```
  Robot application   (our OpModes, subsystems, RobotConfig)
          |
    CurioControl      (hardware, control, drive, commands, telemetry)
          |
      FTC SDK
          |
  Android / hardware
```

It sits *on top of* the SDK, never instead of it. You can always reach the raw SDK object (for example `motor.getSdkObject()`).

### 5.1 Setup (ask a lead)

A lead programmer sets this up once; you do not do it yourself. In outline:

1. The robot project's Gradle file gets the CurioControl repository and one dependency line, with an **exact pinned version**.
2. Access comes from a read-only token in your personal `~/.gradle/gradle.properties`. Never commit it.
3. The SDK version in the robot project must match the version CurioControl was built against. Check `docs/reference/compatibility.md` in the CurioControl repo.

Project layout we follow:

```
TeamCode/src/main/java/org/curioone/robot/
    opmode/       OpModes only: what the robot should do
    subsystem/    mechanisms: each owns its hardware and logic
    config/       RobotConfig: every competition constant
```

Three rules:

1. **OpModes describe intent, not mechanics.** If an OpMode calls `setTargetPosition`, that code belongs in a subsystem.
2. **Subsystems own their hardware.** They expose meaning (`lift.moveTo(HIGH)`), not raw motors.
3. **Constants live in `RobotConfig`.** Wheel sizes, arm positions, gains. If a number appears in two files, it belongs there.

### 5.2 Your first Curio TeleOp

```java
@TeleOp(name = "Main TeleOp", group = "Curio")
public class MainTeleOp extends CurioOpMode {

    @Override
    public void initRobot() {
        // 'robot' is already created for you. Do not assign it again.
        robot.drive().setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
    }

    @Override
    public void runRobot() {
        robot.drive().drive(
            gamepad1.left_stick_x,     // strafe  (+1 = right)
            -gamepad1.left_stick_y,    // forward (+1 = forward), so flip the stick
            -gamepad1.right_stick_x);  // rotation (+1 = counter-clockwise), so flip it
    }
}
```

Two minus signs, both for the same reason: the FTC gamepad and CurioControl use opposite conventions.

- FTC gamepad: stick **up** is **negative** Y.
- CurioControl: **forward** is **positive**, and **counter-clockwise** rotation is **positive**.

**Always test on blocks first.** If the robot still goes the wrong way, change the signs here, not inside the library.

The default drive uses the motor names `frontLeft`, `frontRight`, `backLeft`, `backRight`. If a name is wrong, CurioControl throws an error that names the missing device instead of silently doing something odd. That is deliberate: it is better to fail loudly in the pits than quietly in a match.

### 5.3 Keeping constants in one place

```java
public final class RobotConfig {
    private RobotConfig() {}

    public static final class Drive {
        public static final double WHEEL_DIAMETER_MM = 96.0;
        public static final double TICKS_PER_REV = 537.7;
    }

    public static final class Lift {
        public static final int HOME = 0;
        public static final int LOW = 300;
        public static final int HIGH = 850;
    }
}
```

Now when the lift is re-geared, you change one number in one file. CurioControl itself contains **no** robot constants; that is what lets us reuse it every season.

### 5.4 Subsystems

A **subsystem** is one mechanism: a lift, an intake, a claw. It owns its motors and exposes simple actions.

```java
public class Lift extends Subsystem {

    private final Motor motor;
    private final PIDController pid = new PIDController(0.01, 0.0, 0.001);
    private int targetTicks = RobotConfig.Lift.HOME;

    public Lift(HardwareMap hardwareMap) {
        motor = new Motor(hardwareMap, "lift");
    }

    @Override
    public void init() {
        // Configure here, not in the constructor.
        motor.setRunMode(DcMotor.RunMode.RUN_USING_ENCODER);
        motor.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
        pid.setOutputLimits(-1.0, 1.0);
        pid.setIntegralLimit(0.25);   // anti-windup
        pid.setTolerance(10);         // ticks
    }

    public void moveTo(int ticks) { targetTicks = ticks; }

    public boolean atTarget() { return Math.abs(targetTicks - motor.getPosition()) <= 10; }

    @Override
    public void loop() {
        motor.setPower(pid.calculate(targetTicks, motor.getPosition()));
    }

    @Override
    public void stop() {
        motor.setPower(0.0);   // called for you when the OpMode ends
        pid.reset();
    }
}
```

Register it once in `initRobot()`:

```java
private Lift lift;

@Override
public void initRobot() {
    lift = new Lift(hardwareMap);
    robot.registerSubsystem(lift);   // must happen before initRobot() returns
}

@Override
public void runRobot() {
    if (gamepad1.y) lift.moveTo(RobotConfig.Lift.HIGH);
    if (gamepad1.a) lift.moveTo(RobotConfig.Lift.HOME);
}
```

The framework now calls the subsystem's `init()`, `loop()`, and `stop()` for you. `stop()` is the important one: a lift left under power keeps moving after the OpMode ends.

Why a constructor does not configure hardware: it runs before the Robot Controller's hardware map is fully ready. Configuration belongs in `init()`.

### 5.5 PID control, in plain language

Suppose you want a lift at 850 ticks and it is at 600. **PID** decides the motor power from the *error* (target minus current).

| Term | Idea | Too much of it |
| --- | --- | --- |
| **P** (proportional) | Push harder the farther away you are | Overshoots and oscillates |
| **D** (derivative) | Slow down when approaching fast | Jittery, noisy, buzzing |
| **I** (integral) | Fix a small leftover error that will not go away | Overshoots badly ("windup") |

`PIDController` takes two numbers and knows nothing about motors:

```java
PIDController pid = new PIDController(kP, kI, kD);
double power = pid.calculate(target, current);
```

**Tuning order (do not skip steps):**

1. Set `kI` and `kD` to 0.
2. Raise `kP` until the mechanism reaches the target quickly but starts to oscillate. Back off about 20 percent.
3. Add `kD` until the oscillation calms down.
4. Only if it stops *just short* of the target, add a tiny `kI`, and always set `setIntegralLimit`.
5. Write the final numbers into `RobotConfig` with a comment on the date and the robot weight.

A lift that must fight gravity usually also needs a **feedforward** term, a constant push that holds it up. CurioControl has `GravityFeedforward` and others in the `control` package. Read `docs/guides/control-tuning.md` before using them.

### 5.6 Commands: autonomous as a list of steps

A **command** is one job with a start, a middle, and an end. Commands snap together.

```java
public class MoveLiftCommand implements Command {
    private final Lift lift;
    private final int ticks;

    public MoveLiftCommand(Lift lift, int ticks) {
        this.lift = lift;
        this.ticks = ticks;
    }

    @Override public void initialize()  { lift.moveTo(ticks); }   // once, at the start
    @Override public boolean isFinished() { return lift.atTarget(); }

    @Override
    public Set<Subsystem> requirements() {
        return Collections.singleton(lift);   // the scheduler never runs two commands on one subsystem
    }
}
```

Then an autonomous reads like a recipe:

```java
@Autonomous(name = "Simple Auto", group = "Curio")
public class SimpleAuto extends CurioOpMode {

    private final CommandScheduler scheduler = new CommandScheduler();
    private Lift lift;

    @Override
    public void initRobot() {
        lift = new Lift(hardwareMap);
        robot.registerSubsystem(lift);

        scheduler.schedule(
            Commands.sequence(
                new MoveLiftCommand(lift, RobotConfig.Lift.HIGH),
                Commands.waitSeconds(0.5),
                new MoveLiftCommand(lift, RobotConfig.Lift.HOME)));
    }

    @Override
    public void runRobot() {
        scheduler.run();
        scheduler.publishTelemetry(robot.telemetry());
        robot.telemetry().update();
    }
}
```

Building blocks in `Commands`:

| Helper | Meaning |
| --- | --- |
| `Commands.sequence(a, b, c)` | Do a, then b, then c |
| `Commands.parallel(a, b)` | Do a and b at the same time |
| `Commands.waitSeconds(t)` | Pause |
| `Commands.waitUntil(condition)` | Pause until something becomes true |
| `Commands.instant("name", action, subsystem)` | Do one quick thing |
| `Commands.run(action, subsystem)` | Do something every loop forever (good for TeleOp defaults) |

### 5.7 State machines: when commands are not the right tool

Some behaviour reacts to the world rather than following a script: an intake that runs until it senses a game piece, then holds. A **state machine** models this as named states and the conditions to move between them:

```java
enum IntakeState { IDLE, INTAKING, HOLDING }

StateMachine<IntakeState> sm = new StateMachine<>(IntakeState.IDLE);

sm.onEnter(IntakeState.INTAKING, () -> intakeMotor.setPower(1.0));
sm.onEnter(IntakeState.HOLDING,  () -> intakeMotor.setPower(0.1));
sm.onEnter(IntakeState.IDLE,     () -> intakeMotor.setPower(0.0));

sm.addTransition(IntakeState.IDLE,     IntakeState.INTAKING, () -> gamepad1.right_bumper);
sm.addTransition(IntakeState.INTAKING, IntakeState.HOLDING,  () -> hasPiece());
sm.setTimeout(IntakeState.INTAKING, 3.0, IntakeState.IDLE);   // give up after 3 s

// every loop:
sm.update();
```

This is a sketch: `intakeMotor` and `hasPiece()` are yours to define.

**Rule of thumb:** a fixed sequence of steps is a **command**; behaviour that depends on conditions is a **state machine**. Read `docs/guides/commands-vs-states.md` in the CurioControl repo for the full comparison.

### 5.8 Field-centric driving

In robot-centric driving, "forward" is where the robot faces. In **field-centric**, "forward" is down the field, whichever way the robot is pointing, which most drivers prefer.

It needs the heading from the IMU, and it needs a `MecanumDrive` (the general `robot.drive()` does not have this method):

```java
private MecanumDrive drive;

@Override
public void initRobot() {
    drive = robot.mecanumDrive("frontLeft", "frontRight", "backLeft", "backRight");
    robot.imu().resetHeading();   // do this at the start of every OpMode
}

@Override
public void runRobot() {
    drive.fieldCentric(
        gamepad1.left_stick_x,
        -gamepad1.left_stick_y,
        -gamepad1.right_stick_x,
        robot.imu().heading());   // radians
}
```

If the robot drifts a few degrees, the usual cause is a stale heading from an earlier OpMode, not a bad motor.

### 5.9 Telemetry, logging, and testing without a robot

- `robot.telemetry()` is a managed wrapper over the Driver Hub's telemetry.
- `Logger` writes values to a file every loop so you can graph a run afterwards. Log the target and the actual position when tuning PID, then look at the shape.
- CurioControl's pure logic (`math`, `control`, `util`) never touches SDK or Android classes. That means the tests run on a laptop with `./gradlew test`, no robot required. When you write your own control code, keep the maths in a plain class and test it the same way.

### 5.10 Where to read more

In the CurioControl repo, under `docs/guides/`: `hardware-abstraction`, `drivetrains`, `control-tuning`, `motion-profiles`, `odometry`, `vision`, `commands-vs-states`, `robot-config`, `telemetry-and-logging`, and `bench-testing`. Also `examples/snippets/` for copy-paste fragments.

### 5.11 How one loop flows through CurioControl

Before writing more code, understand *who calls what and when*. This is the single most useful picture in Part 5.

```
You press INIT:
  CurioOpMode.init()
    1. builds the robot (hardware access, clock, telemetry)
    2. calls YOUR initRobot()      <- create and register subsystems here
    3. robot.init()                <- calls every subsystem's init()

You press PLAY, then about 50 times a second:
  CurioOpMode.loop()
    1. YOUR runRobot()             <- read the gamepad, set targets, run the scheduler
    2. robot.loop()                <- every subsystem's loop(), then its telemetry,
                                      then the telemetry is sent to the Driver Hub

You press STOP:
  robot.stop()                     <- every subsystem's stop(): motors to zero
```

What this means in practice:

- **`runRobot()` decides, subsystems do.** `runRobot()` says 'the lift should go to HIGH'. The lift's own `loop()` is what actually turns that into motor power, every cycle, with PID.
- **Order matters.** `runRobot()` runs *before* the subsystems' `loop()`. So a target you set this cycle is acted on this same cycle.
- **`initRobot()` is for creating and registering.** The subsystem's `init()` runs *after* it, so real hardware set-up goes in the subsystem's `init()`.
- **`init()` and `loop()` are `final` in `CurioOpMode`.** You cannot override them. You implement `initRobot()` and `runRobot()` instead, and the framework guarantees the order above.
- **`stop()` always runs.** That is why every subsystem that owns a motor should zero it in `stop()`.
- **Telemetry is automatic.** `robot.loop()` already collects every subsystem's telemetry and sends it, so you rarely need to call `update()` yourself. It is rate-limited, so calling it often does not flood the Driver Hub.

### 5.12 A map of the library

Open the CurioControl project and look under `src/main/java/org/curioone/control/`. Each folder is a *package* with one job:

| Package | What is in it | You reach for it when |
| --- | --- | --- |
| `core` | `CurioOpMode`, `CurioRobot`, `Subsystem`, telemetry manager, hardware registry | Always. Every OpMode starts here |
| `hardware` | `Motor`, `Servo`, `ContinuousServo`, `Encoder`, `IMU`, digital, analog and voltage sensors | Talking to a physical device |
| `drive` | `MecanumDrive`, `TankDrive`, odometry classes, `PoseController` | Driving, field-centric control, going to a position |
| `control` | `PIDController`, `PIDFController`, feedforward classes, `TrapezoidalMotionProfile`, `AimAssist` | Holding or moving a mechanism precisely |
| `command` | `Command`, `Commands`, `CommandScheduler`, `StateMachine` | Autonomous routines and behaviours |
| `math` | `Pose2d`, `Vector2d`, `Rotation2d`, `Transform2d`, `Units`, `MathUtil` | Positions, angles, unit conversion |
| `util` | `EdgeDetector`, `Debouncer`, `Range`, `Clock` | Buttons, noisy sensors |
| `telemetry` | `Logger` | Recording a run to a file |
| `vision` | `VisionManager`, `AprilTagManager`, `TagFieldLayout` | Cameras and AprilTags. Optional |

**Why `math`, `control` and `util` are special.** They contain no FTC or Android classes at all, and an automated test fails the build if anyone adds one. That is the reason their tests run on a laptop in seconds. It is also why a `PIDController` only takes two numbers: it has no idea a motor exists.

**Versions.** CurioControl is pre-release and was built in phases. Check `CHANGELOG.md` and `PHASES.md` to see which release added which package before you depend on a class, and pin an exact version.

### 5.13 The hardware wrappers

Why not just use the SDK's `DcMotor` directly? CurioControl's `Motor` wraps it to give you one tidy, consistent API, to raise a clear error if a device is missing, and to let the logic be tested without a robot. The real SDK object is always available through `getSdkObject()` if you need it.

```java
Motor lift = robot.motor("lift");       // looked up once, by its configured name
lift.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
lift.setPower(0.6);
int ticks = lift.getPosition();
```

| `Motor` method | What it does |
| --- | --- |
| `setPower(p)` / `stop()` | Run at a fraction of full power, or stop |
| `setVelocity(ticksPerSec)` | Hold a speed using the motor controller's own loop |
| `getPosition()` / `getVelocity()` | Encoder ticks, and ticks per second |
| `setTargetPosition(t)` + `setRunMode(RUN_TO_POSITION)` | Let the motor controller move to a position |
| `isBusy()` | Still moving toward the target? |
| `resetEncoder()` | Make the current position zero |
| `setDirection(d)` | Flip which way positive power turns it |
| `isOverCurrent()` | Is the motor drawing too much current (stalled)? |

`Servo` offers `setPosition`, `getPosition`, `setDirection` and `scaleRange(min, max)`. `scaleRange` is handy: if your claw only needs 0.2 to 0.8 of the servo's travel, you can limit it so that 0 to 1 means exactly that range.

### 5.14 Buttons properly: `EdgeDetector` and `Debouncer`

In section 3.7 you wrote edge detection by hand. CurioControl does it for you:

```java
private final EdgeDetector aButton = new EdgeDetector();

@Override
public void runRobot() {
    if (aButton.poll(gamepad1.a) == EdgeDetector.Edge.RISING) {
        claw.toggle();      // runs once per press
    }
}
```

`poll` returns one of three answers: `NONE`, `RISING` (just pressed) or `FALLING` (just released). Call it exactly once per loop.

A `Debouncer` is for noisy inputs such as a limit switch that flickers. `new Debouncer(0.05)` only reports a change after the input has stayed the same for 0.05 seconds. Feed it with `update(input)` and read `output()`.

### 5.15 Putting it together: a complete TeleOp

Three small classes and one OpMode. Read them in this order and trace what each line does.

**1. `RobotConfig`** (all the numbers):

```java
public final class RobotConfig {
    private RobotConfig() {}

    public static final class Lift {
        public static final int HOME = 0;
        public static final int LOW  = 300;
        public static final int HIGH = 850;
    }

    public static final class Claw {
        public static final double OPEN   = 0.8;
        public static final double CLOSED = 0.2;
    }
}
```

**2. `Claw`**, as a CurioControl subsystem:

```java
public class Claw extends Subsystem {
    private final Servo servo;
    private boolean open;

    public Claw(HardwareMap hardwareMap) {
        servo = new Servo(hardwareMap, "claw");
    }

    @Override public void init() { close(); }          // start in a known state

    public void open()   { servo.setPosition(RobotConfig.Claw.OPEN);   open = true;  }
    public void close()  { servo.setPosition(RobotConfig.Claw.CLOSED); open = false; }
    public void toggle() { if (open) { close(); } else { open(); } }

    @Override
    protected void publishTelemetry(TelemetryManager telemetry) {
        telemetry.add(TelemetryCategory.INTAKE, "Claw open", open);
    }
}
```

**3. `Lift`** is the class from section 5.4.

**4. The OpMode**, which now reads like a description of the robot:

```java
@TeleOp(name = "Competition TeleOp", group = "Curio")
public class CompetitionTeleOp extends CurioOpMode {

    private MecanumDrive drive;
    private Lift lift;
    private Claw claw;
    private final EdgeDetector clawButton = new EdgeDetector();

    @Override
    public void initRobot() {
        drive = robot.mecanumDrive("frontLeft", "frontRight", "backLeft", "backRight");
        lift  = new Lift(hardwareMap);
        claw  = new Claw(hardwareMap);
        robot.registerSubsystem(lift);
        robot.registerSubsystem(claw);
    }

    @Override
    public void runRobot() {
        drive.mecanum(
            gamepad1.left_stick_x,
            -gamepad1.left_stick_y,
            -gamepad1.right_stick_x);

        if (gamepad1.y) lift.moveTo(RobotConfig.Lift.HIGH);
        if (gamepad1.x) lift.moveTo(RobotConfig.Lift.LOW);
        if (gamepad1.a) lift.moveTo(RobotConfig.Lift.HOME);

        if (clawButton.poll(gamepad1.right_bumper) == EdgeDetector.Edge.RISING) {
            claw.toggle();
        }
    }
}
```

Notice what is **not** here: no motor names for the lift, no tick maths, no servo positions, no telemetry calls, no stop code. Each lives in the one place that owns it.

**Exercise:** trace one press of the Y button through every class. Which method sets the target? Which one turns it into motor power? When does the power get set? (Answer: `moveTo` stores the target in `runRobot()`; the lift's `loop()` runs straight after and does the PID and the `setPower`.)

### 5.16 Commands in depth

Section 5.6 gave the shape. Here are the rules behind it.

**The lifecycle.** A command has four hooks, and *you never call them yourself*. The scheduler does:

| Hook | When it runs | Typical use |
| --- | --- | --- |
| `initialize()` | Once, when the command is scheduled | Set the target, record a start time |
| `execute()` | Every loop while it runs | Per-loop work, if any |
| `isFinished()` | Checked every loop | Return `true` when the job is done |
| `end(interrupted)` | Once, when it ends | Tidy up. `interrupted` is `true` if it was cancelled |

Put set-up in `initialize()`, **not the constructor**. The constructor runs when you *build* the routine, long before the match starts.

**Ownership.** A command lists the subsystems it needs in `requirements()`. The scheduler never runs two commands that need the same subsystem: scheduling a second one cancels the first, which then ends with `end(true)`. So if you forget to declare a requirement, the scheduler cannot protect you, and two commands may fight over one motor.

**Default commands.** `scheduler.setDefaultCommand(lift, command)` says: 'when nothing else is using the lift, run this'. It is how a mechanism holds position or follows a joystick between jobs.

**Why `isFinished()` must look at real data.** Our `Lift.atTarget()` compares the *live encoder position* to the target. We deliberately do **not** use `pid.atSetpoint()` there. That method only reflects the last time `calculate()` ran, so right after you set a new target it can still say 'yes, we are there' from the previous cycle, and the command would finish instantly without moving. When a command asks 'are we done?', ask the hardware.

**Choosing the right tool:**

| You want... | Use |
| --- | --- |
| A fixed list of steps | `Commands.sequence(...)` |
| Two things at once (raise the lift while driving) | `Commands.parallel(...)` |
| Wait for a sensor or condition | `Commands.waitUntil(condition)` |
| One quick action | `Commands.instant("name", action, subsystem)` |
| Behaviour that reacts to conditions | `StateMachine` |

### 5.17 When CurioControl complains (on purpose)

CurioControl is written to fail loudly with a clear message, because a loud failure in the pits beats a silent one in a match.

| What you see | What it means | Fix |
| --- | --- | --- |
| An error naming a missing device | The name in code does not match the Robot Configuration | Check spelling and capitals in both |
| An error when registering a subsystem | You registered after `initRobot()` finished | Register inside `initRobot()` |
| `IllegalArgumentException` mentioning a value is not finite | You passed `NaN` or infinity into drive or PID | Check the maths that produced the number, often a divide by zero |
| `IllegalArgumentException` from `setTolerance` | A negative or `NaN` tolerance | Use a positive number |
| The mechanism keeps moving after STOP | A subsystem does not zero its motor in `stop()` | Override `stop()` |
| Two commands fighting | A command did not declare a subsystem it uses | Fix `requirements()` |

Read the *whole* message. These are written to tell you what to do.

### 5.18 Reading the library's own source

The best way to understand CurioControl is to read it. The code is heavily commented with the *reasons* behind each decision.

1. Open `PIDController.java` and read the comment at the top. What does 'anti-windup' mean here?
2. Open `MecanumDrive.java`. Find the `normalizationScale` idea and match it to the example in section 3.5.
3. Open `CurioOpMode.java`. It is short. Match it to the loop diagram in 5.11.
4. Open `src/test/` and find `PIDControllerTest.java`. A test shows exactly what the author promises the class will do. Which behaviour surprised you?
5. Open `docs/adr/` and read one *architecture decision record*. These explain why the library is shaped the way it is, which is the same reasoning you will use when designing your own robot code.

### 5.19 Part 5 labs

**Lab 1: Drive.** Build `CompetitionTeleOp` with only the drive. Test on blocks. Fix signs until forward is forward, strafe is right and turning matches the stick.

**Lab 2: A subsystem.** Add the `Claw`. Open and close it with the right bumper. Put the positions in `RobotConfig` and find the real values by testing with the claw unloaded.

**Lab 3: PID.** Add the `Lift`. Tune `kP`, then `kD`, writing down every change and what the lift did. Log the target and position with `Logger` and look at the shape.

**Lab 4: Autonomous.** Build a `Commands.sequence` that raises the lift, waits half a second, opens the claw, then lowers the lift. You will need a small command for the claw, or `Commands.instant`.

**Lab 5: Break it on purpose.** Misspell a motor name. Forget to register a subsystem. Skip the `stop()` override. For each, write down the symptom you saw, so you recognise it in a real emergency.

**Lab 6: Read and explain.** Pick one class from `src/main/java/org/curioone/control/` and explain it to a teammate in five minutes, using only what you read in the source.

### Checkpoint 5

- [ ] A Curio TeleOp drives the robot in the right directions, with both stick signs correct.
- [ ] A `Lift` subsystem with PID holds three preset heights without oscillating.
- [ ] A command-based autonomous scores a game piece and parks.

---

## Part 6. Practice plan and reference

### 6.1 Ten-week plan

| Week | Goal | Deliverable |
| --- | --- | --- |
| 1 | Android Studio, clone, build, Git workflow | Pushed branch with a HelloTeleOp |
| 2 | Java basics | Counter class plus a short quiz with a mentor |
| 3 | Gamepad and one motor | Arm controlled by a stick |
| 4 | Mecanum drive | Driving on blocks, then the floor |
| 5 | Servos and edge detection | Claw toggled by a button |
| 6 | Encoders and autonomous | 24-inch drive within one inch |
| 7 | IMU | 90-degree turn; field-centric drive |
| 8 | CurioControl TeleOp and subsystems | Lift subsystem registered and working |
| 9 | PID and commands | Tuned lift; command-based auto |
| 10 | Capstone | Complete TeleOp plus a two-step autonomous, presented to the team |

### 6.2 Debugging cheat sheet

| Symptom | Most likely cause |
| --- | --- |
| Crash: "unable to find a hardware device" | Name in code does not exactly match the Robot Configuration |
| Robot drives backward | Stick Y not negated (`-gamepad1.left_stick_y`) |
| Robot spins when you try to strafe | One drive motor direction is wrong |
| Robot turns the wrong way | Rotation sign; CurioControl wants counter-clockwise as positive |
| Lift oscillates | `kP` too high, or no `kD` |
| Lift creeps past the target | Integral windup; set `setIntegralLimit` |
| Servo buzzes at the end of travel | Commanding past the physical range |
| Field-centric drifts | Heading not reset, or hub orientation set wrong |
| Worked in the morning, weak in the afternoon | Low battery; use encoders and closed-loop control |
| Button action fires dozens of times | Held vs pressed; use edge detection |
| Everything red after pulling | Sync Project with Gradle Files |
| Will not deploy | Check the device dropdown; reconnect USB or `adb connect`; restart the Control Hub |

**Debug method:** change one thing, test, and write down the result. Put the suspicious value on telemetry. Do not guess for an hour; look at the numbers.

### 6.3 Team coding conventions

- Class names `PascalCase`, methods and variables `camelCase`, constants `UPPER_SNAKE_CASE`.
- No magic numbers. Name every physical value and put it in `RobotConfig`.
- Comments explain **why**, not what. `// negate: gamepad Y is inverted` is useful; `// set power` is not.
- Never call `sleep()` in an iterative OpMode's `loop()`; it freezes the whole robot.
- Every pull request gets one review from someone who did not write it.
- Competition code uses a **pinned library version**. Never upgrade the week of an event.

### 6.4 Safety

- First run of any new code is **on blocks**, wheels off the floor.
- Hands and loose clothing clear of moving parts. Announce "enabling" before pressing Play.
- Know where the Stop button is. Press it first and ask questions later.
- Check the battery before every run and never run a robot on a battery that is nearly flat.
- A subsystem's `stop()` must always leave motors at zero power.

### 6.5 Glossary

| Term | Meaning |
| --- | --- |
| OpMode | One program the Driver Hub can run |
| Telemetry | Messages the robot sends to the Driver Hub screen |
| Encoder | Sensor that counts motor rotation, in ticks |
| IMU | Gyro and accelerometer that tell the robot's heading |
| PID | Controller that sets power from the error to a target |
| Feedforward | A known push added to PID, such as holding against gravity |
| Subsystem | One mechanism and all the code that owns its hardware |
| Command | A job with a start, a run, and an end |
| State machine | Named states plus rules for moving between them |
| Field-centric | Driving where "forward" means down the field |
| Gradle | The build tool that compiles the project |
| Logcat | Android's live log, used to see crashes |

### 6.6 Resources

- Official FTC documentation: `ftc-docs.firstinspires.org` (has Blocks, OnBot Java, and Android Studio tutorials)
- Sample OpModes inside our own FtcRobotController project (best place to start)
- CurioControl's `docs/`, `examples/snippets/`, and `CONTRIBUTING.md`

**Where to go next:** odometry and `PoseController` for driving to field positions, motion profiles for smooth lift moves, and AprilTag vision for self-localising. Each has a guide in the CurioControl docs.

### 6.7 More learning resources

Pick what matches where you are in the course. Links are community and official sites; if one has moved, search for the name.

**Start here (official FTC)**

| Resource | What it is for | Use it in |
| --- | --- | --- |
| [FTC Docs](https://ftc-docs.firstinspires.org) | The official guide: Blocks, OnBot Java and Android Studio tutorials, hardware setup, and the SDK reference | Parts 1 and 3 |
| Sample OpModes in our FtcRobotController project | Working, commented examples for drive, sensors, AprilTags and telemetry. Read them before searching elsewhere | Parts 3 and 4 |
| FTC SDK Javadoc (linked from FTC Docs) | Exact method names and what each argument means | Any time you are unsure what a method does |

**Learning Java**

| Resource | What it is for | Use it in |
| --- | --- | --- |
| [Oracle Java Tutorials](https://docs.oracle.com/javase/tutorial/) | The official free tutorials; read *Language Basics* and *Classes and Objects* | Part 2 |
| [Java Programming MOOC, University of Helsinki](https://java-programming.mooc.fi) | A free, exercise-driven course that takes you from nothing to solid beginner Java | Part 2, in parallel |
| *Learn Java for FTC* (free book by Alan G. Smith, search the title) | Java taught with FTC examples throughout | Parts 2 and 3 |

**Android Studio and Git**

| Resource | What it is for | Use it in |
| --- | --- | --- |
| [Android Studio user guide](https://developer.android.com/studio/intro) | What every panel and menu does | Part 1 |
| [Learn Git Branching](https://learngitbranching.js.org) | An interactive game that makes branches, merges and rebases click | Part 1.8 |
| [Pro Git book](https://git-scm.com/book) | Free and thorough. Read chapters 1 to 3 | Part 1.8 |

**FTC-specific programming and theory**

| Resource | What it is for | Use it in |
| --- | --- | --- |
| [Game Manual 0 (gm0.org)](https://gm0.org) | A community-written FTC guide covering mecanum, motors, PID, feedforward, odometry and more. Excellent for the *why* behind the code | Parts 3 to 5 |
| [FTC Dashboard](https://github.com/acmerobotics/ftc-dashboard) | Live graphs and config editing in a browser while the robot runs; makes PID tuning far easier | Part 5.5 |
| [WPILib: Introduction to PID](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/index.html) | Clear explanation of PID and feedforward written for FRC; the ideas transfer directly | Part 5.5 |

**Libraries other teams use (read to compare approaches)**

| Resource | What it is for | Use it in |
| --- | --- | --- |
| [FTCLib](https://docs.ftclib.org) | A popular command-based FTC library; its docs explain commands and subsystems well | Part 5.6 |
| [Road Runner](https://rr.brott.dev) | Trajectory-following and odometry for autonomous | After Part 5 |
| [Pedro Pathing](https://pedropathing.com) | A path-following library with good documentation | After Part 5 |

**Community and help**

| Resource | What it is for |
| --- | --- |
| [FTC Community Forum](https://ftcforum.firstinspires.org) | Official forum; questions get answered by FIRST staff and volunteers |
| FTC Discord and the r/FTC subreddit | Fast answers from other teams. Always post the exact error text and the code |
| Other teams' public GitHub repos | Search GitHub for FTC team code and read how they structure things. Copy *ideas*, not code you do not understand |

**Inside our own repos**

| Where | What to read |
| --- | --- |
| `CurioControl/docs/getting-started/` | `quickstart`, `installation`, `project-setup`, in that order |
| `CurioControl/docs/concepts/` | `philosophy`, `architecture`, `hardware-independence`, `faq` |
| `CurioControl/docs/guides/` | `bench-testing` first, then `drivetrains`, `control-tuning`, `commands-vs-states`, `odometry` |
| `CurioControl/examples/snippets/` | Short copy-paste fragments for mecanum, field-centric, PID, telemetry and a sequential autonomous |
| `CurioControl/src/test/` | The unit tests. They show exactly how each class is meant to be used, and they are good reading for learning to test your own code |

**Suggested reading order for a new member**

1. FTC Docs Android Studio tutorial, then Part 1 of this course.
2. Helsinki Java MOOC, parts 1 and 2, alongside Part 2.
3. Sample OpModes `BasicOpMode_Iterative` and `RobotTeleopPOV_Linear`, then Part 3.
4. gm0.org pages on mecanum and encoders, then Part 4.
5. gm0.org and WPILib on PID, then Part 5.
6. Other teams' code, once you can read your own comfortably.

---

## Part 7. Using AI to learn, not to skip learning

AI tools can explain a confusing error in seconds, answer the question you were too shy to ask, and quiz you at midnight. They can also hand you code you do not understand, which then breaks at the worst moment and leaves you unable to fix it. Which one you get depends almost entirely on **how you use them**.

Think of an AI as a very well-read tutor who has never seen your robot, sometimes states wrong things with total confidence, and will happily do your homework if you let it. Use it like a tutor, not like a vending machine.

### 7.1 The goal

The goal of this course is not code that works today. It is **you** being able to write, read and fix robot code on your own, at 8 am on competition day when the Wi-Fi is bad and nobody can help. Every time you let an AI do the thinking, you skip a rep. Every time you make it help you think, you get stronger.

**The test:** after using AI, could you rebuild that code on a blank page, and explain every line to a judge? If not, you borrowed an answer; you did not learn it.

### 7.2 What AI is good and bad at

| It is good at | It is bad at |
| --- | --- |
| Explaining a concept in different ways until one clicks | Knowing your robot: your motor names, wiring, wheel size and gear ratios |
| Translating an error message into plain words | Knowing the current FTC SDK or a small, new library such as CurioControl. It may invent methods or use old ones |
| Reviewing your code for mistakes and unclear names | Tuning: it cannot know your `kP`; only the robot can tell you |
| Making practice problems and quizzing you | Being right every time. It sounds just as confident when it is wrong |
| Comparing two approaches with trade-offs | Safety. It does not know your robot can hurt someone if a motor runs away |

### 7.3 The golden rule: ask *why*

Never accept an answer you cannot explain. After **every** answer, ask:

- **Why** does this work?
- **Why** did you choose this approach over another one?
- **What would break** if I changed this line?
- **How would I test** that it is correct?
- **How could I have found this myself?**

The last question is the most valuable. It turns a one-off fix into a skill.

**The learning ladder.** Climb it in order and only move up when you are really stuck:

1. **Try it yourself for 15 minutes.** Read the error, add telemetry, check the docs and the samples.
2. **Ask for an explanation, not a fix.** 'What does this error mean?'
3. **Ask for a hint.** 'Point me in the right direction without giving the answer.'
4. **Ask for a bigger hint**, or for an example *on a different problem*.
5. **Ask a teammate or mentor** if you are still stuck after 30 minutes.
6. **Only then see a full solution**, and when you do, rewrite it yourself from memory and explain it back.

### 7.4 Prompt recipes you can copy

| You want to | Say something like |
| --- | --- |
| Understand an error | `Here is the error and my code. Explain in plain words what the error means and where to look. Do not fix it yet.` |
| Understand code | `Explain this code line by line for a beginner. Then ask me two questions to check I understood.` |
| Get unstuck | `Give me a hint, not the solution. If I am still stuck, I will ask for a bigger hint.` |
| Learn the reasoning | `Why did you choose this approach instead of X? What would go wrong if I used X?` |
| Get a review | `Review my code. List the three most important problems and explain each. Do not rewrite the whole thing.` |
| Practise | `Give me five practice problems about Java methods, at beginner level, with no solutions.` |
| Be quizzed | `Quiz me on this topic one question at a time. Wait for my answer, then tell me if I am right and why.` |
| Teach it back | `I will explain PID in my own words. Tell me what I got wrong or missed.` |
| Plan before coding | `Before writing any code, outline the steps and the classes you would use, and ask me about anything unclear.` |
| Check a claim | `How could I verify that this is correct? Which documentation or test would prove it?` |

Put your level in the prompt: `I am a beginner. I know variables and if-statements but not classes yet.` The answer changes a lot.

### 7.5 Give it the right context

The AI only knows what you tell it. Vague question, vague (or wrong) answer. A good question includes:

```
I'm on an FTC team using Android Studio. FTC SDK 11.1, Java.
I'm a beginner (I know variables, if, and loops).

Goal: the lift should hold at three preset heights.
What I expected: it stops at 850 ticks.
What happened: it overshoots and oscillates.

Here is my Lift class: [paste the code]
Here is the telemetry output: [paste the numbers]

Do not give me the fixed code yet. What should I check first, and why?
```

What to include: the SDK and library versions, what you expected, what actually happened, the **exact** error text, the relevant code (not your whole project), and what you already tried.

**For CurioControl questions,** the AI probably has never seen the library. Paste the relevant class or its Javadoc, or point a coding agent at the repo folder, and tell it to answer from *that source* rather than from memory.

### 7.6 Check everything

Treat every AI answer as a draft from a smart but unreliable classmate. Before you trust code:

1. **Read every line.** Can you say what each one does?
2. **Does it compile?** For every red underline, ask whether the method really exists. `Ctrl+Click` any name you do not recognise.
3. **Check names against the real docs** (FTC SDK Javadoc, CurioControl source). AI invents methods that sound right.
4. **Check units and signs.** Degrees or radians? Is up positive or negative? (CurioControl uses radians and counter-clockwise-positive rotation.)
5. **Compare with the official samples** in FtcRobotController.
6. **Test on blocks first**, at low power, with your hand near the Stop button.
7. **Ask it what could go wrong** and how you would test it.
8. **Get a second opinion** from a mentor, a different tool, or the documentation.

Known traps in FTC:

| Trap | Example |
| --- | --- |
| Invented methods | A method name that looks right but does not exist in the SDK |
| Outdated code | Older tutorials use the `BNO055IMU` class; current code uses the `IMU` interface |
| Guessing your robot | Made-up motor names, wheel sizes or which motor to reverse |
| Mixed libraries | Blending FTCLib or Road Runner style into CurioControl code |
| Copying a doc's mistake | CurioControl's own docs pass `gamepad1.left_stick_y` without flipping it. An AI trained on them repeats the bug. Test it on blocks |
| Over-engineering | Ten classes for a one-motor problem |

### 7.7 Tools

Pick one or two and learn them well. Check each tool's current pricing, free tier and age rules, because many accounts require you to be a certain age. Ask your mentor and a parent or guardian before signing up.

| Tool | What it is | Good for |
| --- | --- | --- |
| **OpenCode** | A free, open-source AI coding agent. It runs in a terminal, as a desktop app, or as an IDE extension, and works with several model providers (including Claude, OpenAI, Google and local models). It has a read-only **plan** agent for exploring and analysing code, and a full-access **build** agent that can change files | Asking questions about our two repos without changing anything. Learning how a codebase fits together |
| **Claude** (claude.ai and Claude Code) | A chat assistant, plus a coding tool that works inside a project folder. Look for a learning-oriented style in the style menu if your version has one | Patient explanations, step-by-step tutoring, quizzes |
| **ChatGPT, Gemini** | General chat tutors. Gemini is also built into Android Studio | Concept explanations and error messages |
| **GitHub Copilot** | Suggests code as you type. Students may be able to get it free through GitHub Education; check current terms | Convenient, but easy to accept suggestions without reading them. Use with care |

**Getting started with OpenCode** (do this with a mentor the first time):

1. Install it from `opencode.ai/download`, or with `npm i -g opencode-ai` if you have Node.js. Other installers (such as `winget` and `brew`) are listed in its docs.
2. Open a terminal **inside the CurioControl or FtcRobotController folder** and run `opencode`.
3. Connect a model provider with `opencode auth login` and follow the prompts. Some providers charge for use, so agree a spending limit with your mentor first.
4. Start in the **plan** agent. Ask it questions: 'Walk me through what `CurioOpMode` does.' It will read the real files.
5. Only when you understand the code should you let the **build** agent change anything, and only a small change at a time.

**Using any coding agent safely, with Git as your safety net:**

1. Commit or stash your work first, so you have a clean starting point.
2. Work on your own branch, never on `master` or `main`.
3. Ask for **one small change**, and ask it to explain the change.
4. Look at the exact changes (`git diff`, or the Commit window) and read every line.
5. Test on blocks.
6. If you do not understand it or do not like it, throw it away with Rollback and try a smaller request.
7. Commit with a message saying what changed, and note that an AI helped.

### 7.8 A worked example

Your robot drives backward when you push the stick forward.

**The vending-machine way:**

```
You: my robot drives backwards fix it
AI:  [rewrites your loop with a minus sign]
You: [pastes it, it works, moves on]
```

It works, but you learned nothing. The next time a stick feels wrong on a different mechanism, you are stuck again.

**The tutor way:**

```
You: My mecanum robot drives backward when I push the left stick forward.
     Here is my loop() [code]. I'm a beginner. Do not give me the fixed
     code yet. Ask me up to three questions that would help me find the
     cause, and give me one hint.
AI:  What number does telemetry show for gamepad1.left_stick_y when you
     push the stick up?
You: -1.0
AI:  So pushing up gives a negative number. What does your formula do
     with a negative 'forward' value?
You: It drives backward. So I need to flip the sign?
AI:  Yes. Try it. Then tell me what you would do for the turn stick, and why.
```

Same bug, same fix, but now you understand *why* the minus sign exists, and you can spot it anywhere.

### 7.9 Safety, privacy and honesty

**Never paste secrets.** Your GitHub token, passwords, or anything from `gradle.properties` must never go into a prompt. Treat the chat box as a public place.

**Do not share other people's personal details** (names, photos, contact info of teammates, mentors or sponsors) without their permission.

**Be honest about where help came from.** FIRST has published guidance saying teams may use AI to help with things such as writing robot code, but must give proper credit and respect licences and intellectual property, just as you would when using a library from GitHub. Rules and judging expectations can change, so confirm with your mentor and check the current FIRST Tech Challenge materials. In practice:

- Note AI help in your commit messages and your engineering portfolio.
- Be ready for judges to ask you to explain your code. 'The AI wrote it' is not an answer. 'I asked it to explain X, then I wrote it myself and tested it' is.

**Respect the robot.** AI-written code can make a motor run away. Never run code you have not read, and always test on blocks first.

### 7.10 Proposed team rules

1. You must be able to explain **every line** you commit. Reviewers will ask.
2. Ask for explanations, hints and reviews before full solutions.
3. Read and test AI-written code before it goes near the robot.
4. Credit AI help in commit messages and the portfolio.
5. No secrets or personal information in prompts.
6. When the AI and the documentation disagree, the documentation and the robot win.
7. Try for 15 minutes, then ask the AI, then after 30 minutes ask a human.
8. Keep one **AI-off** session each week where everyone codes without it.

### 7.11 Habits and exercises

1. **Wrong-answer hunt.** Ask an AI to explain mecanum drive. Check its answer against Part 3 and gm0.org, and find at least one thing it oversimplified or got wrong.
2. **Hint-ladder drill.** Ask a mentor for a program with a deliberate bug. Climb the ladder in 7.3 and record which rung solved it.
3. **Verification drill.** Ask an AI to write a `Claw` class. List every method it calls and `Ctrl+Click` each one to prove it exists. Fix anything made up.
4. **Teach-back.** Explain PID to a teammate with your notes closed. Then ask the AI to point out what you got wrong.
5. **AI log.** Keep a short table: what I asked, what I learned, what it got wrong.
6. **AI-off Friday.** Do a lab from this course with no AI at all, and see what you actually remember.

### 7.12 More on learning well with AI

| Resource | Why read it |
| --- | --- |
| [FIRST: Expanding the FIRST Toolbox with AI](https://community.firstinspires.org/expanding-the-first-toolbox-with-artificial-intelligence) | FIRST's own words on using AI responsibly, including crediting your sources |
| [OpenCode documentation](https://opencode.ai/docs) | Setup, the plan and build agents, and configuration |
| [OpenCode downloads](https://opencode.ai/download) | Desktop app and installers |
| [Prompt engineering overview](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview) | Practical advice on writing clear, detailed prompts |
| [Game Manual 0](https://gm0.org) | A trustworthy human-written source to check AI explanations of FTC topics against |
| Official FTC docs and Javadoc | The final word on what the SDK actually does |

### Checkpoint 7

- [ ] I can explain the learning ladder and where I am on it when I am stuck.
- [ ] I rewrote a prompt to ask for a hint instead of a fix, and I learned from the result.
- [ ] I verified an AI-written method by finding it in the real docs or source.
- [ ] I used Git to review and, if needed, undo an AI-made change.
- [ ] I can explain every line of the last piece of code I committed.
