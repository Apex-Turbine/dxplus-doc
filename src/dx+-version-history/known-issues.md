---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Known Issues

<div align="left">

<figure><img src="../.gitbook/assets/DX+_blue@300x.png" alt="" width="188"><figcaption></figcaption></figure>

</div>

**Last Updated:** October 31, 2024

### List of Known Issues

## Documentation Issues
- **Documentation may not contain up-to-date screenshots** - and some buttons, features, and text may have changed or been removed

## Viewer Issues
- **Y2 Axis Display Problem** - Y2 axis doesn't appear in plot options and changing values in ribbon doesn't work
- **HDF5 Playback Limitations** - DX+Viewer release can only play back 6 plots at a time from HDF5 file
- **Campbell Plot Display Delay** - Delay in Campbell plot displaying graph in DX+ Offline/Viewer through SQLite file
- **Time/History Plot Duration Issues** - SQLite Data Store (DX+ Viewer) - Time/History Plots durations run past their length
- **Grid Clipping on Window Resize** - Viewer grids become clipped when window resized too small
- **Text Scaling Issues** - Text on Graphic Plots (Text, Thermometer, LED) does not scale correctly
- **Clear Button Functionality** - Clear button does not clear cursors
- **Plot Export Problems** - Copied/exported plots do not display axes, z-axis legend, or white axis labels
- **Zoom Reset Issues** - Zoom Reset with Mouse MiddleButton doesn't always reset the trace
- **Marker Clearing Issues** - Unable to Clear Markers from Zmod Plot
- **Plot Deletion Problems** - Remove merge/remove space leads to undeletable plots
- **Peak Display Inconsistency** - Peaks disappear forever (sometimes) when threshold goes too high (campbell, zmod)
- **Z-Axis Range UI Problem** - Zmod & Campbell Z-Axis Range arrows disappear
- **Graphic Plot Title Overlay** - Graphic Plots' titles overlaid on whatever titles are below them when expanded
- **Stream Selection Issue** - 1 Trace Per option not available for multi-space selection unless all spaces selected
- **Missing Bar Charts from Peaks** - DX+ Bar Charts created from Peaks do not show up
- **Channel Tree Organization** - Unselected channels in the viewer element still appear in plotting tree

## Core Functionality Issues
- **Included Streams Propagation** - "Included Streams" do not propagate to Statistics or Octave
- **Designer-Viewer Transition** - DX+ must be restarted when unable to return to viewer to stop DAQ
- **MeCalc Performance** - MeCalc device takes a very long time to save, load, and process
- **Setup Badge Visibility** - Pull Setup badges not shown until clicked, no errors given on Submit
- **Help File Persistence** - Output elements' Help files persist in side panel when Design elements are clicked
- **Limit Alert Display** - New graphic plots not showing over-limit alerts (red color) until reprocess
- **Octave Band Issues** - Octave bands responding seem off by a factor of 10
- **Notes Badge Display** - Notes Badge still shows when note information gets cleared
- **Strip Chart Behavior** - Strip Chart Y-axis label and trace change to match History plot on resubmit

## Data Processing Issues
- **FFT Limit Application** - Issues with limit application to FFT when limit range starts at 0
- **Peaks Data Issue** - DX+ Peaks element produces no graphable data
- **Filter Selection Problems** - Order Filter has issues with selecting filter for RPM input
- **Filter Output Quality** - Order Filter has output discontinuities
- **Unit Propagation** - EU Scalar Units not propagated downstream

## Technical Issues
- **Debug Artifacts** - Release package contains debug Qt plugins
- **FFT Implementation** - FFT Zoom and FFT Overlap do not match DX and DS in methodology
- **Publisher/Subscriber Organization** - Propagated channels do not remain organized by processing type
- **PTP Time Sync** - Address case of PTP with no Master: MeCalc showing 1970

### Notes

* Please report any new issues to Apex @ [https://users.apexturbine.com/](https://users.apexturbine.com/)
* Regular updates will be provided as issues are resolved.
