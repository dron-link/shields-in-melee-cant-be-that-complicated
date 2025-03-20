
powershield mechanics compendium (v1 from 20 March 2025)
========================================================

The two basic ways to input a shield
------------------------------------

The usual method to input shield is by pressing a shoulder trigger.

A shoulder trigger consists of two parts that are able to input a shield:

- a slider that moves when you apply a light pressure to the trigger: trigger analog
- a button that you press when you reach the bottom of the trigger: trigger digital

In game: how to Put-up Shield 
-----------------------------

To Put-up a shield, you have to input shield. If you're actionable your character will put up his shield immediately.

The only ways you're prevented from putting-up shield if you're actionable:

- If you're less than 3 frames into dash and you input roll forward or buffer (hold) roll forward
- If you're in wait or walk and you input spotdodge or buffer (hold) spotdodge
- If you do an A press or Z press exactly in the frame you intended to put up the shield. This results in grab.

Frame 1 of putting up shield prevents any actions that are not the three ones described above.

Buffering A
-----------

There's no buffer for A to grab.

If you hold A before a grab is possible, you can't execute that grab with your controller, until you let go of A.

We call this buffering A, as opposed to buffering grab which is not possible.

#### Two ways to buffer A

There's obviously an A button in your controller. We can call this the physical A button.

Pressing or holding Z is the same as pressing or holding [Shield + "Virtual A"], or that is what i call the other type of A.

Holding the physical A or the "virtual A", before a grab is possible, makes it so that you can't grab until you have let go of _both_. 

By buffering A in this way, you prevent grab, and this means you can put-up a shield pressing Z.

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

* (reduces) Damage, when the physical shield bubble hitbox gets hit
* (reduces) Decay, any frame the shield is on
* (increases) Regeneration, in the frames the shield remains turned off

The shield inevitably shrinks as it loses health.

Another factor controlling the size of the shield is its strength. A shield is overall bigger (and particularly, its shield bubble is bigger) if it is _less strong_.

What does shield strength do, upon hit
--------------------------------------

When your shield bubble is hit with an attack that inflicts shieldstun, you enter hitlag.

After hitlag ends, these are three things that happen:

- you undergo shieldstun frames where you keep your shield online but do not have any control over your character
- your character gets pushed from the hit (pushback)
- if you were hit by the attacker and not by a projectile, the attacker also gets pushed (attacker pushback), but not if the attacker is airborne.

All of these effects are increased by the hit's power.

Shield strength also changes the magnitude of these effects:

- Attack on a stronger shield means
	- less shieldstun frames,
	- less pushback,
	- more attacker pushback.
- Attack on a weaker shield means
	- more shieldstun frames,
	- more pushback,
	- less attacker pushback.

Shield pushback magnitude has a cap. To illustrate its magnitude: i'll let you know that you _almost reach it_ by hard shielding some attack that can deal 32.5 damage; an example of such an attack is Bowser's fully charged f-smash.

Unlike shield pushback, the attacker pushback magnitude doesn't have a limit.

Shield strength number
----------------------

The strength of a shield ranges from 0.307 (=43/140) to 1.000 (=140/140)

We call the strongest shield a **hard shield**, and all other shields are called **lightshields**. 0.307 would be the weakest possible lightshield.

Input of the shield strength
----------------------------

We review all the ways that the controller inputs shield.

1. Trigger analog
2. Trigger digital
3. Z if grab is locked out

One way all of these input methods are different is in their control over the strength of the shield.

1. By increasing the pressure you put on a shoulder trigger slider, you can input any strength. From the minimum, to the maximum.
2. By pressing the button that is deep inside L or R, you give your shield a fixed strength, the maximum or hard shield strength.
3. By shielding with Z, you give your shield a fixed strength of 0.350 (=49/140).

#### Strength input conflict-solving

You can input shield by mixing input methods in any combination in any frame. But only one of the sent shield strengths prevails; this is how you know which one:

- If you're using both sliders, (two trigger analogs at the same time) and nothing else, the strongest slider takes priority.
- If you're using any slider but you're also pressing digital L or R, the trigger digital takes priority and you get a hard shield.
- If you're shielding with Z, the fixed strength of the Z shield overrides any other shield strength inputs no matter what they are.
	- Z shield has the highest priority.

Initial strength of the shield
------------------------------

The shield strength in the first couple of frames of the shield, is decided by the shield strength input that has the most priority at the exact moment you put-up your shield.

Buffered shield
---------------

if you input a shield when you can't put it up yet, and _later_ you become actionable while you held shield, your character puts-up the shield with the current strength you're inputting, without taking into account strengths inputted earlier. It's just as you could expect, but as it turns out the game will remember the fact you buffered the shield.

The shield states' internal names
---------------------------------

- `GuardOn`
- `GuardReflect`
- `GuardDamage`
- `GuardOff`

