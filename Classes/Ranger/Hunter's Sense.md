# Hunter's Sense (Monster Slayer)
*by Aethera#2228*

Spits out Hunter's Sense text, subtracts from Hunter's Sense counter, creating counter if none exists. Will display failure if counter is zero. Displays remaining uses.

Usage: `!huntersense`

### Code
```  
!alias huntersense embed
{{set("counter", "Hunter's Sense")}}
{{create_cc_nx(counter, 0, max(1,wisdomMod), "long", "bubble")}}
-title "<name> focuses{{" but can't sense anything" if get_cc(counter)<=0 else " their Hunter's Sense"}}."
-desc "{{"You can peer at a creature and magically discern how best to hurt it. As an action, choose one creature you can see within 60 feet of you. You immediately learn whether the creature has any damage immunities, resistances, or vulnerabilities and what they are. If the creature is hidden from divination magic, you sense that it has no damage immunities, resistances, or vulnerabilities." if get_cc(counter)>0 else "While usually you can sense the vulnerabilities of most creatures, right now you're not getting much of a reading from your target. There could be nothing there, or you might just be tired."}}

You can use this feature {{max(1,wisdomMod)}} time{{"s" if max(1,wisdomMod)>1 else ""}}. You regain all expended uses of it when you finish a long rest."
-f "{{mod_cc(counter, -1, True) if get_cc(counter)>0 else ""}}{{counter}}|{{cc_str(counter)}}"
-footer "Monster Slayer | XGE 43" -color <color> -thumb <image>
```
