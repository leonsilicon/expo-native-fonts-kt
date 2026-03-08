# expo-native-fonts

> Load fonts on iOS and Android using native code.

Traditionally, loading fonts in an Expo project requires using the `expo-fonts` library. While this has historically been a great solution, it has to load the fonts at runtime which necessitates you to show the splash screen.

With `expo-native-fonts`, font files are loaded via native code. What does that mean?

**Fonts will be available immediately at runtime.**

> No more long splash screens!

**You can change the font family, weight, and style individually.**

> No more `fontFamily: 'Raleway-BoldItalic'`!

## Installation

1. Install the package:

   ```bash
   bun add expo-native-fonts-kt
   ```

2. Add your font files to a directory (we recommend `assets/fonts`):

   ```bash
   app/
   assets/
   |- fonts/
      |- Raleway-Black.ttf
      |- Raleway-BlackItalic.ttf
      |- ...
   ```

3. Add the plugin to your `app.json` config:

   ```js
   {
     "expo": {
       "plugins": [
         [
           "expo-native-fonts-kt",
           {
             "Raleway": [
               {
                 "path": "./assets/fonts/Raleway-Black.ttf",
                 "weight": 900
               },
               {
                 "path": "./assets/fonts/Raleway-BlackItalic.ttf",
                 "weight": 900,
                 "style": "italic"
               }
               // ...
             ]
           }
         ]
       ]
     }
   }
   ```

4. Rebuild your app as described in the ["Adding custom native code"](https://docs.expo.io/workflow/customizing/) guide

5. Start using the newly-defined font in your style objects:

   ```tsx
   const styles = StyleSheet.create({
     text: {
       fontFamily: "Raleway",
       fontWeight: "900",
       fontStyle: "italic",
     },
   });
   ```

## Gotchas

### Supported Font Files

This plugin has only been tested with `.ttf` and `.otf` files.

The use of other file types may not work!

### Font Family Name

The key you use to define a family in the plugin config **must exactly match** the actual font family name defined in the font files.

To find the family name:

1. Install the `lcdf-typetools` package:

   ```bash
   brew install lcdf-typetools
   ```

2. Run the following on one of the font files:

   ```bash
   otfinfo --family Raleway-Regular.ttf
   ```

3. The printed value is the family name to use.

   For example, if the command printed `Matter`, you should format your config like so:

   ```js
   {
     "expo": {
       "plugins": [
         [
           "expo-native-fonts-kt",
           {
             "Matter": [
               // ...
             ]
           }
         ]
       ]
     }
   }
   ```

## Contributing

Check out our [Contributing](.github/CONTRIBUTING.md) guide for more information on reporting issues, submitting feedback, or contributing code.

### Setup

To set up the repository locally on your machine, follow these steps:

1. Install the project dependencies:

   ```bash
   yarn
   ```

2. Create a new build:

   ```bash
   yarn build
   ```

## Credits

Original creator [@joshpensky]
Major props to [@jsamr](https://github.com/jsamr) for their documentation on supporting fonts natively: https://github.com/jsamr/react-native-font-demo
