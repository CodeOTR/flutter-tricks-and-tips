# Await Multiple Futures
Use the [Future.wait](https://api.flutter.dev/flutter/dart-async/Future/wait.html) method to wait for multiple futures to complete 🕦🕝🕑

The response from Future.wait is a list of the results in the order you specified them. This is useful for cases when your UI depends on several backend calls.

```dart
FutureBuilder(                                            
  future: Future.wait([                                   
    Future.delayed(const Duration(seconds: 1), () => '1'),
    Future.delayed(const Duration(seconds: 2), () => '2'),
    Future.delayed(const Duration(seconds: 3), () => '3'),
  ]),                                                     
  builder: (context, snapshot) {                          
    if (snapshot.hasData) {                               
      return Text(snapshot.data.toString());              
    } else {                                              
      return const CircularProgressIndicator();           
    }                                                     
  },                                                      
),
```