# app_color

Flutter package widening a Color class which can be used to create, convert, compare colors and uses
in UI. And also for working with editing color

```dart
// Usage hex from string and alternative color systems

void main() {
  AppColor.fromHex('000000'); // -> Color(0xFF000000)
  AppColor.fromHsl(164, 100, 88); // -> Color(0xFFC2FFEF)
  AppColor.fromXYZ(0.1669, 0.2293, 0.0434); // -> Color(0xFF659027)
  AppColor.fromCielab(36.80, 55.20, -95.61); // -> Color(0xFF4832F7)

  // Make color darker or lighter
  Color(0xFF000000).lighter(100); // -> Color(0xFFFFFFFF)
  Color(0xFF000000).darker(50); // -> Color(0xFF808080)

  // Mix with other colors
  Color(0xFFFF0000).mix(Color(0xFF00FF00), .25); // -> Color(0xFFBF3F00)

  // Colors conversion
  Color
      .fromRGBO(255, 255, 255, 1)
      .asHex; // -> '#FFFFFFFF'
}
```

## Getting Started

In your flutter project add the dependency:

```yaml
dependencies:
  app_color: any
```

## Examples

```dart
void main() {
  // HexColor
  assert(AppColor.fromHex('000000') == Color(0xFF000000));
  assert(AppColor.fromHex('#000000') == Color(0xFF000000));
  assert(AppColor.fromHex('FFFFFFFF') == Color(0xFFFFFFFF));
  assert(AppColor.fromHex('#B1000000') == Color(0xB1000000));
  assert(AppColor
      .fromHex('#B1000000')
      .asHex == '#B1000000');

  // HslColor
  assert(AppColor.fromHsl(164, 100, 88) == Color(0xFFC2FFEF));

  // HyzColor
  assert(AppColor.fromXYZ(0.1669, 0.2293, 0.0434) == Color(0xFF659027));

  // CielabColor
  assert(AppColor.fromCielab(36.80, 55.20, -95.61) == Color(0xFF4832F7));
}
```

*Make color darker or lighter*

```dart
void main() {
  // [black -> white] lighter by 100 percents
  assert(Color(0xFF000000).lighter(100) == Color(0xFFFFFFFF));
  assert(Color(0xFF000000).lx(100) == Color(0xFFFFFFFF));

  // Another lighter example
  assert(Color.fromARGB(255, 64, 64, 64).lighter(50) == Color.fromARGB(255, 192, 192, 192));
  assert(Color.fromARGB(255, 64, 64, 64).lx(50) == Color.fromARGB(255, 192, 192, 192));

  // [white -> grey] darker by 50 percents
  assert(Color(0xFF000000).darker(50) == Color(0xFF808080));
  assert(Color(0xFF000000).dx(50) == Color(0xFF808080));

  // Another darker example
  assert(Color.fromARGB(255, 192, 192, 192).darker(25) == Color.fromARGB(255, 128, 128, 128));
  assert(Color.fromARGB(255, 192, 192, 192).dx(25) == Color.fromARGB(255, 128, 128, 128));
}
```

## COLOR THEME
```dart
import 'package:app_color/app_color.dart';
import 'package:flutter/material.dart';

void main() {
  ColorTheme.init(
    data: [
      const ColorThemeData(
        name: "scaffold",
        config: ColorThemeConfig(
          light: ThemeColors(
            primary: Colors.green,
          ),
          dark: ThemeColors(
            primary: Colors.red,
          ),
        ),
      ),
    ],
  );
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      themeMode: ThemeMode.light,
      theme: ThemeData.light(),
      darkTheme: ThemeData.dark(),
      home: Scaffold(
        backgroundColor: context.themeOf("scaffold").primary,
      ),
    );
  }
}
```

## COLOR CUSTOMIZATION
```dart
import 'package:app_color/app_color.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.white,
        body: Column(
          children: [
            Expanded(
              child: Container(
                color: Colors.white,
                width: double.infinity,
                child: Center(
                  child: SizedBox(
                    width: 200,
                    height: 200,
                    child: Container(
                      color: Colors.white.dx(10),
                      alignment: Alignment.center,
                      child: const Text("DARK 10%"),
                    ),
                  ),
                ),
              ),
            ),
            Expanded(
              child: Container(
                color: Colors.black,
                width: double.infinity,
                child: Center(
                  child: SizedBox(
                    width: 200,
                    height: 200,
                    child: Container(
                      color: Colors.black.lx(10),
                      alignment: Alignment.center,
                      child: const Text(
                        "LIGHT 10%",
                        style: TextStyle(color: Colors.white),
                      ),
                    ),
                  ),
                ),
              ),
            ),
            Expanded(
              child: Row(
                children: [
                  Expanded(
                    child: Container(
                      color: Colors.green.shade400,
                      width: double.infinity,
                      child: Center(
                        child: AspectRatio(
                          aspectRatio: 1,
                          child: Container(
                            color: Colors.green.shade400.auto(10),
                            margin: const EdgeInsets.all(32),
                            alignment: Alignment.center,
                            child: Text(
                              "AUTO 10%\nDETECT ON COLOR \nBRIGHTNESS",
                              textAlign: TextAlign.center,
                              style: TextStyle(
                                color: Colors.green.shade400.auto(75, true),
                              ),
                            ),
                          ),
                        ),
                      ),
                    ),
                  ),
                  Expanded(
                    child: Container(
                      color: Colors.green.shade600,
                      width: double.infinity,
                      child: Center(
                        child: AspectRatio(
                          aspectRatio: 1,
                          child: Container(
                            color: Colors.green.shade600.auto(10),
                            margin: const EdgeInsets.all(32),
                            alignment: Alignment.center,
                            child: Text(
                              "AUTO 10%\nDETECT ON COLOR \nBRIGHTNESS",
                              textAlign: TextAlign.center,
                              style: TextStyle(
                                color: Colors.green.shade600.auto(75, true),
                              ),
                            ),
                          ),
                        ),
                      ),
                    ),
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```