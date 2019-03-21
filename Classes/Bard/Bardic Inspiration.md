# Bardic Inspiration
*by Aethera#2228*

Subtracts from Bardic Inspiration counter, creating counter if none exists. Spits out the text for different inspiration uses based on arguments, and size of die based upon character level. Displays remaining dice pool. Limited based on 2k character limit.

Usage: `!inspire [args]`

Optional Args: `-cutting` (Cutting Words, College of Lore)

### Code
```  
!alias inspire embed  
{{set("counter", "Bardic Inspiration")}}
{{create_cc_nx(counter, 0, max(1,charismaMod), "long", "default")}}
{{use = 1 if get_cc(counter)>=1 else 0}}
{{mod_cc(counter,-1,"True") if use==1 else ""}}
{{set("die","d6") if level<5 else set("die","d8") if level<10 else set("die","d10") if level<15 else set("die","d12")}}
{{cutt = 0 if "%*%"=="" else 1 if ("%1%"=="-cutting"or "%2%"=="-cutting" or "%3%"=="-cutting") else 0}}
-title "<name> {{"calls upon inspiring words and music!" if (use==1 and cutt==0) else "spins a string of insults!" if (use==1 and cutt==1) else"fails to call on her magic."}}"
{{yes = "You can inspire others with words or music. A creature other than yourself in 60 feet who can hear you gains one Bardic Inspiration die, a "+die+".\n\nIn the next 10 minutes, they can roll the die and add the number rolled to one check, attack, or save, before or after the d20 is rolled, but before the GM determines success."}}{{roll = vroll(die)}}{{sad = "You can use your wit to distract, confuse, and undermine others. When a creature you can see within 60 feet of you makes an attack roll, an ability check, or a damage roll, you can expend one use of Bardic Inspiration, and subtract the number rolled from the creature’s roll. It must be after the creature makes its roll, but before the GM determines success, or before the creature deals its damage. The creature is immune if it can’t hear you or if it’s immune to being charmed.\n\n**Cutting Words:** subtract "+str(roll)}}{{"-desc \"Unfortunately, there are only so many times per day this will work, and this is not one of those times. You need to rest.\"" if use==0 else "-desc \""+yes+"\"" if cutt==0 else "-desc \""+sad+"\""}}
{{"-f \"Action|Bonus Action\"" if (use==1 and cutt==0) else "-f \"Action|Reaction\"" if (use==1 and cutt==1) else ""}}
{{"-f \""+counter+"|"+str(get_cc(counter))+"/"+str(get_cc_max(counter))+"\""}}
-footer "Bard | PHB 53"
-color <color> -thumb <image>
```
