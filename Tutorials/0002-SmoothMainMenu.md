# Smooth Main Menu

The files that will be modified:

* MainMenuState.hx

## How to do It

First of all, after:
```hx
private var camGame:FlxCamera;
private var camAchievement:FlxCamera;
```

Add these:
```hx
public static var firstStart:Bool = true;
public static var finishedFunnyMove:Bool = false;
```

Then, replace:
```hx
var scr:Float = (optionShit.length - 4) * 0.135;
if(optionShit.length < 6) scr = 0;
menuItem.scrollFactor.set(0, scr);
```

With:
```hx
menuItem.scrollFactor.set(0, 1);
```

And last but not least, underneath:
```hx
menuItem.updateHitbox();
```

Add:
```hx
if (firstStart)
					FlxTween.tween(menuItem,{y: 60 + (i * 160)},1 + (i * 0.25) ,{ease: FlxEase.expoInOut, onComplete: function(flxTween:FlxTween) 
						{
							finishedFunnyMove = true; 
							changeItem();
						}});
				else
					menuItem.y = 60 + (i * 160);
```

And there you go.

[SCREENSHOT GOES HERE]