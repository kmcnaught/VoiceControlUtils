# VoiceAttack references and script snippets

### Get spoken command as a string.
This is the exact variant recognised, e.g. if the command phrase is: `step [left;right;up;down] [1..9]` then the spoken command could be `"step left 2"` or `"step up 4"` for example. 
```
string command = VA.Command.Name();
```
This is used in all of the below code snippets, you do not need to use it by itself. 

### Convert direction to WASD
If the spoken command contains "left", "right", "forward", "forwards", "backwards" or "back", this will convert to a direction key (W, A, S, D) and save the key name in the variable `DirectionKey`

```	
string command = VA.Command.Name();
		
if (command.ToLower().Contains("left")) {
  VA.SetText("DirectionKey", "A");
} else if (command.ToLower().Contains("right")) {
  VA.SetText("DirectionKey", "D");
} else if (command.ToLower().Contains("forward")) {
  VA.SetText("DirectionKey", "W");	
} else if (command.ToLower().Contains("back")) {	
  VA.SetText("DirectionKey", "S");					
}
```


### Convert direction to controller inputs
If the spoken command contains "left", "right", "forward", "forwards", "backwards" or "back", this will convert to the corresponding key for joystick holds via the SpecialEffect Titan script (w,g,h,b) or (t,c,y,v).

For 100% stick holds:

```
string command = VA.Command.Name();
		
if (command.ToLower().Contains("left")) {
  VA.SetText("DirectionKey", "g");
} else if (command.ToLower().Contains("right")) {
  VA.SetText("DirectionKey", "h");
} else if (command.ToLower().Contains("forward")) {
  VA.SetText("DirectionKey", "w");	
} else if (command.ToLower().Contains("back")) {	
  VA.SetText("DirectionKey", "b");					
}
```

or, for 50% stick holds:
```	
string command = VA.Command.Name();
		
if (command.ToLower().Contains("left")) {
  VA.SetText("DirectionKey", "c");
} else if (command.ToLower().Contains("right")) {
  VA.SetText("DirectionKey", "v");
} else if (command.ToLower().Contains("forward")) {
  VA.SetText("DirectionKey", "y");	
} else if (command.ToLower().Contains("back")) {	
  VA.SetText("DirectionKey", "z");					
}
```

You would use the output in VoiceAttack, with commands like:
`Press down variable key(s) [{DirectionKey}]` 



### Convert direction to arrow keys
If the spoken command contains "up", "down", "left", "right", convert to arrow keys and save the key name in the variable `DirectionKey`. Note that the keys have specific identifiers and need square brackets. A full list of possible key names can be found in the `Quick Input, Variable Keypress and Hotkey Key Indicators` section of the VoiceAttack manual (press F1 in VoiceAttack, look around page 164). 

```
string command = VA.Command.Name();
		
if (command.ToLower().Contains("left")) {
  VA.SetText("DirectionKey", "[ARROWL]");
} else if (command.ToLower().Contains("right")) {
  VA.SetText("DirectionKey", "[ARROWR]");
} else if (command.ToLower().Contains("up")) {
  VA.SetText("DirectionKey", "[ARROWU]");	
} else if (command.ToLower().Contains("down")) {	
  VA.SetText("DirectionKey", "[ARROWD]");				
}
```

You would use the output in VoiceAttack, with commands like:
`Press down variable key(s) [{DirectionKey}]` 

### Get number from command
If command contains a number, extract it and save to the variable `RepeatCount`. If no number is found, `RepeatCount` is set to 1.
```
string command = VA.Command.Name();

char[] arr = command.ToCharArray();			
arr = Array.FindAll<char>(arr, (c => (char.IsDigit(c)))); // extract digits only from string
string str = new string(arr);

int counter = 0;
if (Int32.TryParse(str, out counter)) {
  VA.SetInt("RepeatCount", counter);		
} else {
  VA.SetInt("RepeatCount", 1);						
}
```

You would use the output as a loop count in VoiceAttack, for instance:
`Start Loop : Repeat [{RepeatCount}] Times`
