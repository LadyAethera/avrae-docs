# Primeval Awareness
*By Aethera#2228.*

Spits out Primeval Awareness text, uses a spell slot, and will reject the command if there are no spell slots to burn.

Usage: `!primeval [args]`
Args: `-l [slot level]` (optional; defaults to level 1, if available)

### Code
```GN
!alias primeval embed
{{ lvl = 1 if "&*&"=="" else int("&2&") if ("&1&"=="-l" and "&2&".isdigit() and int("&2&")>0 and int("&2&")<=9) else 1 }}
{{good = 1 if (get_slots(lvl)>0 and lvl<=9) else 0}}
-title "<name> {{"magically extends their Primeval Awareness using a level "+str(lvl)+" spell slot!" if good else "doesn't have the magical strength to fuel Primeval senses."}}"
-desc "{{"Beginning at 3rd level, you can use your action and expend one ranger spell slot to focus your awareness on the region around you." if good==0 else "You expend a level "+str(lvl)+" spell slot to focus your awareness on the region around you."}} For {{"1 minute per level of the spell slot you expend" if good==0 else "For the next "+(str(lvl) if lvl>1 else "")+" minute"+("s" if lvl>1 else "")}}, you can sense whether the following types of creatures are present within 1 mile of you (or within up to 6 miles if you are in your favored terrain): aberrations, celestials, dragons, elementals, fey, fiends, and undead. This feature doesn't reveal the creatures' location or number."
-f "{{use_slot(lvl) if good else ""}}{{slots_str(lvl)}}"
-footer "Ranger | PHB 92" -color <color> -thumb <image>
```
