# Increment Build Number with Perl
Use perl to increment your app's build number in Fastlane and CI/CD pipelines.

This ensures the built-in Flutter variables (ex. $(FLUTTER_BUILD_NUMBER)) aren't replaced with hardcoded values.

```ruby
lane :bump do
    Dir.chdir("../..")
    sh("perl","-i","-pe","s/(version:\\s+\\d+\\.\\d+\\.)(\\d+)(\\+)(\\d+)$/$1.($2+1).$3.($4+1)/e", "pubspec.yaml")
    Dir.chdir("android/fastlane")
end
```
This was inspired by this [GitHub comment](https://github.com/flutter/flutter/issues/41955#issuecomment-601266745).