# Neofetch GUI

A modern, dark-themed GTK4 wrapper for Neofetch with terminal emulation.

## Installation

This application is distributed as a Flatpak bundle. 

### 1. Install Dependencies
Before installing the app, you need to ensure the GNOME 47 runtime is installed on your system. Run the following command:

```bash
flatpak install flathub org.gnome.Platform//47
```

### 2. Install the App
1. Go to the **[Releases](../../releases)** tab on this GitHub page.
2. Download the latest `neofetch-gui.flatpak` file.
3. Open your terminal in the download folder and run:

```bash
flatpak install --user neofetch-gui.flatpak
```

## Usage

You can launch the app directly from your system's application menu, or via terminal:

```bash
flatpak run org.tiwut.NeofetchGui
```
