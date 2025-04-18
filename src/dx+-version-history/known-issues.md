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

**Last Updated:** April 16, 2025

## List of Known Issues for version 2025.15

### Documentation Issues
- **Documentation may not contain up-to-date screenshots** - and some buttons, features, and text may have changed or been removed

### Viewer Issues
- **Y2 Axis Display Problem** - Y2 axis doesn't appear in plot options and changing values in ribbon doesn't work
- **HDF5 Format Limitations** - DX+ Viewer can only play back a limited number of plots at a time from APEX-H5 files before significant slowdown
  - Apex still recommends SQLite format for performance reasons and direct compatibility with file viewing and post processing
- **Campbell Plot Display Delay** - Delay in Campbell plot displaying graph in DX+ Offline/Viewer through SQLite file - plots may need to be maximized to update
- **Time/History Plot Duration Issues** - SQLite Data Store (DX+ Viewer) - Time/History Plots durations run past their length
- **Grid Clipping on Window Resize** - Viewer grids become clipped when window resized too small
- **Text Scaling Issues** - Text on Graphic Plots (Text, Thermometer, LED) does not always scale correctly
- **Clear Button Functionality** - Clear button does not clear cursors
- **Plot Export Problems** - Copied/exported plots may not display axes, z-axis legend, or white axis labels
- **Zoom Reset Issues** - Zoom Reset with Mouse MiddleButton doesn't always reset the trace
- **Marker Clearing Issues** - Unable to Clear Markers from Zmod Plot
- **Plot Deletion Problems** - Remove merge/remove space action can lead to undeletable plots
- **Peak Display Inconsistency** - Peaks can disappear forever when threshold goes too high (Campbell, Zmod)
- **Z-Axis Range UI Problem** - Zmod & Campbell Z-Axis Range arrows can sometimes disappear
- **Graphic Plot Title Overlay** - Graphic Plots' titles are overlaid on whatever titles are below them when expanded, sometimes making them hard to read
- **Plot Space Selection Issue** - 1 Trace Per option not available for multi-space selection unless all spaces selected
- **Missing Bar Charts from Peaks** - DX+ Bar Charts created from Peaks do not show up
- **Channel Tree Organization** - Unselected channels in the Viewer element still appear in Viewer tree
- **Transmit/Receive  Organization** - Propagated channels do not remain organized by processing type in Viewer tree
- **LED Graphic Plot Orientation** - Orientation setting in dialog shows "Horizontal" when saved setting is "Vertical" - making changes to other LED settings will require user to re-select "Vertical" if that is the desired orientation
- **Analog Trigger Tach causing plotting hangup on Campbell** - issue is present after RPM reaches Max Speed. Issue is not present when using Digital Trigger setting in Tach element

### Core Functionality Issues
- **Included Streams Propagation** - "Included Streams" do not propagate to Statistics or Octave elements
- **Designer-Viewer Transition** - DX+ must be restarted when unable to return to viewer to stop DAQ under certain circumstances
- **MeCalc Performance** - MeCalc device takes a very long time to save, load, and process
- **Setup Badge Visibility** - Pull Setup badges not shown until clicked, no errors given on Submit
- **Help File Persistence** - Output elements' Help files persist in side panel when Design elements are clicked
- **Limit Alert Display** - New graphic plots not showing over-limit alerts (red color) until design is resubmitted
- **Octave Band Issues** - Octave bands responding may be off by a factor of 10 - standard in use needs to be documented
- **Notes Badge Display** - Notes Badge still shows when note information gets cleared
- **Strip Chart Behavior** - Strip Chart Y-axis label and trace change to match History plot on design resubmission

### Data Processing Issues
- **FFT Limit Application** - Issues can occur with limit application to FFT when limit range starts at 0
- **Filter Selection Problems** - Order Filter has issues with selecting filter for RPM input
- **Filter Output Quality** - Order Filter can have output discontinuities
- **Unit Propagation** - EU Scalar Units not propagated downstream

### Technical Issues
- **FFT Implementation** - FFT Zoom and FFT Overlap do not currently match DX and DS in methodology
- **PTP Time Sync** - Address case of PTP with no Master: MeCalc showing 1970

## Reporting Issues
* Please report any new issues to Apex @ [https://users.apexturbine.com/](https://users.apexturbine.com/)
* Regular updates will be provided as issues are resolved.
