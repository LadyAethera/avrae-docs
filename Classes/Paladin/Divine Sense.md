# Divine Sense
*updated by Aethera#2228*

Spits out Divine Sense text, subtracts from Divine Sense counter, creating counter if none exists. Will display failure if counter is zero. Displays remaining dice pool.

Usage: `!divinesense`

### Code
```  
!alias divinesense embed
{{set("counter", "Divine Sense")}}
{{create_cc_nx(counter, 0, 1+charismaMod, "long", "bubble")}}
-title "<name> focuses{{" but can't sense anything" if get_cc(counter)<=0 else " their Divine Sense"}}."
-desc "{{"The presence of strong evil registers on your senses like a noxious odor, and powerful good rings like heavenly music in your ears. As an action, you can open your awareness to detect such forces. Until the end of your next turn, you know the location of any celestial, fiend, or undead within 60 feet of you that is not behind total cover. You know the type (celestial, fiend, or undead) of any being whose presence you sense, but not its identity (the vampire Count Strahd von Zarovich, for instance). Within the same radius, you also detect the presence of any place or object that has been consecrated or desecrated, as with the hallow spell." if get_cc(counter)>0 else "While usually strong evil and powerful good register clearly on your senses, right now you're not getting much of a reading from your surroundings. There could be nothing there, or you might just be tired."}}

You can use this feature {{1+charismaMod}} times. When you finish a long rest, you regain all expended uses."
-f "{{mod_cc(counter, -1, True) if get_cc(counter)>0 else ""}}{{counter}}|{{cc_str(counter)}}"
-footer "Paladin | PHB 84" -color <color> -thumb <image>
```