A shield that was just put-up is of one of the two following types: `GuardOn` and `GuardReflect`. There are methods to input each.

How to put-up a shield, using GuardOn
-------------------------------------

Buffered shields are put-up in the `GuardOn` state. As it turns out, this is the only way that a shield you put-up with your 'Trigger Digital' can begin in `GuardOn`.

To put-up a `GuardOn` shield without buffering the shield, use one or a combination of the following input methods:

- Shoulder trigger sliders (trigger analog)
- Z shield.

How to put-up a shield, using GuardReflect
------------------------------------------

Avoid the buffered shield.

To put-up a `GuardReflect` shield, press any of the trigger digitals alone or in combination to other shield input methods.

Changing the shield strength
----------------------------

At some point after entering `GuardReflect` or `GuardOn` you become able to freely adjust your shield strength any time you want, or so you're told. But there are minor quirks with how this works:

- The shield in frame 3 gets assigned the strength that was inputted between frames 1-2,
- the shield in frame 4 gets assigned the strength that was inputted between frames 2-3,
- the shield in frame 5 gets assigned the strength that was inputted between frames 3-4,
- and so on…

To generalize, the game actually looks one frame in the past when setting your shield strength.

Another way to see it is as a one-frame delay, from when you input your new desired shield strength, and when it actually goes live in your shield.

This doesn't happen when you put-up your shield, because its strength is determined by the current strength input.

GuardDamage state
-----------------

`GuardDamage` is a state that you get locked into during your hitlag frames and your shieldstun frames.

Powershield effect in the physical shield bubble hitbox
-------------------------------------------------------

Hits from the attacker (but not projectiles) are powershielded when they come into contact with your with physical shield bubble hitbox, for as long as your _powershield counter_ hasn't ran out.

Effects of the powershield are applied on the first frame of hitlag.

The powershield animation involves light rays coming from the contact point of the hit.

The pushback that your character undergoes is multiplied.

Your shield loses no health.

Additional effects of the powershield will be touched upon later.

On the other hand, you get none of these effects with a projectile as there is no way to physically powershield them.

Powershield counter
-------------------

When you input a `GuardReflect`, the powershield counter begins at 4.

As long as you have not counted down to zero yet, your physical shield bubble hitbox will powershield upon being hit by the attacker.

This counter decreases by 1 after every frame in `GuardReflect`, by 1 when you get inflicted hitlag and sent into `GuardDamage`, and by 1 for every shieldstun frame spent in `GuardDamage`. 

It doesn't decrease in the `GuardOn` state.

Reflect hitbox
--------------

The reflect hitbox size is only 75% as large as a physical shield bubble hitbox.

It can only interact with hitboxes of projectiles that you didn't shoot/throw yourself.

When it connects with the projectile, the reflect hitbox emits a blinding light. This is a sign that the projectile was reflected.

Reflecting a projectile inflicts no effect on your character; you get no hitlag, no shield stun, and no pushback.

The reflected projectile is sent into the opposite direction. You also own this projectile (this means it works as if you shot it/threw it); because of that, it can hit your opponent. 

A reflected projectile can only cause half the original damage.

This reflect hitbox has priority over the physical shield bubble hitbox. When the two overlap **on a projectile hitbox**, the projectile interacts with the reflect hitbox, not the physical shield bubble.

Due to the way the various time windows in the game engine interact:

- The reflect hitbox is tied to the initial size of the shield when putting it up.
- The reflect hitbox can't change size once it spawns.

In the same frame, what connects first: a hitbox from an attack or a hitbox from a projectile?
----------------------------------------------------------------------------------------------

(This was conjectured from the result of carrying a test with Peach turnip + bair)

In the same frame, the hitbox from your attacker has precedence over an enemy projectile. Even if you touch a projectile hitbox with your reflect bubble hitbox, an attacker hitbox can and will interact with your physical shield bubble first, sending your character into the `GuardDamage` state.

Inside `GuardDamage`, you lose your reflect hitbox, because of this, there's no chance of reflecting a projectile; you end up blocking the projectile using the physical shield bubble.

GuardOff state
--------------

`GuardOff` is a state that you eventually fall into if you stop inputting shield and do not input any action out of `GuardOn`, out of `GuardOff` or out of `GuardDamage`.

Clingy shield counter
---------------------

The clingy shield counter begins at 8.

This counter decreases by 1 every frame of `GuardReflect` and every frame of `GuardOn`.

As long as it doesn't reach zero or isn't reset to zero, you won't be able to `GuardOff` out of `GuardOn` or `GuardReflect`.

But there exists a way to `GuardOff` after `GuardDamage` which will be touched upon later.

Powershield cancel
------------------

Powershield canceling is when you exit the `GuardOff` state by inputting any attack or special move.

