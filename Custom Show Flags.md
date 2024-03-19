## Show Flags
Show flags are toggleable values that can be set through an FEngineShowFlags struct.
Show flags that are set through the console, are within the Game Viewport Client and can be retrieved through:
```cpp
GetWorld()->GetGameViewport()->GetEngineShowFlags()
```

Examples of show flag commands Include:
```
Show Collision
Show Bloom
Show Bounds

Show (Shows the state of all show flags)
```

## Custom Show Flags
Custom show flags can be created through a constructing a static FShowLevelZonesFlag.
The value of the custom show flag can be retrieved as such:

```cpp
static TCustomShowFlag<> MyShowFlag(TEXT("ShowFlagName"), false, SFG_Custom);
...

if(MyShowFlag.IsEnabled(*GetWorld()->GetGameViewport()->GetEngineShowFlags()))
{
	//Flag Is enabled.
}
else
{
	//Flag is not enabled.
}
```