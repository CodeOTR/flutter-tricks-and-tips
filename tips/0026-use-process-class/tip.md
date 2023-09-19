# Use the Process Class to Run Executables
You can use the [Process](https://api.dart.dev/stable/3.1.0/dart-io/Process-class.html) class to run just about any executable with any arguments in a Dart app.

```bash
await Process.run('flutter', ['create', appName, '--empty', '--org', orgName ]);

await Process.run('flutter', ['pub', 'get']);

await Process.run('flutter', ['build', 'appbundle', '--release', '--no-sound-null-safety']);
```

This also works for non-Flutter executables:

```bash
await Process.run('ls', ['-l']);

await Process.run('git', ['commit', '-m', 'commit message']);
```