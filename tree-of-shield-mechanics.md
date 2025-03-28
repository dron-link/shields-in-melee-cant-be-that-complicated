
The Tree of Shield Mechanics (v1.1.1 from 28 March 2025)
========================================================

`  In Memory Of: Hax$  `

##### Thanks

Deep Blue C.

PracticalTAS

##### Credits

Thanks for the freely-available work of: tauKhan, Kadano, Magus420, @alexspuffstuff, schmooblidon, PracticalTAS, B&D Games, and the SmashWiki contributors

Writer: dron-link

Contributions: PracticalTAS, Deep Blue C.

##### How reliable is the information contained here

My original input is based on what I gleaned from simple frame-by-frame planned interactions in TrainingMode-CommunityEdition's Training Lab; the rest of the information contained here was sourced from the work of experts in the field; the fraction that I managed to find while putting together this document. I'm privy of the niche research carried by them, and you may find mistakes and inconsistency in this content because my research procedure isn't as polished as theirs.

None of the following information was gathered with Yoshi's unique shield in mind.

Table of contents
-----------------

- [Table of Contents](#table-of-contents)
- [The basic way(s) to input a shield](#the-basic-ways-to-input-a-shield)
- [[In-game: starting up the shield](#in-game--starting-up-the-shield)](#in-game-starting-up-the-shield)
- [Buffering A](#buffering-a)
    - [Two ways to buffer A](#two-ways-to-buffer-a)
- [Elements of shield](#elements-of-shield)
- [What does shield strength do, upon hit](#what-does-shield-strength-do-upon-hit)
- [Shield strength number](#shield-strength-number)
- [Input of the shield strength](#input-of-the-shield-strength)
    - [Strength input conflict-solving](#strength-input-conflict-solving)
- [Initial strength of the shield](#initial-strength-of-the-shield)
- [Animations and their associated state](#animations-and-their-associated-state)
- [How to get the `GuardOn`/`` animation on the first frame of shielding](#how-to-get-the-guardon--animation-on-the-first-frame-of-shielding)
- [How to get the `GuardReflect`/` ` animation on the first frame of shielding](#how-to-get-the-guardreflect--animation-on-the-first-frame-of-shielding)
- [Changing the shield strength](#changing-the-shield-strength)
- [The `GuardSetOff`/`GuardDamage` animation](#the-guardsetoffguarddamage-animation)
- [Powershield effect in the physical shield bubble hitbox](#powershield-effect-in-the-physical-shield-bubble-hitbox)
    - [Powershield counter](#powershield-counter)
- [Projectile on the physical shield bubble hitbox](#projectile-on-the-physical-shield-bubble-hitbox)
- [Reflect hitbox](#reflect-hitbox)
    - [More on the reflect bubble hitbox](#more-on-the-reflect-bubble-hitbox)
- [Autoshield](#autoshield)
  	- [Autoshield counter](#autoshield-counter)
- [Autorelease](#autorelease)
- [Inputting the `GuardOff`/`GuardOff` animation](#inputting-the-guardoffguardoff-animation)
    - [Without autorelease](#without-autorelease)
    - [With autorelease](#with-autorelease)
- [Powershield cancel](#powershield-cancel)
    - [Powershield cancel counter](#powershield-cancel-counter)
- [Animation timelines](#animation-timelines)
    - [Shield startup](#shield-startup)
    - [`GuardOn`/` `](#guardon-)
    - [`GuardReflect`/` `](#guardreflect-)
    - [`GuardSetOff`/`GuardDamage`](#guardsetoffguarddamage)
    - [`Guard`/`_` after the complete shield startup animation](#guard--after-the-complete-shield-startup-animation)
    - [`Guard`/`_` after shieldstun](#guard--after-shieldstun)
    - [`GuardOff`/`GuardOff`](#guardoffguardoff)
- [Appendix](#appendix)
    - [Appendix A - Types of inputs by buffer](#appendix-a---types-of-inputs-by-buffer)
    - [Appendix B - Frame flowchart](#appendix-b---frame-flowchart)
- [Work in Progress](#work-in-progress)
- [References used, Additional reading](#references-used-additional-reading)

The basic way(s) to input a shield
----------------------------------

The usual method to input shield is by pressing a shoulder trigger.

A shoulder trigger consists of two parts that are able to input a shield:

- a slider that moves when you apply a light pressure to the trigger: analog input
- a button that you press when you reach the bottom of the trigger: digital input

In-game: starting up the shield
-------------------------------

To start up a shield, you have to input shield during an actionable state, or buffer<sub>(hold)</sub> shield until reaching an actionable frame. 

Your character will start up its shield instantaneously, if it is actionable, or when it becomes actionable.

Right from the first frame of this action, your shield bubble hitbox protects you.

There are ways you are prevented from starting up your shield. Not only there are frames where your character isn't actionable, but it you input an action that is of higher _priority_ than shield startup, your character will do just that.

List of actions that involve inputting shield but have priority over actually starting up the shield:

- Grab; if you input A exactly in the frame you intended to start up the shield, you grab instead.
- Spotdodge; in a Wait state, tap or buffer<sub>(timed + hold)</sub> control stick down, while inputting shield.
- Roll forward; once you begin the dash-forward animation, you cancel your dash into roll-forward by timing shield within frames 2 and 3 of the dash animation. This happens due to the fact that there's a _window extension_ for rolling forward.

Other actions that have a higher priority than your shield start-up:<sup> [ref][buffer]</sup>

- Special moves
- Smash attacks with the C-stick
- Smash turn from Dash
- `Squat` from `RunBrake`

Frames that are not considered as lag, but you can't start up your shield during them:<sup> [ref][buffer]</sup>

- Fourth frame of dash forward.

Buffering A
-----------

There's no buffer for A to grab.

If you hold A before a grab is possible, you can't execute that grab with your controller, until you let go of A.

We call this 'buffering A', as opposed to buffering grab which is not possible.

#### Two ways to buffer A

There's obviously an A button in your controller. We can call this the physical A button.

Pressing or holding Z is the same as pressing or holding Shield + "Virtual A"… or that is what we can call the 'A' part of the Z macro.

Holding the physical A or the "virtual A", before a grab is possible, makes it so that you can't grab until you let go of _both_ buttons. 

By buffering A in this way, you prevent grab, and this enables you to start-up a shield by pressing Z.

Elements of shield
------------------

- Health
- Strength
- Hitbox
	- Size
	- Tilt
	- Physical shield bubble hitbox
	- To be described:
		- Reflect bubble hitbox
		- The powershield effect

What changes shield health?

* (reduces) Damage suffered when the physical shield bubble hitbox gets hit.
* (reduces) Degeneration, any frame the shield is on — not during hitlag or shieldstun though. Degeneration reduces your shield health less when you use a shield of lower strength.
* (increases) Regeneration, in the frames the shield remains turned off.

The shield shrinks as it loses health.

Another factor that determines the shield size is the shield strength at the current moment. Shield sizes are bigger as the shields get _less strong_.

What does shield strength do, upon hit
--------------------------------------

When you block an attack that inflicts shieldstun, your shield loses health first.

These effects also apply:

- Your character gets pushed from the hit (pushback)
- If you were hit by the attacker and not by a projectile, the attacker also gets pushed (attacker pushback), but not if the attacker is airborne.
- You enter hitlag and then shieldstun. Your shield bubble protects you.

All of these effects' magnitudes increase with the hitbox's damage had-it-connected with a player hurtbox.<sup>[ ref][shieldstun is universal]</sup>

They are not increased by the hitbox's damage _on block_ which is sometimes different (as in Marth's Shield Breaker.)<sup>[ ref][shieldstun is universal]</sup>

Shield strength changes the magnitude of these effects. Receiving a hit on a strong shield has these properties:

- less shield health loss,
- less hitlag and shieldstun frames,
- less pushback that you receive,
- more attacker pushback.

Receiving a hit on a low strength shield has these properties:

- more shield health loss,
- more hitlag and shieldstun frames,
- more pushback that you receive,
- less attacker pushback.

The pushback that you receive has a cap.<sup>[ ref][wiki shield pushback]</sup> To illustrate its magnitude: try shielding some attack that can deal 32.5 damage; an attack that deals close to this amount of damage is Bowser's fully charged f-smash. When you shield it, the resulting pushback is the maximum pushback possible, and is always the same no matter what are your shield's properties.

Unlike shield pushback, the attacker pushback magnitude doesn't have an upper limit.<sup> [ref][wiki shield pushback]</sup> Notably, this makes possible the 'kamikaze glitch'.

Shield strength number
----------------------

The strength of a shield ranges from 0.30714 (=43/140) to 1.000 (=140/140).<sup> [ref][wiki shield analog shield data (Melee only)]</sup>

We call the strongest shield **hard shield**, and all other shields are labeled **lightshields**. The smallest value (~0.307) is the weakest possible of the shields.


Input of the shield strength
----------------------------

We review all the ways that the controller inputs shield.

1. Trigger analog
2. Trigger digital
3. Z if grab is locked out (you buffer A)

One way all of these input methods are different is in their manipulation of the shield strength.

1. By increasing the pressure in your trigger analog, you can input every strength possible.
2. By pressing any of the trigger digitals, you give your shield a fixed strength: hard shield/maximum strength.
3. By shielding with Z, you give your shield a fixed strength of 0.350 (=49/140).

#### Strength input conflict-solving

You can input shield by mixing input methods in any combination, over the course of any frame. But only one of the shield strengths sent by your inputs will be chosen. The following will help you know how they're prioritized and chosen:

- If you're using both sliders (two trigger analogs at the same time) and nothing else, the strongest among your two analog inputs will have the higher priority.
- If you're using any slider but you're also pressing digital L or R, the trigger digital takes priority and you get a hard shield.
- If you're shielding with Z, the fixed strength set by the Z shield overrules any other shield strength inputs no matter what those are.
	- Z shield has the highest priority.

Initial strength of the shield
------------------------------

The shield strength in the first couple or so of frames of shielding, also called initial strength, is decided by the shield strength input that has the most priority at the exact moment you start up your shield.

Animations and their associated state
-------------------------------------

- `Guard`/` `

- `GuardReflect`/` ` : Shield startup animation (Powershield)

- `GuardOn`/` ` : Shield startup animation

- `GuardSetOff`/`GuardDamage` : Shieldstun animation

- `GuardOff`/`GuardOff` : Shield release animation

The shield action can only be one of the following two animations during the startup: `GuardOn`/` ` and `GuardReflect`/` `. There are methods to input each.

How to get the `GuardOn`/` ` animation on the first frame of shielding
----------------------------------------------------------------------

Buffered shields start up in the `GuardOn`/` ` animation. Any buffered<sub>(hold)</sub> shield input method, alone or in combination, results in a `GuardOn`/` ` startup shield.

To get a `GuardOn`/` ` shield startup _without_ having to buffer the input, avoid using unbuffered trigger digital inputs, just use one or a combination of the following input methods:

- Shoulder trigger sliders (trigger analog)
- Z shield

How to get the `GuardReflect`/` ` animation on the first frame of shielding
---------------------------------------------------------------------------

To get the `GuardReflect`/` ` animation You must avoid the buffered shield.

To start up a shield with `GuardReflect`/` `, press any of the trigger digitals alone or in combination to other means of shield strength input.

Changing the shield strength
----------------------------

At some point after entering a shield startup animation (or entering the `Guard`/` ` animation after shieldstun), you become able to freely adjust your shield strength frame by frame. You can adjust your shield size even right before the sub-frame your shields are hit. But there are minor quirks with how this works:

- The shield in frame 3 gets assigned the strength that was inputted on frame 2,
- the shield in frame 4 gets assigned the strength that was inputted on frame 3,
- and so on…

To generalize: there is always a one-frame delay from when you input your new desired shield strength, to when it actually goes live. (Technically this mechanism can be understood as a queue that holds 1 input at a time)

Another way to see it is, the game looks up your inputs _a frame into the past_ when setting shield strengths.

The `GuardSetOff`/`GuardDamage` animation
-----------------------------------------

When your physical shield bubble hurtbox gets hit with an attack or a projectile that deals shieldstun, you're forced into the `GuardSetOff`/`GuardDamage` animation. It's an animation that you get locked into during your hitlag frames and your shieldstun frames.

_More details:_ `GuardSetOff`/`GuardDamage` is the final animation in the frame you get hit, but it is never the _intended animation_ in that frame (see appendix B), unless the hit occurred while you were still in hitlag or shieldstun from a previous hit.

Powershield effect in the physical shield bubble hitbox
-------------------------------------------------------

Hits from the attacker (but not projectiles) are powershielded when they come into contact with your with physical shield bubble hitbox, for as long as your _powershield counter_ hasn't run out.

The powershield visuals involve light rays coming from the contact point of the hit.

Physics effects of the powershield are applied on the first frame of `GuardSetOff`/`GuardDamage`:

- Your shield loses no health.
- The pushback that your character undergoes gets multiplied.
	- But recall that the amount of pushback is never able to go past a certain limit.

Additional effects that the powershield has over your character will be touched upon later.

### Powershield counter

Under the right conditions, the powershield countdown starts at 4.

As long as it still hasn't ticked down to zero yet, your physical shield bubble hitbox will powershield upon being hit by the attacker.

This counter decreases by 1 each frame where your final state is:

- `GuardReflect`/` `
- `GuardSetOff`/`GuardDamage` but only in the set of frames that deplete counters. 

The powershield counter doesn't decrease in the `Guard`/` ` state. This causes the phenomenon known as <3% powershielding (heart powershielding). <sup> [ref 1][heart powershielding op] [ref 2][heart powershielding taukhan]</sup>

Projectile on the physical shield bubble hitbox
-----------------------------------------------

If your physical shield bubble hitbox comes into contact with an enemy projectile hitbox, the projectile can be stopped, disappear, or be launched at an upward angle if it hits close enough to the top of your shield bubble. 

You suffer hitlag, shieldstun and pushback from physically shielding projectiles.

Physical _powershielding_ of a projectile doesn't exist: it's only possible to shield them normally, or reflect them with your reflect bubble hitbox.

Reflect hitbox
--------------

The reflect hitbox size is only 75% as large as a physical shield bubble hitbox created under the same health & input strength conditions.

It can only interact with hitboxes of projectiles that you didn't shoot/throw yourself.

When it connects with the projectile, the reflect hitbox emits a blinding light. This is a sign that the projectile was reflected.

Reflecting a projectile is unlike physical powershielding in that it inflicts no positive or negative effect on your character; for starters, you get no change of animation or of state, no hitlag, no shield stun and no pushback.

The reflected projectile is sent at an angle of 180 degrees from its original direction (true for fixed direction projectiles, and gravity influenced projectiles).

You own the projectile once you reflect it. This means that it works as if you shot it/threw it; if the enemy-owned projectile has the property that it can hit anyone except him, then the reflected projectile can hit anyone except _you_.

A reflected projectile can only cause half the original damage.

##### More on the reflect bubble hitbox

Your reflect bubble hitbox has priority over the physical shield bubble hitbox. When both touch an enemy projectile's hitbox, the latter interacts only with the reflect bubble, not the physical shield bubble.

Your reflect bubble hitbox can't connect with a projectile hitbox at a distance; they have to intersect.

Due to the way the various time windows in the game engine interact:

- The reflect hitbox is tied to the initial size of the shield when putting it up.
- The reflect hitbox can't change size once it spawns.

A projectile that deals more than 60% of damage cannot be reflected. Upon contacting your reflect hitbox, you block it but your character enters shieldbreak. <sup>[ ref][reflectors can break]</sup>


Autoshield
----------

Autoshield is a condition that lets you hold up your shield without any shield input necessary from your controller. On the flipside, autoshield makes you unable to easily `GuardOff`/`GuardOff`.

Specifically, autoshield completely prevents you from going from `Guard`/` `, `GuardOn`/` `, or `GuardReflect`/` `, into `GuardOff`/`GuardOff` by letting go of all shield inputs. It also impedes going from `GuardSetOff`/`GuardDamage` into `GuardOff`/`GuardOff` unless you have buffered<sub>(timed)</sub> _autorelease_.

Autoshield is active as long as the _autoshield counter_ hasn't counted down to zero.

When you let go of all shield inputs in your controller, during autoshield, your shield strength remains as the last value you sent to the game.

You're able to spotdodge or roll during an actionable autoshield frame just by tilting your control stick, even if there's no shield input currently. But you can't grab just by pressing A, instead you have to press A + Shield or press Z.

### Autoshield counter

The autoshield countdown begins at 8.

This count decreases by 1 every frame where the animations `GuardReflect`/` `, `GuardOn`/` `, or `Guard`/` ` are the final state in that frame.

Autorelease
-----------

Autorelease is an input that puts your character in `GuardOff`/`GuardOff` as soon as it becomes possible. 

To autorelease, all you need to do is letting go of all your shield inputs while in the `GuardOn`/` `, `Guard`/` `, or `GuardReflect`/` ` _intended animations_, and before your autoshield counter has depleted. 

By nature, autorelease is a buffered input. Autorelease is not lost even if you're launched into the shieldstun animation.

_More details:_ autorelease is an input of the buffer<sub>(timed)</sub> type. You can't cancel your autorelease once you input it. Inputting shield won't work to put you into the `Guard`/` ` animation once `GuardOff`/`GuardOff` is possible. The only way to avoid entering `GuardOff`/`GuardOff` is if you input an animation of higher priority than that.

Inputting the `GuardOff`/`GuardOff` animation
---------------------------------------------

There are four scenarios where you can `GuardOff`/`GuardOff`. 

##### Without autorelease

When not in hitlag or shieldstun, and if autoshield expired (autoshield counter = 0), you can `GuardOff`/`GuardOff` by letting go of shield. `GuardOff`/`GuardOff` occurs in that frame you let go of all shield inputs.

When in the `GuardSetOff`/`GuardDamage` animation (meaning you're under hitlag or shieldstun), and if the autoshield counter = 0, you can buffer<sub>(hold)</sub> shield release by letting go of all shield inputs, though you still can shield out of `GuardSetOff`/`GuardDamage` if you input shield again.

##### With autorelease

If you buffered<sub>(timed)</sub> autorelease,

- it makes your character `GuardOff`/`GuardOff` immediately after `GuardSetOff`/`GuardDamage` shieldstun finishes; but certain other actions are still accessible: see the relevant section.
- if you're still shielding with `Guard`/` `, `GuardOn`/` `, or `GuardReflect`/` ` and you reach the frame where the autoshield counter depletes, you will `GuardOff`/`GuardOff`.

Powershield cancel
------------------

Powershield cancel is when you abruptly get out of the shield release animation (`GuardOff`/`GuardOff`) by inputting any attack, special move, or grab.

A condition to do this is that you must first physically powershield an attack; after that, you have to enter `GuardOff`/`GuardOff` before your _powershield cancel counter_ runs out.

##### Powershield cancel counter

In the right conditions, the powershield cancel countdown will begin at 4.

The count goes down by 1 every frame where `Guard`/` ` is your _intended state_ (see appendix B).

Animation timelines
-------------------

To understand how and when you can apply these points in your frame-by-frame analysis, you may read Appendix B first.

### Shield startup

Variant animations for this action:

- `GuardOn`/` `
- `GuardReflect`/` `

### `GuardOn`/` `

##### Frame 1 of `GuardOn`/` `

Tasks unique to this animation

- Set the initial shield strength
- Spawn physical shield bubble hitbox
	- Size: 1x initial shield size
- Powershield counter = 0

Tasks common to all startup animations

- Autoshield counter = 8
- Powershield cancel counter = 0
- You can displace your shield hitboxes by tilting them

##### Frame 2 of `GuardOn`/` `

Available animations (ranked from highest priority to lowest)

- `GuardReflect`/` ` (condition: your shield was not buffered) (input: timing a trigger digital press on this frame)
- Spotdodge
- Roll
- Jump
- Grab
- `GuardOn`/` ` (continue)

Common tasks

- Make every shield strength input  wait 1 frame inside a queue

##### Frame 3 of `GuardOn`/` `

Available animations (ranked from highest priority to lowest)

- Spotdodge
- Roll
- Jump
- Grab
- `GuardOn`/` ` (continue)

Common tasks

- From this frame onwards, constantly update the shield strength using the inputs that were stored in the queue for 1 frame

##### On `GuardOn`/` ` animation end (total runtime: 8 frames)

Available animations (ranked from highest priority to lowest)

- `GuardOff`/`GuardOff`
- Spotdodge
- Roll
- Jump
- Grab
- `Guard`/` `


### `GuardReflect`/` `

##### Frame 1 of `GuardReflect`/` `

Tasks unique to this animation

- Set the initial shield strength
- Spawn physical shield bubble hitbox
	- Size: 1x initial shield size
- Powershield counter = 4
- Spawn reflect bubble hitbox
	- Size: 0.75x initial shield size

Tasks common to all startup animations

- Autoshield counter = 8
- Powershield cancel counter = 0
- You can displace your shield hitboxes by tilting them

##### Special: Frame 1 of `GuardReflect`/` ` by escaping frame 2 of `GuardOn`/` `

Unique tasks

- Powershield counter = 4
- Spawn reflect bubble hitbox
	- Size: 0.75x initial shield size
- De-spawn your existing physical shield bubble hitbox

Common tasks

- Autoshield counter = 8
- Powershield cancel counter = 0
- You can displace your shield hitboxes by tilting them

##### Frame 2 of `GuardReflect`/` `

Available animations (ranked from highest priority to lowest)

- Spotdodge
- Roll
- Jump
- Grab
- `GuardReflect`/` ` (continue)

Common tasks

- Make every shield strength input wait 1 frame inside a queue

##### Frame 3 of `GuardReflect`/` `

Unique tasks

- De-spawn your existing reflect bubble hitbox
- If you lack a physical shield bubble hitbox, it reappears this frame

Common tasks

- From this frame onwards, constantly update the shield strength using the inputs that were stored in the queue for 1 frame

##### On `GuardReflect`/` ` animation end (total runtime: 8 frames)

Available animations (ranked from highest priority to lowest)

- `GuardOff`/`GuardOff`
- Spotdodge
- Roll
- Jump
- Grab
- `Guard`/` `

### `GuardSetOff`/`GuardDamage`

##### Hitlag frame 1 of `GuardSetOff`/`GuardDamage`

Available animations

- `GuardSetOff`/`GuardDamage` (continue)

Tasks

- Physical shield bubble hitbox stays up in the same stage position it was before hit
- The reflect bubble hitbox despawns if there is one
- Shield SDI is possible during hitlag spent in this animation

- If the hit was from an attacker as opposed to a projectile, and your powershield counter > 0
	- Powershield visuals
	- No shield health loss
	- Multiply your pushback
	- Autoshield counter = 0 (gets cleared)
	- Powershield cancel counter = 4
- else 
	- Normal shield hit visuals
	- Shield loses health
	- Pushback as normal

##### Last hitlag frame of `GuardSetOff`/`GuardDamage`

Tasks:

- Frames of the `GuardSetOff`/`GuardDamage` animation that deplete counters are this frame and all incoming frames

##### First shieldstun frame of `GuardSetOff`/`GuardDamage`

Tasks:

- Physical shield bubble hitbox teleports to its centered no-tilt position

##### On `GuardSetOff`/`GuardDamage` animation end ( : after shieldstun)

Available animations (ranging from highest priority and ending on middle high priority) **on the condition:** buffered autorelease, and, at the same time, powershield cancel counter > 0 

- Special moves
- Grab
- C-stick smash attacks
- Normals and smashes

More available animations (starting from middle low priority and ending on lowest priority)

- Spotdodge (condition: buffered autorelease)
- Jump (condition: buffered autorelease)
- `GuardOff`/`GuardOff` (condition: buffered autorelease)
- `Guard`/` `
- `GuardOff`/`GuardOff` (condition: autoshield counter = 0)

### `Guard`/` ` after the complete shield startup animation

Tasks

- Ongoing processes from previous animation


### `Guard`/` ` after shieldstun

##### Frame 1 of `Guard`/` ` after shieldstun

Tasks

- Shield snaps to control stick tilt
- Make every shield strength input  wait 1 frame inside a queue
- As long as the autoshield counter > 0, keep checking to see if the player buffers<sub>(timed)</sub> an autorelease

##### Frame 2 of `Guard`/` ` after shieldstun

Available animations (ranked from highest priority to lowest)

- `GuardOff`/`GuardOff` (condition: autoshield counter = 0)
- Spotdodge
- Roll
- Jump
- Grab
- `Guard`/` ` (continue)

Tasks

- From this frame onwards, constantly update the shield strength using the inputs that were stored in the queue for 1 frame

### `GuardOff`/`GuardOff`

##### Frame 1 of `GuardOff`/`GuardOff`

Tasks 

- Despawn the physical shield bubble hurtbox (leaves the character unprotected)

##### Frame 2 of `GuardOff`/`GuardOff`

Available animations (ranked from highest priority to lowest)

- Special moves (condition: powershield cancel counter > 0)
- Grab (condition: powershield cancel counter > 0)
- C-stick smash attacks (condition: powershield cancel counter > 0)
- Normals and smashes (condition: powershield cancel counter > 0)
- Spotdodge
- Jump
- `GuardOff`/`GuardOff` (continue)

##### On `GuardOff`/`GuardOff` animation end

The character has access to all the Wait state actions.

##### Total runtime of `GuardOff`/`GuardOff` animation

Source: ["Buffer Mechanics in Melee - Smashboards"][buffer]

1 frame: Sandbag.

14 frames: Peach, Jigglypuff, Zelda and Male Wireframe.

15 frames: Dr Mario, Mario, Luigi, Donkey Kong, Falco, Fox, Ness, Ice Climbers, Kirby, Sheik, Link, Young Link, Pichu and Pikachu.

16 frames: Bowser, Falcon, Ganon, Samus, Mewtwo, Game & Watch, Marth, Roy, Male Wireframe and Giga Bowser.


APPENDIX
========

Appendix A - Types of inputs by buffer
--------------------------------------

Based on the post: [Buffer Mechanics in Melee - Smashboards][buffer]

Buffer: mechanic that lets you "successfully input actions before they can actually be executed, causing the inputs to be carried out the first frame possible" — <cite>SmashWiki</cite>

- No buffer: you must enter the input right in the frame you want to act.
- Timed + hold: enter the input within the valid time window, and do not let go of it until success.
- Timed: do the input once within the valid time window. In this case, your action can't be aborted by un-doing your input, unlike the buffer Timed + hold.
- Hold: inputting under any situation + holding that input, results in your character always carrying out the action.
- Window extension: useful for inputting actions that require input combos, an action A that was executed by partially inputting action B can be canceled into action B by completing the inputs necessary for B within some allowed time window.

In all cases, your action — buffered or not — will _not_ execute if there's an action of higher priority that is set to start in the same frame.

Appendix B - Frame flowchart
----------------------------

#### Frame flowchart (normal)

1. Start
2. Read inputs: current and past (buffers)
3. The state selected because of the input (or the lack of it) is the _intended state_. Its animation is the _intended animation_.
4. Do the actions indicated for the current frame of your _intended animation_
5. If partially spending a frame in your _intended animation_ depletes some counter, here you substract 1 from the count
6. Check if your shield is hit or your hurtbox is hit
	- If _No_:
		1. _Intended animation_ = Final animation. If spending a frame in your final animation depletes some counter, here you substract 1 from the count.
	- If _Yes, and the hit inflicts hitstun/shieldstun_:
		1. Your state and animation change to one of the damage/knockback/tumble family; this will be your final state and final animation.
		2. Do the actions indicated for the first frame of your final animation
7. End, Show frame

#### Frame flowchart (middle of hitlag)

If you're on frames 2 - next-to-final of hitlag

1. Start
2. Read inputs
3. SDI [if applicable][phantom hits sdi]
4. Check if your shield is hit or your hurtbox is hit
	- Does the hit inflict hitstun/shieldstun? _Yes_

	1. Your state and animation change to one of the damage/knockback/tumble family.
	2. Do the actions indicated for the first frame of your final animation
	3. Enter hitlag from the beginning, again
5. End, Show Frame

#### Frame flowchart (final frame of hitlag) (also: hitstun/shieldstun)

1. Start
2. Read inputs
3. The current damage/knockback/tumble state is the _intended state_. Its animation is the _intended animation_
4. Apply steps 4 onwards of ["Frame flowchart (normal)"](#frame-flowchart-normal)


Work in Progress
================

##### Miscellaneous

- If the shield gets hit with a physical attack that doesn't inflict shieldstun (Jigglypuff up-b: Sing) while the powershield counter still has a value of 1 or more, powershield visuals play but your character doesn't enter `GuardSetOff`/`GuardDamage`.<sup> [ref][heart powershielding op]</sup>

- PracticalTAS helped by coining the term _intended state_. He was prompted to, by the question:
    > I've seen that the character obeys my controller input first, entering a temporary character state, and then the game determines if my char gets hit and sends it into a damage state.
    >
    > Of course I can use my controller input to shield before getting hit in the same frame (this sends me into `GuardDamage`). Or I can release shield, to get hit in the same frame and be sent into tumble or some other dmg state, instead of `GuardOff`. 
    >
    > What is the name for this state that answers to my controller input but can be changed by a hit before next frame?

He noted that it was too late to name it because we're not even close to being the first to study the _intended state_.

References used, Additional reading
===================================

- [Buffer Mechanics in Melee - Smashboards][buffer]
- [Magus420's Some stuff - Balance Patch - Smashboards][shieldstun is universal]
- [Phantom Hits + DI = ? - SmashBoards][phantom hits sdi]
- [Shield - SmashWiki, the Super Smash Bros. wiki](https://www.ssbwiki.com/Shield)
- [Heart Shield (Powershield Storing): r/SSBM][heart powershielding op]
- [Melee Myth #130: Reflectors Can Break - YouTube][reflectors can break]
- [Alex's Puff Stuff: Powershields Reference Post](https://alexspuffstuff.blogspot.com/2017/03/powershields-reference-post.html) (some info is outdated)
- [Powershield (PS) - Official Ask Anyone Frame Things Thread - Smashboards](https://smashboards.com/threads/official-ask-anyone-frame-things-thread.313889/page-17#post-18512581)



<!-- hypertext label definitions -->

[buffer]: https://smashboards.com/threads/buffer-mechanics-in-melee.512821/ "Buffer Mechanics in Melee - Smashboards"
[shieldstun is universal]: https://smashboards.com/threads/balance-patch.293025/page-2#post-11787029 "Balance Patch - Smashboards"
[phantom hits sdi]: https://smashboards.com/threads/phantom-hits-di.274763/#post-10274330 "Phantom Hits + DI = ? - SmashBoards"

[wiki shield pushback]: https://www.ssbwiki.com/Shield#Shield_pushback "Shield - SmashWiki, the Super Smash Bros. wiki"
[wiki shield analog shield data (Melee only)]: https://www.ssbwiki.com/Shield#Analog_shield_data_.28Melee_only.29 "Shield - SmashWiki, the Super Smash Bros. wiki"

[heart powershielding op]: https://www.reddit.com/r/SSBM/comments/4yd5kb/heart_shield_powershield_storing/ "Heart Shield (Powershield Storing): r/SSBM"
[heart powershielding taukhan]: https://www.reddit.com/r/SSBM/comments/4yd5kb/comment/d6p8bwy/ "Heart Shield (Powershield Storing): r/SSBM"

[reflectors can break]: https://www.youtube.com/watch?v=ycUF7-UMLMU "Melee Myth #130: Reflectors Can Break - YouTube"

