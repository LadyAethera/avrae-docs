Second Wind: regain vroll("d10+"+level) HP
Combat Superiority check/update PHB 73
Maneuvers PHB 74


# Second Wind (Fighter)
*by Aethera#2228*

Spits out Second Wind text, updates 1/rest counter. Will display failure if counter is zero. Updates your HP for you, no need for a second command. Passing the argument '-info' will display the text without rolling or attempting to use the ability.

Usage: `!secondwind [-info]`

### Setup

**Important!** If you are a multiclass character, you must check that your Fighter level is saved separately from your total class level. (I believe the DiceCloud and GSheet v2.0 sheets both do this automatically, but I can only speak to the GSheet.) Run `!test <FighterLevel>` and it will tell you if it's set up or not. If it's not, you'll need to do this manually, replacing the number after *FighterLevel* as appropriate, and adding a separate variable for whatever other class you have. The code below is written as Fighter 3 / Warlock 1 for clarity.
```
!multiline
!cvar multiclass True
!cvar FighterLevel 3
!cvar WarlockLevel 1
```
If it becomes a problem updating them each time you level, DM me and let me know to automate it better. Scripts written by me should check that all class level variables add up to your total level and return an error if not, but other coders won't know how I've set this up, and older code by me won't have this built in.

### Code
```  
!alias secondwind embed
{{go = 1 if get("multiclass",0)==0 else 1 if get("ArtificerLevel",0)+get("BarbarianLevel",0)+get("BardLevel",0)+get("ClericLevel",0)+get("DruidLevel",0)+get("FighterLevel",0)+get("MonkLevel",0)+get("MysticLevel",0)+get("PaladinLevel",0)+get("RangerLevel",0)+get("RogueLevel",0)+get("SorcererLevel",0)+get("WarlockLevel",0)+get("WizardLevel",0)==level else err('`Multiclass levels not properly defined. Please check that all your levels are saved individually as ClericLevel, FighterLevel, etc.`')}}
{{info = 1 if "%*%"=="-info" else 0}}
{{lvl = get("FighterLevel",0) if get("FighterLevel",0)>=1 else level}}
{{set("counter", "Second Wind")}}
{{create_cc_nx(counter, 0, 1, "short", "bubble")}}
-title "{{name+" tries to rally but finds themselves winded." if (get_cc(counter)<=0 and info==0) else "Fighter: Second Wind" if info==1 else name+" finds their Second Wind!"}}"
-desc "{{"You have a limited well of stamina that you can draw on to protect yourself from harm. On your turn, you can use a bonus action to regain hit points equal to 1d10 + your fighter level ("+str(lvl)+")." if (get_cc(counter)>0 or info==1) else "While usually you can rally to fight longer, at the moment you must be tired, for you find no well of energy to draw upon."}} You {{"can use your Second Wind once and then you" if (get_cc(counter)<=0 or info==1) else ""}} must rest before using {{"it" if (get_cc(counter)<=0 or info==1) else "Second Wind"}} again."
{{rolls = vroll("d10+"+str(lvl))}}
{{"-f \"Healing Received | "+str(rolls)+"\"" if (go==1 and info==0 and get_cc(counter)>0) else ""}}
{{set_hp(min(get_hp()+rolls.total,hp)) if (go==1 and info==0 and get_cc(counter)>0) else ""}}
{{"-f \"Hit Points | "+hp_str()+"\"" if (go==1 and info==0 and get_cc(counter)>0) else ""}}
{{mod_cc(counter, -1, True) if (get_cc(counter)>0 and info==0) else ""}}
-footer "Fighter | PHB 72" -color <color> -thumb <image>
```
