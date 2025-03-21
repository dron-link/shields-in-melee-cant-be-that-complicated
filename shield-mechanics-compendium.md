
shield mechanics compendium (v1.0.1 from 20 March 2025)
=======================================================

thanks to: the work of taukhan, kadano, alexs puff stuff, schmooblidon, practicaltas, deep blue c, B&D Games

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

- If you're in a `Wait` state and you input shield + control stick down, you spotdodge
- If you input shield before frame 2 or frame 3 of your dash forward animation, you will roll forward regardless of your control stick position
- If you do an A press or Z press exactly in the frame you intended to put up the shield, you grab.

Frame 1 of putting up shield prevents realizing any actions other than the ones listed above.

Buffering A
-----------

There's no buffer for A to grab.

If you hold A before a grab is possible, you can't execute that grab with your controller, until you let go of A.

We call this buffering A, as opposed to buffering grab which is not possible.

#### Two ways to buffer A

There's obviously an A button in your controller. We can call this the physical A button.

Pressing or holding Z is the same as pressing or holding [Shield + "Virtual A"], or that is what i call the other type of A.

Holding the physical A or the "virtual A", before a grab is possible, makes it so that you can't grab until you let go of _both_ inputs. 

By buffering A in this way, you prevent grab, and this enables you to put-up a shield by pressing Z.

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

Shield pushback has a cap. To illustrate its magnitude: try hard shielding some attack that can deal 32.5 damage; an attack that deals close to this amount of damage is Bowser's fully charged f-smash. When you shield it, the resulting pushback is the maximum pushback possible.

Unlike shield pushback, the attacker pushback magnitude doesn't have an upper limit.

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

The shield strength in the first couple of frames of the shield, is decided by the shield strength input that has the most priority at the exact moment you put-up your shield.

Buffered shield
---------------

if you input a shield when you can't put it up yet, and _later_ you become actionable while you're still holdind shield, the game will take into account the fact you buffered the shield.

Yet, the specific shield strength values you inputted earlier are not remembered, just the fact that you buffered shield. Your character will still put-up the shield with the strength you're currently inputting at that moment.

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

At some point after entering `GuardReflect` or `GuardOn` you become able to freely adjust your shield strength any time you want. You can adjust your shield size even right before the sub-frame your shields are hit. But there are minor quirks with how this works:

- The shield in frame 3 gets assigned the strength that was inputted between frames 1-2,
- the shield in frame 4 gets assigned the strength that was inputted between frames 2-3,
- the shield in frame 5 gets assigned the strength that was inputted between frames 3-4,
- and so on…

To generalize: there is a one-frame delay from when you input your new desired shield strength, to when it actually goes live.

Another way to see it is that the game looks up your inputs _a frame into the past_ when reading your shield strength inputs.

GuardDamage state
-----------------

`GuardDamage` is a state that you get locked into during your hitlag frames and your shieldstun frames, when the thing that was hit is your physical shield bubble hurtbox.

Powershield effect in the physical shield bubble hitbox
-------------------------------------------------------

Hits from the attacker (but not projectiles) are powershielded when they come into contact with your with physical shield bubble hitbox, for as long as your _powershield counter_ hasn't run out.

The powershield visuals involve light rays coming from the contact point of the hit.

Physics effects of the powershield are applied on the first frame of `GuardDamage`:

- Your shield loses no health.
- The pushback that your character undergoes gets multiplied.
	- But recall that the amount of pushback is never able to go past a certain limit.

Additional effects that the powershield has over your character will be touched upon later.

Projectile on the physical shield bubble hitbox
-----------------------------------------------

If your physical shield bubble hitbox comes into contact with an enemy projectile hitbox, the projectile can be stopped, disappear, or be launched at an upward angle if it hits close enough to the top of your shield bubble. 

You suffer hitlag, shieldstun and pushback from physically shielding projectiles.

Physical powershielding of a projectile doesn't exist: it's only possible to shield them normally, or reflect them with your reflect bubble hitbox.

Powershield counter
-------------------

When you input a `GuardReflect`, the powershield counter begins at 4.

As long as you have not counted down to zero yet, your physical shield bubble hitbox will powershield upon being hit by the attacker.

This counter decreases by 1 after every frame in `GuardReflect`, by 1 when you get hit with an attack that inflicts you shieldstun, and by 1 for every shieldstun frame spent in `GuardDamage`. 