A condition to do this is that you must enter `GuardOff` before your _powershield cancel counter_ runs out.

Powershield cancel counter
--------------------------

Begins with a value of 4 and counts down from there.

The counter goes down by 1 after every frame you spend in `GuardOn`. It also goes down by 1 for every hit you suffer that sends you into `GuardDamage`.

If you enter `GuardOff` before this counter runs out, you can powershield cancel that `GuardOff`.

Complete timeline of shield
---------------------------

Information: Carry out all the steps described for your current `GuardOn` or `GuardReflect` frame before checking if the physical shield bubble hitbox gets hit. 

If the shield gets hit — with the resulting hitlag + shieldstun being greater than zero frames — the character gets into the `GuardDamage` state, instead of staying in `GuardOn` or `GuardReflect`. (You will have to skip to the section [Hitlag and shieldstun, a.k.a. GuardDamage state](#hitlag-and-shieldstun-aka-guarddamage-state) and follow its Frame 1 steps too.)

#### Put-up shield

To put-up shield, first carry the calculation of the initial shield strength and size. Also, find out which state you will enter: `GuardOn`, or `GuardReflect`? 

Then, follow the respective steps for frame 1.

#### Path you follow for as long as you don't undergo hitlag / shieldstun

- Frame 1 of `GuardOn`
	- The physical shield bubble hitbox spawns.
	- The Powershield counter is reset to zero.
- Frame 1 of `GuardReflect`
	- Spawn the reflect bubble hitbox.
	- Spawn the physical shield bubble hitbox, but only if you _did_ put-up your shield using `GuardReflect`
	- The following counter begins:
		- Powershield counter (is set to 4).
- Frame 1 All:
	- The following counter begins:
		- Clingy shield counter (is set to 8)
- Frame 2 of `GuardOn`
	- If the shield isn't a buffered shield:
		- Here, if you begin pressing any of the trigger digitals, alone or in combination to other shield input methods, you return to "Frame 1 of `GuardReflect`" right after you read this instruction, while keeping in mind that you _did **not**_ access `GuardReflect` by putting-up your shield using it.
- Frame 2 All:
	- All out of shield options are accessible from now on.
- Frame 3 of `GuardReflect`
	- Set the shield as a physical shield bubble hitbox, with no reflect bubble hitbox (the latter just despawns).
- Frame 3 All:
	- Shield strength becomes able to be adjusted; your shield is no longer locked to initial shield strength
- Frame 7 of `GuardReflect`:
	- Your character goes into `GuardOn`. This has no noticeable effect. 

- If the clingy shield counter reaches zero:
	- You have a new action available to you: going into `GuardOff` by stopping all of your shield inputs 

#### Hitlag and shieldstun, a.k.a. GuardDamage state

- Frame 1 of hitlag in `GuardDamage`:
	- If the hit was from an attacker as opposed to a projectile, and your powershield counter hasn't run out yet
		- You powershield the hit
		- The clingy shield counter is reset to zero
	- If you didn't powershield this hit, your shield loses health
	- The physical shield bubble hitbox active will be kept on this position during all of `GuardDamage`
	- Despawn the reflect hitbox, if there was one
- After final frame of hitlag:
	- Enter shieldstun
- Frame 1 of shieldstun:
	- Teleport the shield hitbox to the character's center. This hitbox can't be tilted until your character exits `GuardDamage`
- If you're hit again during the hitlag or shieldstun:
	- Go back to "Frame 1 of hitlag in `GuardDamage`"
	
The following determines what state your character enters, after the final frame of shieldstun ends.

- If the clingy shield counter is not zero:
	- If there _was_ a shield input present in frame 1 of hitlag, the character will enter `GuardOn`, continuing with the current clingy shield count.
	- If there was no shield input present in frame 1 of hitlag, the character will enter `GuardOff`
- If the clingy shield counter is zero, your character will enter `GuardOn` or `GuardOff` depending on if you are inputting shield or not at the moment of this decision.
	- If you are exiting the `GuardDamage` of a physical powershield, the following counter begins:
		- Powershield cancel counter (set to 4)

#### GuardOn after shieldstun

- Frame 1:
	- Re-tilt the shield bubble hitbox.

- Any frame after the clingy shield counter reaches zero:
	- You are able to enter `GuardOff` by stopping all of your shield inputs 

- Frame 2:
	- Shield strength becomes able to be adjusted; your shield is no longer locked to the strength it had upon hit.

#### GuardOff

- Frame 1:
	- The `GuardOff` animation plays out for this frame, and no actions are available.
	- Your physical shield bubble hitbox despawns.
- Frame 2:
	- From now on you can exit this `GuardOff` by inputting an OOS option.
	- If the powershield cancel counter didn't run out, powershield cancel becomes accessible from this frame onwards.
- After frame 15:
	- The `GuardOff` animation ends: you are fully actionable.

