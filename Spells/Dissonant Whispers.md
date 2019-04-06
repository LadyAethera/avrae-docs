# Dissonant Whispers (non SRD Warlock)
*by Aethera#2228*

Spits out Dissonant Whispers text, subtracts a spell from your spell slots. Will display failure if counter is zero. Displays remaining spell slots. Doesn't check if this is on your spell list. If you don't want to have to type the level each time, replace the first line of code with {{level = #}} and save the alias again.

Usage: `!whispers -l #`

### Code
```  
!alias whispers embed
{{level = int("%2%") if ("%*%" != "" and "%1%"=="-l" and "%2%".isdigit() and int("%2%")>0 and int("%2%")<=9) else 1}}
{{slots = get_slots(level)}}
-title "<name> casts Dissonant Whispers!"
-desc "Effect
You whisper a discordant melody that only one creature of your choice within range can hear, wracking it with terrible pain. The target must make a Wisdom saving throw, **DC {{8+proficiencyBonus+charismaMod}}**. On a failed save, it takes 3d6 psychic damage (+1d6/higher levels) and must immediately use its reaction, if available, to move as far as its speed allows away from you. The creature doesn't move into obviously dangerous ground, such as a fire or a pit. On a successful save, the target takes half as much damage and doesn't have to move away. A deafened creature automatically succeeds on the save.{{"\n\n**Damage:** "+str(vroll(str(2+level)+"d6")) if slots>0 else ""}}"
-f "{{use_slot(level) if slots>0 else "**Cannot cast spell!**\n"}}{{slots_str(level)}}"
-footer "Dissonant Whispers | PHB 234" -color <color> -thumb <image>
```
