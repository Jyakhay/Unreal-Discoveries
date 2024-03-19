## Tab Spawner
Tab spawners are used to create the window that your window slate will be drawn onto, they're fairly simple to create and use.

A tab spawner can be registered through;
```cpp
FGlobalTabManager::Get()->RegisterTabSpawner
(
	FName("TabID",
	FOnSpawnTab::CreateStatic(&OnTabSpawned))
)
```

Tabs may be spawned in as such:
```
FGlobalTabManager::Get()->TryInvokeTab(FName("TabID"));
```

Spawning in a tab will then call the OnTabSpawned callback above which has the following function signature:
```cpp
TSharedRef<SDockTab> OnTabSpawned(const FSpawnTabArgs& Args)
```

Within the callback, you may then fill the new window with your custom slate widget:
```cpp
TSharedRef<SDockTab> FMyClass::OnTabSpawned(const FSpawnTabArgs& Args)
{
	return SNew(SDockTab)
	.TabRole(NomadTab)
	[
		SNew(SMyCustomWindowSlate)
	]
}
```

## Window Slate Content

A compound widget class is used to fill the window contents like so:
```cpp
struct SMyWindowContent : public SCompountWidget
{
	SLATE_BEGIN_ARGS(SMyWindowContent)
	{
	}
	SLATE_END_ARGS()

	void Construct(const FArguments& InArgs);
}
```

The construct method is where the custom slate is created, however it may modified at any time during the window's lifespan.

```cpp
void SMyWindowContent::Construct(const FArguments& InArgs)
{
	this->ChildSlot
	[
		//Add in window contents.
	]
}
```