It doesn't decrease in the `GuardOn` state.

Reflect hitbox
--------------

The reflect hitbox size is only 75% as large as a physical shield bubble hitbox.

It can only interact with hitboxes of projectiles that you didn't shoot/throw yourself.

When it connects with the projectile, the reflect hitbox emits a blinding light. This is a sign that the projectile was reflected.

Reflecting a projectile inflicts no effect on your character; you get no hitlag, no shield stun, and no pushback.

The reflected projectile is sent at an angle of 180 degrees from its original direction (true for fixed direction projectiles, and gravity influenced projectiles). You also own this projectile (this means that it works as if you shot it/threw it); if the enemy-owned projectie has the property that it can hit anyone except him, then the reflected projectile can hit anyone except _you_.

A reflected projectile can only cause half the original damage.

Your reflect hitbox has priority over the physical shield bubble hitbox. When both touch an enemy projectile's hitbox, the latter interacts only with the reflect bubble, not the physical shield bubble.

Your reflect bubble hitbox can't connect with a projectile hitbox at a distance; they have to intersect.

Due to the way the various time windows in the game engine interact:

- The reflect hitbox is tied to the initial size of the shield when putting it up.
- The reflect hitbox can't change size once it spawns.

A projectile that deals more than 60% of damage cannot be reflected. Upon contacting your reflect hitbox, you defend from it but your character enters shieldbreak.

GuardOff state (shield release)
-------------------------------

`GuardOff` is a state that you _eventually_ fall into if you lift all of your shield inputs and do not input any action out of `GuardOn`, out of `GuardOff` or out of `GuardDamage`.

There are different ways to enter `GuardOff`.

Autoshield
----------

Autoshield is a condition that lets you hold up your shield without any shield input necessary from your controller. Specifically, autoshield makes you unable to `GuardOff` out of `GuardOn` or out of `GuardReflect`.

Autoshield is active as long as the _autoshield counter_ hasn't counted down to zero.

When you let go of shield during autoshield, your shield strength stays as the last valid strength value you sent to the game.

You can spotdodge or roll during an autoshield frame just by tilting your control stick, even if there's no shield input currently. But you can't grab unless you press Z, or A + Shield.

Autoshield counter
------------------

The autoshield counter begins at 8.

This counter decreases by 1 every frame of `GuardReflect` and every frame of `GuardOn`.

Autorelease
-----------

Autorelease happens when you fulfill both conditions:

- You let go of all your shield inputs in any one frame of `GuardOn`, `GuardRelease` or the first hitlag frame
- You enter `GuardDamage` with an autoshield counter of at least 1.

If you autorelease, you will enter `GuardOff` after `GuardDamage` ends.

Powershield cancel
------------------

Powershield canceling is when you exit the `GuardOff` state by inputting any attack, special move, or grab.

A condition to do this is that you must enter `GuardOff` before your _powershield cancel counter_ runs out.

Powershield cancel counter
--------------------------

The powershield cancel counter goes down by 1 after every frame you spend in `GuardOn`. It also goes down by 1 for every hit you suffer that inflicts shieldstun.

If you enter `GuardOff` before this counter runs out, you can powershield cancel that `GuardOff`.

Complete timeline of shield
---------------------------

Carry out all the steps described for your current `GuardOn` or `GuardReflect` frame, before checking if the physical shield bubble hitbox gets hit. 

If the shield gets hit with a hitbox that inflicts shieldstun, you can't end your frame yet. Your character gets into the `GuardDamage` state, so you will have to skip to the section [Hitlag and shieldstun, a.k.a. GuardDamage state](#hitlag-and-shieldstun-aka-guarddamage-state) and follow its steps beginning from Frame 1.

If the shield gets hit with a physical attack that doesn't inflict shieldstun (Jigglypuff up-b: Sing) while the powershield counter still has a value of 1 or more, powershield visuals play but your character doesn't enter `GuardDamage`.

#### Put-up shield

When your character puts up its shield, first carry the calculation of the initial shield strength and size. (The initial shield strength cannot be changed from this initial value, until the game allows it). Also, you have to find out which state you will put-up your shield with: `GuardOn`, or `GuardReflect`? 

The counters that are always reset to zero before putting up shield are:

- Powershield counter
- Powershield cancel counter

#### Shield timeline for as long as your character doesn't suffer shieldstun

- Frame 1 of `GuardOn`
	- The physical shield bubble hitbox spawns.
