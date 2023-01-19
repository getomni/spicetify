### [Spicetify v2](https://github.com/khanhas/spicetify-cli)

#### Linux and MacOS:

In **Bash**:

```bash
cd "$(dirname "$(spicetify -c)")/Themes"
git clone https://github.com/getomni/spicetify.git omni
cd omni
cp omni.js ~/.config/spicetify/Extensions
spicetify config extensions omni.js
spicetify config current_theme omni color_scheme base
spicetify config inject_css 1 replace_colors 1 overwrite_assets 1
spicetify apply
```

#### Windows

In **Powershell**:

```powershell
cd "$(spicetify -c | Split-Path)\Themes"
git clone https://github.com/getomni/spicetify.git omni
cd omni
Copy-Item omni.js %appdata%\spicetify\Extensions\
spicetify config extensions omni.js
spicetify config current_theme omni color_scheme base
spicetify config inject_css 1 replace_colors 1 overwrite_assets 1
spicetify apply
```

From Spotify > v1.1.62, in sidebar, they use an adaptive render mechanic to actively show and hide items on scroll. It helps reducing number of items to render, hence there is significant performance boost if you have a large playlists collection. But the drawbacks is that item height is hard-coded, it messes up user interaction when we explicity change, in CSS, playlist item height bigger than original value. So you need to add these 2 lines in Patch section in config file:

```ini
[Patch]
xpui.js_find_8008 = ,(\w+=)32,
xpui.js_repl_8008 = ,${1}56,
```

#### Hide Window Controls

Windows user, please edit your Spotify shortcut and add flag `--transparent-window-controls` after the Spotify.exe:
![instruction1](./windows-shortcut-instruction.png)

Alternatively, you can use `SpotifyNoControl.exe`, included in this theme package, to completely remove all windows controls and title menu (three dot at top left corner). Title menu still can be access via Alt key. Closing, minimizing can be done via right click menu at top window region.
`SpotifyNoControl.exe` could be used as Spotify launcher, it opens Spotify and hides controls right after. So you should make a shortcut for it, change icon and add to desktop or start menu.
Moreover, by default, Spotify adjusted sidebar items and profile menu icon to stay out of Windows native controls region. If you decided to use `SpotifyNoControl.exe` from now on, please open `user.css` file and change variable `--os-windows-icon-dodge` value to 0 as instruction to snap icons back to their original position.

![nocontrol](https://i.imgur.com/qdZyv1t.png)

#### How to uninstall

Remove the omni script with the following commands

```
spicetify config extensions omni.js-
spicetify apply
```
