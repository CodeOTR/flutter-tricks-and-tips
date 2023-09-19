# Programmatically Open the Scaffold Drawer
If you are inside a context that contains a Scaffold with a Drawer, you can programmatically open and close it via the nearest `ScaffoldState`.
```dart
Scaffold.of(context).openDrawer();

Scaffold.of(context).closeDrawer();
```
Equivalent methods exist for the end drawer (for right-to-left users, this drawer appears on the right side of the screen):
```dart
Scaffold.of(context).openEndDrawer();

Scaffold.of(context).closeEndDrawer();
```

The Scaffold widget also has an `onDrawerChanged` property that can be used to listen for drawer state changes. This can be used to create some interesting animations:

<img src="drawer.gif"  height="700"/>

Full Code:

```dart
class DrawerTip extends StatelessWidget {
  DrawerTip({Key? key}) : super(key: key);

  ValueNotifier<bool> open = ValueNotifier(false);

  void setOpen(bool val) => open.value = val;

  double drawerWidth = 100;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Drawer Tip')),
      drawer: Drawer(
        width: drawerWidth,
        child: ListView(
          children: const [
            ListTile(title: Text('One')),
            ListTile(title: Text('two')),
          ],
        ),
      ),
      drawerScrimColor: Colors.red.withOpacity(.2),
      onDrawerChanged: (val) => setOpen(val),
      body: ValueListenableBuilder(
        valueListenable: open,
        builder: (context, open, child) {
          return Stack(
            children: [
              AnimatedPositioned(
                duration: const Duration(milliseconds: 300),
                curve: Curves.easeInOut,
                left: open ? drawerWidth + 20 : 0,
                child: Column(
                  children: [
                    TextButton(
                        onPressed: () {
                          Scaffold.of(context).openDrawer();
                        },
                        child: const Text('Open Drawer')),
                  ],
                ),
              ),
            ],
          );
        },
      ),
    );
  }
}
```

## Troubleshooting
If you are not inside a context that contains a Scaffold, you'll see a super clear message telling you what the issue is:
```agsl
Scaffold.of() called with a context that does not contain a Scaffold.
```
You can fix this by wrapping your widget in any other widget that adds a new BuildContext layer (ex. Builder, ValueListenableBuilder, ListenableBuilder, etc).