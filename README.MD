# MAUI Window Bug Repro

## How to reproduce

1. Open the software and click the "Open Second Window" button.
2. Click the "Exit App" button.
3. Open the software again and you will get the exception.

## Workaround for developement only

To fix this in while developing (in the IDE, this can't be done at runtime to my knowledge):

1. Remove the following from the Platforms/MacCatalyst/Info.plist file

   ```xml
    <key>UIApplicationSceneManifest</key>
    <dict>
        <key>UIApplicationSupportsMultipleScenes</key>
        <true/>
        <key>UISceneConfigurations</key>
        <dict>
            <key>UIWindowSceneSessionRoleApplication</key>
            <array>
                <dict>
                    <key>UISceneConfigurationName</key>
                    <string>__MAUI_DEFAULT_SCENE_CONFIGURATION__</string>
                    <key>UISceneDelegateClassName</key>
                    <string>SceneDelegate</string>
                </dict>
            </array>
        </dict>
    </dict>
   ```

2. Rebuild the software and debug it (a window won't open)
3. Stop debugging
4. Add those lines back to the Info.plist file.
5. Rebuild
6. Debug again (the software should open again)