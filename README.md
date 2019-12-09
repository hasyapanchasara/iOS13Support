# iOS13Support
Things to take care for giving iOS 13 Support

Dear Friends,

I am going to keep writting important points to be taken care while giving support of iOS 13 to your iOS App.

# (1) Theme ( Light / Dark )
With quick support, you can add below key and value to your Info.plist file to restrcit to 1 particular theme.
```
<key>UIUserInterfaceStyle</key>
<string>Light</string>
```

# (2) Set status bar color 
If you face any such app crash for startus bar like below. You can check iOS 13 condition and apply status bar color this way.

Problem : App crash log
````
*** Terminating app due to uncaught exception 'NSInternalInconsistencyException', reason: 'App called -statusBar or -statusBarWindow on UIApplication: this code must be changed as there's no longer a status bar or status bar window. Use the statusBarManager object on the window scene instead.'
````

Solution : code - Objective C
````
if (@available(iOS 13, *)){

    UIView *statusBar = [[UIView alloc]initWithFrame:[UIApplication sharedApplication].keyWindow.windowScene.statusBarManager.statusBarFrame] ;
    statusBar.backgroundColor = [UIColor clearColor]; //set whatever color you like
    [[UIApplication sharedApplication].keyWindow addSubview:statusBar];

}
else{
    
    UIView *statusBar = [[[UIApplication sharedApplication] valueForKey:@"statusBarWindow"] valueForKey:@"statusBar"];
    
    if ([statusBar respondsToSelector:@selector(setBackgroundColor:)]) {
        statusBar.backgroundColor = [UIColor clearColor]; //set whatever color you like
    }
    
}
`````

# (3) UITextField search crash

Problem : App crash log
`````
 *** Terminating app due to uncaught exception 'NSGenericException', reason: 'Access to UISearchBar's _searchField ivar is prohibited. This is an application bug'


Solution : code - Objective C - Just need to remove _ ( underscore ) :)
````
\\ OLD Code 
UITextField *searchField = [searchBar valueForKey:@"_searchField"]; 

\\ iOS 13 Compatible code
UITextField *searchField = [searchBar valueForKey:@"searchField"];
````
