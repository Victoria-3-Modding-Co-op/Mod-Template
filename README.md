# Overview
This is a template to create a new repository for a Victoria 3 mod.

# Content
- [Setup](#setup)
  - [Creating your own Repository](#creating-your-own-repository)
  - [Checkout your new Repository](#checkout-your-new-repository)
  - [Adjusting Mod Metadata](#adjusting-mod-metadata)
  - [Open the Launcher](#open-the-launcher)
  - [Final Adjustments](#final-adjustments)
- [Folder Structure](#folder-structure)
- [Further Resources](#further-resources)

# Setup

## Creating your own Repository

To set up a new repository using this template,
click on the "Use this Template" button on GitHub:
![button-example](documentation/template-guide.png)

## Checkout your new Repository

It is recommended to not check out the repository into the games mod folder.
If you are new to git and GitHub please read up on how to do this.

## Adjusting Mod Metadata

You can set up your mod's metadata in one of two ways:

**Manual approach:**
Edit the [mod/.metadata/metadata.json](mod/.metadata/metadata.json) file directly. The important things to change are:
- name
- id
- short_description

> ⚠️ **Important:** If you choose the manual approach, you must also delete or manually adjust the following files:
> - `mod/events/ABBREVIATION_PLACEHOLDER_events.txt`
> - `mod/common/on_action/ABBREVIATION_PLACEHOLDER_on_actions.txt`

**Automated via GitHub Action:**

You can automatically initialize your mod's metadata and abbreviation using the included GitHub Actions workflow.  
This workflow not only sets up your abbreviation, but also:

- Generates a unique global variable (e.g., `on_mod_loaded_<your_abbreviation>`) to improve compatibility with other mods.
- Suppresses errors related to this variable, so you won't see unnecessary warnings during development, since you typically won't use it directly within your own mod.

This automation streamlines setup and helps avoid common issues.

**To use the workflow:**

1. **Enable write permissions for the workflow in the repository settings**
  - Go to your repository's **Settings**.
  - Under **Actions > General**, locate **Workflow permissions**.
  - Select **Read and write permissions** and click **Save**.

2. **Run the `Initialize Mod Template` workflow**
  - Open the **Actions** tab in your repository.
  - Select the **`Initialize Mod Template`** workflow.
  - Start the workflow and enter your desired abbreviation or prefix. Fill in any optional fields as needed.
  - When the workflow finishes, check [mod/events/abbreviation_event.txt](mod/events/abbreviation_event.txt):
    - The first line should now use your abbreviation instead of `ABBREVIATION_PLACEHOLDER_error_suppression`.

For a visual guide to the workflow options, see the screenshot in `documentation/workflow.png`.

Using this workflow ensures your mod's abbreviation is set up correctly and your files are ready for development.

## Adding your Mod to the Game

To add the mod to the game/launcher we need to link it in the games mod folder.

### Windows

This can best be done via a folder junction. To create a new junction, we can use this command:
```
mklink /j "X:\path\to\Documents\Paradox Interactive\Victoria 3\mod\your-mod-folder" "X:\path\to\the\mod\directory\in\the\repo"
```
Important is that we point not to the repository but to the [mod](mod) subfolder.

The command can be run by either opening a Terminal or by pressing Win + R and putting the adjusted command into the run window.

**NOTE:** You need to replace the paths with the corresponding ones for your installation

### Linux

```
ln -s "~/path/to/mod/directory/in/the/repo" "~/.local/share/Paradox Interactive/Victoria 3/mod/your-mod-folder"
```

## Open the Launcher

In the Paradox Launcher, your mod should now show up and can be added to a playset as normal.

## Final Adjustments

It is recommended to replace the thumbnails before releasing your mod to steam.

There are two thumbnails for Victoria 3 mods:
- [Steam Workshop Thumbnail](mod/thumbnail.png)
- [Paradox Launcher Thumbnail](mod/.metadata/thumbnail.png)

# Folder Structure

This Repository is designed so you do not release your documentation or git folders to steam.

The [documentation](documentation) folder is meant for documentation
you may have for your mod like Markdown files or other types of documents.

The [image](image) folder is meant for reference images like original size images
that you used to create game images or templates for game images.
Included in this repository are:
- Template images for game logos of different types
- GIMP files to easily create Production Method and Building icons

The [mod](mod) folder contains the mod itself and is where you generally work in.

Finally, the [script](script) folder is meant for bash or batch scripts that you
developed for automating tasks for your mod.
This repository contains a script to copy your localization files from one language
to another.
That is helpful if you develop your mod in a base language like english and still want
your players to be able to use the mod in other languages.

# Further Resources

## Victoria 3 Wiki

The Victoria 3 Wiki can be outdated at times when it comes to modding,
but it is still a great resource and starting point for new modders.

https://vic3.paradoxwikis.com/Modding

## Victoria 3 Modding Coop

The Victoria 3 Modding Coop is a community maintained Discord server
that is quite active and can answer a lot of potential questions about
how to do specific things.

https://discord.com/invite/uUbuMTQjA7
