# Magic Missile Fix
*by Aethera#2228*

Usage: `!mm` or `!mm -l [cast-at level]`

### Setup
None. This should work with your existing character sheet, though it doesn't actually check to make sure you know the spell.

### Code
```GN
!alias mm embed
{{d1 = roll("1d4")}}{{d2 = roll("1d4")}}{{d3 = roll("1d4")}}{{d4 = roll("1d4")}}{{d5 = roll("1d4")}}{{d6 = roll("1d4")}}{{d7 = roll("1d4")}}{{d8 = roll("1d4")}}{{d9 = roll("1d4")}}{{d10 = roll("1d4")}}{{d11 = roll("1d4")}}
{{level = int("%2%") if ("%*%" != "" and "%1%"=="-l" and "%2%".isdigit() and int("%2%")>0 and int("%2%")<=9) else 1}}
{{good = 1 if get_slots(level)>0 else 0}}
{{use_slot(level) if good else ""}}
-title "<name> casts Magic Missile!"
-desc "{{" \n**Damage:** "+str(max(3,2+level))+" darts, d4+1 each. [**"+str(d1+1)+", "+str(d2+1)+", "+str(d3+1)+(", "+str(d4+1) if 2+level>=4 else "")+(", "+str(d5+1) if 2+level>=5 else "")+(", "+str(d6+1) if 2+level>=6 else "")+(", "+str(d7+1) if 2+level>=7 else "")+(", "+str(d8+1) if 2+level>=8 else "")+(", "+str(d9+1) if 2+level>=9 else "")+(", "+str(d10+1) if 2+level>=10 else "")+(", "+str(d11+1) if 2+level>=11 else "")+"**]\n\nEach dart hits a creature of your choice that you can see within range. A dart deals 1d4+1 force damage to its target. The darts all strike simultaneously and you can direct them to hit one creature or several." if (good==1) else "No spell slots of that level available to spend, so sad! Better luck next time." if (good==0) else "Something strange is going on here. Contact your broker for alternate spell options."}}"
-f "{{slots_str(level)}}"
-footer "Magic Missile | PHB 257" -color <color> -thumb <image>
```
