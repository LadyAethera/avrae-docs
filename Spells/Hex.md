# Hex (non SRD Warlock)
*by Aethera#2228*

Spits out Hex text, subtracts a spell from your spell slots. Will display failure if counter is zero. Displays remaining spell slots. Doesn't check Hex is on your spell list.

Usage: `!hex`

### Code
```  
!alias hex embed
{{level = int("%2%") if ("%*%" != "" and "%1%"=="-l" and "%2%".isdigit() and int("%2%")>0 and int("%2%")<=9) else 1}}
{{slots = get_slots(level)}}
-title "<name> casts Hex!"
-desc "Effect
You place a curse on a creature that you can see within range. Until the spell ends, you deal an extra 1d6 necrotic damage to the target whenever you hit it with an attack. Also, choose one ability when you cast the spell. The target has disadvantage on ability checks made with the chosen ability.

If the target drops to 0 hit points before this spell ends, you can use a bonus action on a subsequent turn of yours to curse a new creature. A *remove curse* cast on the target ends this spell early.

***At Higher Levels.*** When you cast this spell using a spell slot of 3rd or 4th level, you can maintain your concentration on the spell for up to 8 hours. When you use a spell slot of 5th level or higher. you can maintain your concentration on the spell for up to 24 hours."
-f "{{use_slot(level) if slots>0 else "**Cannot cast spell!**\n"}}{{slots_str(level)}}"
-footer "Hex | PHB 251" -color <color> -thumb <image>
```
