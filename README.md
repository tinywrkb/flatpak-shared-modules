# flatpak-shared-modules

Here you can find common Flatpak modules that I've been using in the packaging of different Flatpak apps in my [flatpaks](https://github.com/tinywrkb/flatpaks) repo.

These modules are only updated when the relevant application is updated, and most applications I update only when there's  
a new runtime release, so don't be surprised if a module is outdated.  
If I don't have a use for a module, then it's very possible that it will be removed.  
Due to the above, I suggest copying a module into your Flatpak packaging, instead of adding this repo as a git submodule.

Please note that `x-checker-data` properties are included in most modules for easily updating them with [flatpak-external-data-checker](https://github.com/flathub/flatpak-external-data-checker/).
