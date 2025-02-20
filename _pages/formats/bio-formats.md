---
section: Learn:ImageJ Basics:File Formats
categories: [Import-Export,SciJava,OME]
doi: 10.1083/jcb.201004104
icon: /media/icons/bio-formats.png
artifact: ome:bio-formats_plugins
---

## Purpose

Import data from many life sciences file formats, and export to several open formats.

## History

See [LOCI's Bio-Formats site](https://loci.wisc.edu/software/bio-formats) for a historical narrative of the project.

## Documentation

What follows is a brief overview of the available plugins. You will find them all under the "Bio-Formats" submenu of Plugins. See the [Bio-Formats website](https://www.openmicroscopy.org/bio-formats/) for additional information about Bio-Formats in general.

See especially the [Using Bio-Formats](https://docs.openmicroscopy.org/latest/bio-formats/users/imagej/load-images.html#using-bio-formats-to-load-images-into-imagej) page for detailed instructions.

### Bio-Formats Importer

The **Bio-Formats Importer** is a plugin for reading data into Fiji. It can open many dozens of proprietary life sciences formats, and standardize their acquisition metadata into a common [OME data model](https://docs.openmicroscopy.org/latest/ome-model/developers/model-overview.html). It will also extract and set basic metadata values such as [spatial calibration](/imaging/spatial-calibration) if they are available in the file.

Often, you will not need to worry about this plugin to import your data, because Bio-Formats is largely integrated with the {% include bc path="File|Open" %} command of Fiji. However, for certain file formats, you may wish to explicitly activate the Bio-Formats Importer to override the default behavior of Fiji. For example, by default Fiji uses some built-in logic to open TIFF files, but this logic may fail with certain TIFFs. The Bio-Formats Importer plugin may be able to import such TIFFs successfully.

### Bio-Formats Exporter

The **Bio-Formats Exporter** is a plugin for exporting data to disk.

It can save to the open [OME-TIFF](https://docs.openmicroscopy.org/latest/ome-model/#ome-tiff) file format, as well as several movie formats (e.g., QuickTime, AVI) and graphics formats (e.g., PNG, JPEG).

-   Animated PNG (\*.png)
-   {% include wikipedia title="Audio Video Interleave" %} (\*.avi)
-   [CellH5](https://github.com/CellH5/cellh5) File Format (\*.ch5)
-   Encausupated PostScript (\*.eps, \*.epsi)
-   {% include wikipedia title="Image Cytometry Standard" %} (\*.ids, \*.ics)
-   Java source code (\*.java)
-   JPEG (\*.jpg, \*.jpeg, \*.jpe)
-   JPEG-2000 (\*.jp2)
-   [OME-TIFF](https://docs.openmicroscopy.org/latest/ome-model/ome-tiff/) (\*.ome.tif, \*.ome.tiff, \*.ome.tf2, \*.ome.tf8, \*.ome.btf)
-   [OME-XML](https://docs.openmicroscopy.org/latest/ome-model/ome-xml/) (\*.ome, \*.ome.xml)
-   QuickTime (\*.mov)
-   Tagged Image File Format (TIFF) (\*.tif, \*.tiff, \*.tf2, \*.tf8, \*.btf)
-   [Vaa3d](https://github.com/Vaa3D/Vaa3D_Wiki/wiki/Vaa3D-Wiki) (\*.v3draw)
-   [Woolz](https://www.emouseatlas.org/emap/analysis_tools_resources/software/woolz.html) (\*.wlz)

{% include notice icon="note" content="For OME-TIFF and TIFF formats, the file extensions `*.tif` and `*.tiff` are associated with the standard 32-bit TIFF, which has a 4GB size limit. On the other hand, the file extensions `*.tf2`, `*.tf8`, and `*.btf` are automatically associated with [the 64-bit BigTIFF format](https://www.awaresystems.be/imaging/tiff/bigtiff.html), which can store much bigger data." %}

### Bio-Formats Remote Importer

The **Bio-Formats Remote Importer** is a plugin for importing data from a remote URL.

It is likely to be less robust than working with files on disk, so when possible we recommend downloading your data to disk and using the regular Bio-Formats Importer instead.

### Bio-Formats Windowless Importer

The **Bio-Formats Windowless Importer** is a version of the **Bio-Formats Importer** plugin that runs with the last used settings to avoid popping up any additional dialogs beyond the file chooser. If you find that you always use the same import settings, you may wish to use the windowless importer to save time.

### Bio-Formats Macro Extensions

The Bio-Formats plugins come with a set of macro extensions to enable additional functionality from macros. The **Bio-Formats Macro Extensions** plugin prints out the available commands to the ImageJ log window, along with instructions for using them.

### Stack Slicer

The **Stack Slicer** plugin is a helper plugin used by the **Bio-Formats Importer**. It can also be used standalone to split a stack across channels, focal planes or time points.

### Bio-Formats Plugins Configuration

The **Bio-Formats Plugins Configuration** dialog is a useful way to configure the behavior of each file format. You can see a list of supported file formats on the Formats tab, toggle each format on or off (which is useful, for example, if your file is being detected as the wrong format), and toggle whether each format bypasses the importer options dialog using the "Windowless" checkbox. You can also configure any specific options for each format—for example, for QuickTime, you can toggle between Apple's QTJava library or Bio-Formats's built-in support.

In addition, you can see a list of available helper libraries used by Bio-Formats on the Libraries tab.

### Bio-Formats Plugins Shortcut Window

The **Bio-Formats Plugins Shortcut Window** is a small window with a quick-launch button for each plugin. You can also drag and drop files onto the shortcut window to open them quickly using the **Bio-Formats Importer** plugin.

### Update Bio-Formats Plugins

The **Update Bio-Formats Plugins** command will check online for updates to the Bio-Formats Plugins. In the case of Fiji, we recommend that you do not use this method of update, but instead use the [ImageJ Updater](/plugins/updater).

## Calling Bio-Formats from the command line

You can invoke Bio-Formats from the command line using the [ImageJ Launcher](/learn/launcher):

1.  Use the [Macro Recorder](/scripting/macro#the-recorder) to record the line of macro code that runs Bio-Formats that way you want.
2.  Click "Create" to pop up the [Script Editor](/scripting/script-editor), edit as desired, then save the macro as a `.ijm` macro file.
3.  Run the macro from the command line; e.g.:

```bash
ImageJ-win32.exe -macro myMacro.ijm -batch
```

Leave off the `-batch` flag if you want ImageJ to remain open afterward.

Note that you cannot use the [--headless option](/learn/headless#running-macros-in-headless-mode) because Bio-Formats does not work in headless mode, even when running as a macro. (You will see `VerifyError` on the console if you try.)

Here is an example macro created in such a fashion:
```java
run("Bio-Formats Importer", "open=/Users/jdoe/data.ome.tif " +
  "autoscale color_mode=Default view=Hyperstack stack_order=XYCZT");
saveAs("Tiff", "/Users/jdoe/Desktop/result.tif");
```

## Scripting

Bio-Formats has a high-level scripting interface, accessible by Java and all scripting languages supported by Fiji (but not the ImageJ macro language). Java example:
```java
String id = "/path/to/myFile.ext";
ImagePlus[] imps = BF.openImagePlus(id);
```

If needed, import options can be set:
```java
String id = "/path/to/myFile.ext";
ImporterOptions options = new ImporterOptions();
options.setId(id);
options.setAutoscale(true);
options.setCrop(true);
options.setCropRegion(0, new Region(x, y, w, h));
options.setColorMode(ImporterOptions.COLOR_MODE_COMPOSITE);
//...etc.
ImagePlus[] imps = BF.openImagePlus(options);
```

## Daily builds

{% include notice icon="warning" content='The daily builds are **not yet released** and should be considered **beta** in quality. There may be new bugs. In particular, you should **avoid exporting data using the Bio-Formats Exporter** because the files it writes might not be readable later by release versions of Bio-Formats or other OME-compliant tools.' %}

Fiji ships release versions of Bio-Formats. However, given the long time frame between releases, you can update to the latest code by toggling the **Bio-Formats** update site, which includes the latest bug-fixes.

When reporting a bug, the developers may ask you to test with the **Bio-Formats** update site enabled.

To enable the Bio-Formats update site:

1.  Launch the updater: **Update** from the **Help** menu.
2.  Click the **Manage update sites** button.
3.  Tick the **Bio-Formats** box: <img src="/media/formats/bf-manage-update-sites.png" title="fig:Bf-manage-update-sites.png" width="700" alt="Bf-manage-update-sites.png" />
4.  Click the **Close** button. The updater should want to update some files now: <img src="/media/formats/bf-jars-to-update.png" title="fig:Bf-jars-to-update.png" width="700" alt="Bf-jars-to-update.png" />
5.  Click the **Apply changes** button.
6.  Restart Fiji when prompted.
7.  To verify the upgrade, choose **Bio-Formats Plugins...** from **About Plugins** beneath the **Help** menu: <img src="/media/formats/bf-about-plugins.png" title="fig:Bf-about-plugins.png" width="700" alt="Bf-about-plugins.png" />

## Source code

The Bio-Formats source code is {% include github org='openmicroscopy' repo='bioformats' %}.

## Reporting bugs

To report a bug in Bio-Formats, please see [reporting a bug in Bio-Formats](https://docs.openmicroscopy.org/latest/bio-formats/about/bug-reporting.html).

## Publication

{% include citation %}

   
