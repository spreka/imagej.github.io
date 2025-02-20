---
mediawiki: Slice_Labeler
title: Slice Labeler
categories: [Image Annotation]
---

{% include info-box software='ImageJ' name='Slice Labeler' author='Pedro Ramos-Cabrer' filename=' [Slice\_Labeler.class](https://imagej.nih.gov/ij/plugins/download/Slice_Labeler.class)' source=' [Slice\_Labeler.java](https://imagej.nih.gov/ij/plugins/download/Slice_Labeler.java)' released='13 May 2004' latest-version='' status='stable' category='Image annotation' website=' [Slice Labeler](https://imagej.nih.gov/ij/plugins/slice-labeler.html)' %} This plugin is superceeded by the [Series Labeler](/plugins/series-labeler)

*Copy from the website:*

This plugin adds a label in the top-left corner of each slice of a stack or to the location of any rectangular selection. The labels are drawn in the current foreground color. A dialog box allows the user to specify font size for the labels, text for the body of the labels, a starting point for a counter, the interval between frames of the counter, and the number of digits used by the counter. The counter will be added after the body text to identify slices or set the number of digits to zero and no counter will be displayed.

For Example, if we have a stack with 30 slices of MRI sections of a rat brain, running the plugin and introducing "Rat203-" as text, "1" as starting value, "1" as increment between slices and "2" as the number of digits, slices of the stack will be labeled as follows: "Rat203-01", "Rat203-02", "Rat203-03"..."Rat203-30".

 
