# Disc-Style Freeplay

The files that will be modified:

* Alphabet.hx
* FreeplayState.hx

## 0.6.2 AND UNDER
### Step 1: Modifying `Alphabet.hx`
To start this off, go to line 24.

Underneath that line, add this:
```hx
public var targetX:Float = 0;
```

Then under these lines:
```hx
public var yMult:Float = 120;
public var xAdd:Float = 0;
public var yAdd:Float = 0;
```

Add these:
```hx
public var itemType:String = "";
public var isMenuItemCentered:Bool = false;
```

After that, go to `override function update(elapsed:Float)`.

Now, underneath that, add this line:
```hx
var scaledY = FlxMath.remapToRange(targetY, 0, 1, 0, 1.3);
```

Then, remove the duplicate line in `if (isMenuItem)`.

After:
```hx
y = FlxMath.lerp(y, (scaledY * yMult) + (FlxG.height * 0.48) + yAdd, lerpVal);
			if(forceX != Math.NEGATIVE_INFINITY) {
				x = forceX;
			} else {
				x = FlxMath.lerp(x, (targetY * 20) + 90 + xAdd, lerpVal);
			}
		}
```

Add:
```hx
if (isMenuItemCentered)
			{
				var lerpVal:Float = CoolUtil.boundTo(elapsed * 9.6, 0, 1);
				y = FlxMath.lerp(y, (scaledY * yMult) + (FlxG.height * 0.48) + yAdd, lerpVal);
				if(forceX != Math.NEGATIVE_INFINITY) {
					screenCenter(X);
				} else {
					screenCenter(X);
				}
			}

		switch (itemType)
		{
		case "Classic":
			y = FlxMath.lerp(y, (scaledY * 120) + (FlxG.height * 0.48), 0.16);
			x = FlxMath.lerp(x, (targetY * 20) + 90, 0.16);

		case "Vertical":
			y = FlxMath.lerp(y, (scaledY * 120) + (FlxG.height * 0.5), 0.16);
			x = FlxMath.lerp(x, (targetY * 0) + 308, 0.16);
			x += targetX;

		case "C-Shape":
			y = FlxMath.lerp(y, (scaledY * 65) + (FlxG.height * 0.39), 0.16);

			x = FlxMath.lerp(x, Math.exp(scaledY * 0.8) * 70 + (FlxG.width * 0.1), 0.16);
			if (scaledY < 0)
				x = FlxMath.lerp(x, Math.exp(scaledY * -0.8) * 70 + (FlxG.width * 0.1), 0.16);

			if (x > FlxG.width + 30)
				x = FlxG.width + 30;
		case "D-Shape":
			y = FlxMath.lerp(y, (scaledY * 90) + (FlxG.height * 0.45), 0.16);

			x = FlxMath.lerp(x, Math.exp(scaledY * 0.8) * -70 + (FlxG.width * 0.35), 0.16);
			if (scaledY < 0)
				x = FlxMath.lerp(x, Math.exp(scaledY * -0.8) * -70 + (FlxG.width * 0.35), 0.16);

			if (x < -900)
				x = -900;
		}
```

And that's it for Alphabet.hx.

### Step 2: Modifying `FreeplayState.hx`
Now for this, underneath:
```hx
songText.isMenuItem = true;
```

Add:
```hx
songText.itemType = 'D-Shape';
```

And you're done.

## 0.6.3

### Step 1: Modifying `Alphabet.hx`
Go to line 30.

Underneath that line, add this:
```hx
public var targetX:Float = 0;
```

Then add these lines:
```hx
public var yMult:Float = 120;
public var xAdd:Float = 0;
public var yAdd:Float = 0;
```

And these also:
```hx
public var forceX:Float = Math.NEGATIVE_INFINITY;
public var itemType:String = "";
public var isMenuItemCentered:Bool = false;
```

After that, go to `override function update(elapsed:Float)`.

Now, underneath that, add this line:
```hx
var scaledY = FlxMath.remapToRange(targetY, 0, 1, 0, 1.3);
```

Then, after:
```hx
var lerpVal:Float = CoolUtil.boundTo(elapsed * 9.6, 0, 1);
			if(changeX)
				x = FlxMath.lerp(x, (targetY * distancePerItem.x) + startPosition.x, lerpVal);
			if(changeY)
				y = FlxMath.lerp(y, (targetY * 1.3 * distancePerItem.y) + startPosition.y, lerpVal);
```

Add:
```hx
if (isMenuItemCentered)
			{
				var lerpVal:Float = CoolUtil.boundTo(elapsed * 9.6, 0, 1);
				y = FlxMath.lerp(y, (scaledY * yMult) + (FlxG.height * 0.48) + yAdd, lerpVal);
				if(forceX != Math.NEGATIVE_INFINITY) {
					screenCenter(X);
				} else {
					screenCenter(X);
				}
			}

		        switch (itemType)
		        {
		        case "Classic":
			y = FlxMath.lerp(y, (scaledY * 120) + (FlxG.height * 0.48), 0.16);
			x = FlxMath.lerp(x, (targetY * 20) + 90, 0.16);

		        case "Vertical":
			y = FlxMath.lerp(y, (scaledY * 120) + (FlxG.height * 0.5), 0.16);
			x = FlxMath.lerp(x, (targetY * 0) + 308, 0.16);
			x += targetX;

		        case "C-Shape":
			y = FlxMath.lerp(y, (scaledY * 65) + (FlxG.height * 0.39), 0.16);

			x = FlxMath.lerp(x, Math.exp(scaledY * 0.8) * 70 + (FlxG.width * 0.1), 0.16);
			if (scaledY < 0)
				x = FlxMath.lerp(x, Math.exp(scaledY * -0.8) * 70 + (FlxG.width * 0.1), 0.16);

			if (x > FlxG.width + 30)
				x = FlxG.width + 30;
		        case "D-Shape":
			y = FlxMath.lerp(y, (scaledY * 90) + (FlxG.height * 0.45), 0.16);

			x = FlxMath.lerp(x, Math.exp(scaledY * 0.8) * -70 + (FlxG.width * 0.35), 0.16);
			if (scaledY < 0)
				x = FlxMath.lerp(x, Math.exp(scaledY * -0.8) * -70 + (FlxG.width * 0.35), 0.16);

			if (x < -900)
				x = -900;
		        }
```

And that's it for Alphabet.hx.

### Step 2: Modifying `FreeplayState.hx`
Underneath:
```hx
songText.isMenuItem = true;
```

Add:
```hx
songText.itemType = 'D-Shape';
```

And you're done.

[SCREENSHOT GOES HERE]
