VoiceAttack allows you to write really flexible phrases to trigger an action. For instance, you might 
sometimes say "go up", but sometimes naturally just say "up". You can tell VoiceAttack to accept both
options. 

VoiceAttack uses square brackets `[` and semi-colons `;` to define complex phrases, with the following rules:
- Anything without brackets (or outside of brackets) is compulsory  

e.g. `say hello world` will only trigger if the entire phrase "say hello world" is spoken

- Square brackets contain alternative words or phrases - you must include one of the options from the list

e.g. `good [morning; afternoon; evening]` will trigger for "good morning", "good afternoon" or "good evening"

- For part of the phrase to be optional, you need an empty item in the list inside the square brackets

e.g. `good [morning; afternoon; evening; ]` will also trigger for "good" on its own

- Number ranges can also be included, with `..` to define an inclusive range

e.g. `jump [1..3]` will trigger for "jump 1", "jump 2" or "jump 3"

## Examples

`hello [there; world]`
accepts "hello there" or "hello world"

`hello [there; world;]`
accepts "hello there" or "hello world" or "hello"

`hello [;there; world]`
accepts "hello" or "hello there" or "hello world"

(i.e. the empty thing in the list can be at the start or the end)

`[good;] [morning; afternoon; evening] [to you;]`
accepts "good morning", "morning", "good morning to you"
               "good afternoon", "afternoon", "good afternoon to you"
               "good evening", "evening", "good evening to you"

`I am [3,5,7] years old`
accepts "I am 3 years old", "I am 5 years old", "I am 7 years old"

`I am [3..5] years old`
accepts "I am 3 years old", "I am 4 years old", "I am 5 years old"

(i.e. the double dots means anything within the range is accepted)

`I am [;3..5] years old`
accepts "I am 3 years old", "I am 4 years old", "I am 5 years old" or "I am years old"

