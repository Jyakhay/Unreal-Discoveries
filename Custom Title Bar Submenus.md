![[Images/MainMenuImage.png]]
The bar at the top of Unreal containing the menus above is referred to as the Main Menu within the engine. 

The main menu can be extended to have custom submenus through the UToolMenus module as so:
```cpp
UToolMenu* MainMenu = UToolMenus::Get()->ExtendMenu("MainFrame.MainMenu");
UToolMenu* CustomSubMenu = MainMenu->AddSubMenu
(	
	"MainMenu",
	NAME_None,
	"SubMenuTitle",
	LOCTEXT("SubMenuLabel", "Label"),
	LOCTEXT("SubMenu_Tooltip", "MyTooltop")
);
```

Main menu extensions are typically done through a module struct, within StartupModule().
## Sections
![[Images/SectionsImage.png]]
Submenus are split into multiple sections as seen in the image above, the sections are:
- Open
- Save
- Import/Export
- Project
- Exit

Sections can be added very simply:
```cpp
CustomSubMenu->AddSection("MySectionName", FText::FromString("MySectionLabel"));
```

From here, you can add addition submenus to the newly created submenu, or you can add menu entries, which act as button:
```cpp
CustomSubMenu->AddMenuEntry
(
	FName("OwningSectionName"),
	FToolMenuEntry::InitMenuEntry
		(
			FName("EntryName"),
			FText::FromString("Entry Label"),
			FText::FromString("Entry tooltip"),
			FSlateIcon(),
			FUIAction(FExecuteAction::CreateStatic(&MyCallback))
		)
)
```

The callback is executed when the user clicks on the menu entry.