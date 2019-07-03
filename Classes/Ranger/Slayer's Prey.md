# Slayer's Prey
*By Aethera#2228.*

Spits out Slayer's Prey text for Monster Hunter rangers, creating counter if necessary, and will reject the command if it has been used already.

### Code
```GN
!alias slayersprey embed
{{set("counter", "Slayer’s Prey")}}
{{create_cc_nx(counter, 0, 1, "short", "bubble")}}
{{ target = " at %2%" if ("%*%"!="" and "%1%"=="-t") else "" }}
-title "<name> {{"cannot focus their ire on their prey" if get_cc(counter)<=0 else " focuses their Slayer's Prey ire"}}."
-desc "{{"Starting at 3rd level, you can focus your ire on one foe, increasing the harm you inflict on it. As a bonus action, you designate one creature you can see within 60 feet of you as the target of this feature. The first time each turn that you hit that target with a weapon attack, it takes an extra 1d6 damage from the weapon." if get_cc(counter)>0 else "While usually you can focus your talents against most creatures, right now you're just not feeling it. There could be something impeding you, or you might just be tired."}}

This benefit lasts until you finish a short or long rest. It ends early if you designate a different creature."
-f "{{mod_cc(counter, -1, True) if get_cc(counter)>0 else ""}}{{counter}}|{{cc_str(counter)}}"
-footer "Monster Slayer | XGE 43" -color <color> -thumb <image>```
