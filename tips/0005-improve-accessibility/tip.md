# Improve Accessibility
You can drastically improve the accessibility of your application using a few simple widgets.

1. Wrap unlabeled parts of your UI with the [Semantics](https://api.flutter.dev/flutter/widgets/Semantics-class.html) widget to give users more information about its purpose.
```agsl
Semantics(                             
  label: 'Power',                      
  child: Switch(                       
    value: true,                       
    onChanged: (value) => print(value),
  ),                                    
),                                       
```

2. Use [MergeSemantics](https://api.flutter.dev/flutter/widgets/MergeSemantics-class.html) to group widgets in the Semantics tree. When a screen reader is used, the following example will read as "This is a MergedSemantics example"
```agsl
const MergeSemantics(                             
  child: Column(                                  
    children: [                                   
      ListTile(                                   
        title: Text('This is a '),                
      ),                                           
      ListTile(                                   
        title: Text('MergedSemantics example'),   
      ),                                           
    ],                                            
  ),                                               
)                                                  
```

3. Update your UI when a screen reader is being used by checking the "[accessibleNavigation](https://api.flutter.dev/flutter/widgets/MediaQueryData/accessibleNavigation.html)" flag on MediaQuery. Some gestures, like tapping outside of a modal to close it, aren't as obvious when using Android's TalkBack or iOS' VoiceOver.
```agsl
showDialog(
  context: context,
  builder: (context) => AlertDialog(
    title: const Text('Dialog Title'),
    content: const Text('Dialog Content'),
    actions: [
      if (MediaQuery.of(context).accessibleNavigation)
        TextButton(
          onPressed: () => Navigator.of(context).pop(),
          child: const Text('Cancel'),
        ),
    ],
  ),
);
```