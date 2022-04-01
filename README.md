# Nim-AppImage-Template
A template for creating _Nim_ applications that will get converted to an AppImage.

## Structure
- `myapp.AppDir`: Here goes all the AppImage data.
  - `AppRun`: The file that _Nim_ outputs after compiling.
  - `.DirIcon`: PNG icon. Should be in one of the standard image sizes, e.g., 128x128 or 256x256 pixels.
  - `myapp.desktop`: Destkop file describing the payload application.
  - `myapp.svg`: Application’s icon in the best available quality.
- `src`: Application source.
  - `myapp.nim`: Main module.
- `LICENSE`: Application's license (see https://choosealicense.com).
- `myapp.nimble`: Configuration file to define the [dependencies and more](https://github.com/nim-lang/nimble#creating-packages) of the _nimble_ package.
- `README.md`: Description of the application.

## Desktop File
The file allocated at `myapp.AppDir/myapp.desktop` requires to define the following entries:
- `Type`: _Application_, _Link_ or _Directory_.
- `Name`: Application's name.
- `Categories`: A list of categories for your application separated by a semi-colon.  
  ([List of the valid categories](https://specifications.freedesktop.org/menu-spec/latest/apa.html))
- `Icon`: Application's icon filename, without the extension.  
- `Èxec`: A command line consisting on an executable program.

Optional entries:
- `X-AppImage-Name`: Application's name. Used to relate two AppImages of the same application but different versions.
- `X-AppImage-Version`: Application's version (e.g., `1.0.0-beta-2` or `2019.1.1`).
- `X-AppImage-Arch`: Application's architecture (e.g., `x86_64` or `i386`).

([More desktop entry keys](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#recognized-keys)).

By default `myapp.desktop` file looks like:
```ini
[Desktop Entry]
Type=Application
Name=My App
Categories=Utility;
Icon=myapp
Exec=AppRun

X-AppImage-Version=0.1.0
X-AppImage-Arch=x86_64
```

## Deploy
To generate the actual AppImage we will use [_appimagetool_](https://appimage.github.io/appimagetool/). So you may want to download it.  
But before generating it we must compile our application as following:
```sh
nim c --outdir:myapp.AppDir --out:myapp.AppDir/AppRun src/myapp.nim # Or cpp
```
Now we just need to use [appimagetool](https://appimage.github.io/appimagetool/) to generate the AppImage.
```
appimagetool myapp.AppDir/
```
This will output a new AppImage with the name of `My_App-x86_64.AppImage`.

## More
- [AppImage website](https://appimage.org).
- [AppImage docs](https://docs.appimage.org/index.html).
- [AppImage packaging guide](https://docs.appimage.org/packaging-guide/index.html).
- Discord: _Patitotective#0127_.
- Email: cristobalriaga@gmail.com.
- Twitter: [@patitotective](https://twitter.com/patitotective).