- Frame 1 of `GuardReflect`
	- Spawn the reflect bubble hitbox.
	- Spawn the physical shield bubble hitbox, but only if you _did_ put-up your shield using `GuardReflect`
	- The following counter begins:
		- Powershield counter (is set to 4).
- Frame 1 All:
	- The following counter begins:
		- Autoshield counter (is set to 8)

- Frame 2 of `GuardOn`
	- If the shield isn't a buffered shield:
		- Here, if you begin pressing any of the trigger digitals (alone or in combination to other shield input methods), you return to "Frame 1 of `GuardReflect`" right after you read this instruction, while keeping in mind that you _did **not**_ put-up your shield by using `GuardReflect`.
- Frame 2 All:
	- All out of shield options are accessible from now on.

- Frame 3 of `GuardReflect`
	- Set the shield as a physical shield bubble hitbox, with no reflect bubble hitbox (the latter just despawns right now).
- Frame 3 All:
	- Your character lets its shield strength be changed by you, from now on.

- Frame 7 of `GuardReflect`:
	- Your character enters into `GuardOn`. This has no noticeable effect. 

- Any frame, if the autoshield counter reaches zero:
	- You have a new action available to you: going into `GuardOff` by stopping all of your shield inputs.

#### Hitlag and shieldstun, a.k.a. GuardDamage state

Note: you can't change your shield strength during GuardDamage.

- Frame 1 of hitlag in `GuardDamage`:
	- If the hit was from an attacker as opposed to a projectile, and your powershield counter hasn't run out yet
		- You powershield the hit
		- Visuals of physical powershield play
		- The autoshield counter is reset to zero
	- If you didn't powershield this hit, your shield loses health
	- If there is a reflect bubble hitbox, it despawns
	- The physical shield bubble hitbox freezes in its current place (relative to your body)

- After final frame of hitlag:
	- Enter shieldstun

- Frame 1 of shieldstun:
	- Teleport the shield hitbox to the character's center. This hitbox can't be tilted until your character exits `GuardDamage`

- If you're hit again during the hitlag or shieldstun:
	- Go back to step "Frame 1 of hitlag in `GuardDamage`"
	
The following determines what state your character enters, after shieldstun ends.

- If the autoshield counter hasn't run out:
	- If you did let go of all your shield inputs in any one frame of `GuardOn`, `GuardRelease` or the first hitlag frame, you will autorelease into `GuardOff`

	- Otherwise, the character will enter `GuardOn`, continuing the current autoshield count from where it left off.
- If the autoshield counter is zero, your character will enter `GuardOn` or `GuardOff` depending on if you are inputting shield or not in your last frame of shieldstun.
	- If you powershielded this last hit, the following counter begins:
		- Powershield cancel counter (set to 4)

#### GuardOn after shieldstun

- Frame 1:
	- Re-tilt the shield bubble hitbox.
	- All of your actions OOS are available

- Frame 2:
	- Shield strength becomes able to be adjusted; your shield is no longer locked to the strength it had upon hit.

- Any frame after the autoshield counter reaches zero:
	- You are able to enter `GuardOff` in the current frame, by stopping all of your shield inputs 

#### GuardOff

- Frame 1 if Autorelease:
	- At any time, you can input or buffer: jump or spotdodge, to cancel `GuardOff`
- Frame 1 All:
	- Your physical shield bubble hitbox despawns.

- Frame 2:
	- At any time, you can input or buffer: jump or spotdodge, to cancel `GuardOff`
	- If the powershield cancel counter didn't run out before you entered `GuardOff`, you can powershield cancel this state.

- After frame 14-16 depending on character:
	- The `GuardOff` state ends: you are fully actionable.

Work in progress
================

W.I.P.: What happens when the attacker connects with your shield bubble + you attempt to reflect at the same time?
------------------------------------------------------------------------------------------------------------------

The answer to this is open (for me). You need to set up experiments, or look into the characters' hitbox data, in order to answer: does the game check first if the physical attack's hitboxes hit your shield bubble? Or are the projectile hitboxes checked first?

I know that if the physical attack connects with your hitbox first, then the game puts your character inside the first frame of `GuardDamage`. Here, you lose your reflect hitbox; and because of this, there's no chance to reflect a projectile in this frame. You end up blocking the projectile using the physical shield bubble.

I don't know what happens on the reverse.
