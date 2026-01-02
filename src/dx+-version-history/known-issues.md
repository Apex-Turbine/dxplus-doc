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

**Last Updated:** January 1, 2025
## List of Known Issues for version 2025.52.13

### Documentation Issues
- **Documentation may not contain up-to-date screenshots** - and some buttons, features, and text may have changed or been removed

### Plot Issues
- **User Interaction pauses other Tests** - When running tests alongside the Campbell Plot, interacting with the plot can cause other tests to pause briefly before resuming.
- **Campbell Plot memory usage** - If DAQ is started with Campbell Plots present but no rig running, memory usage continuously increases as data is buffered. Starting the rig or removing Campbell Plots resolves the issue.
- **Plots background turns gray when loading plot setup file** - Loading a plot setup file for Campbell (and sometimes scatter plots) can cause the background to turn gray. This may also occur when resubmitting a design.
- **Trace order issues in plot options** - Reordering traces in the plot options traces tab may not work as expected, especially with multiple graphic text displays.
- **Graphic plot PDF export issues** - Exported PDFs of Text and Gauge graphic plots may have unreadable text due to white backgrounds, and plot spaces may turn gray when exporting.
- **Plots durations run past their length** - The time and history plots in the SQLite Data Store (DX+ Viewer) start at the beginning of play, but the duration continues after the data display ends.

### Viewer Issues
- **HDF5 playback limited plots** - DX+ Viewer release can only play back limited plots at a time from HDF5 files (limit may vary by machine).
  - Apex still recommends SQLite format for performance reasons and direct compatibility with file viewing and post processing
- **Disabled element in HDF5 Output causes errors on write** - Input or processor elements that are unselected in HDF5 output can cause write errors for HDF5 files.
- **Background image options delayed from Ribbon** - When selecting background image options from the ribbon, the change does not take effect until a mouse move or click.
- **Viewer streams duplicated** - Opening the same design multiple times in the Viewer can result in duplicate data streams being displayed.
- **Design marked as modified when opened** - Opening a design may immediately mark it as modified, even if no changes have been made.
- **Clear All Pages button** - In the DX+ File Viewer, the "Clear All Pages" button remains disabled until a second page is created.
- **Idle CPU usage with dynamic update** - Creating plots before starting DAQ can cause DX+ to use 5-10% CPU due to dynamic updates. Starting and stopping DAQ resolves the issue.
- **Time-sync button** - When switching from DAQ to Offline Mode by loading an offline design, the time-sync button in the Viewer may not enabled.
- **Multiple error dialogs** - Opening an old design with element creation errors shows a separate error dialog for each issue.
- **Drag-and-drop stops working** - When the plot selector dialog is open in DX+, drag-and-drop operations may stop working until the dialog is closed.
- **Graphic plot PDF export issues** - Exported PDFs of Text and Gauge graphic plots may have unreadable text due to white backgrounds, and plot spaces may turn gray when exporting.
- **Incorrect 'Reference Domain' setting does not error and prevents Viewer tree display** - If an incorrect 'Reference Domain' is set (e.g., Pressure instead of Time), no error is shown and the Viewer tree is not produced. Correcting the setting allows the design to load as expected.
- **"Reading File" progress window** - When an incorrect file type or an SQLite file with no streams is selected, the "Reading File" progress window may remain open after the "No streams found in the selected file" dialog is closed.
- **Expanding some plots causes overlap** - Expanding certain graphic plots can result in them overlapping other plots in the Viewer.

### Model Issues
- **Zone Visibility Issue in SDR Models** – Deselecting Zones does not hide the corresponding Zone as expected.
- **Loading bars do not appear for model loading** - When loading models, progress/loading bars are not displayed.
- **Model does not load with previously active solution** - When opening a saved model, the solution that was active at the time of saving is not automatically loaded.
- **SDRs do not properly interpolate color contours between vertices** - Some SDR models, especially those using quadratic or nonlinear cells, may not interpolate color contours correctly between vertices, resulting in incorrect coloring of intermediate points.

### Video Issues
- **Multiple webcam instances not supported** - DX+ cannot handle multiple instances of the same webcam. Limiting to one device should resolve the issue.
- **Video always opens too small with Absolute Layout enabled** - When Absolute Layout is enabled, video opens at a smaller size than expected.
- **Crash when deleting plots before resources finish loading** - Deleting a video plot before its resources (such as webcam drivers) have finished loading can cause a crash due to race conditions and dangling references.

### Technical Issues
- **DX+ launch lag** - On new installations, DX+ may take several seconds or minutes to launch. The splash screen does not appear until after loading procedures are complete.
- **DAQ tab displayed in Offline Mode for old designs** - Opening a design intended for Online mode while in Offline mode may incorrectly display the DAQ tab, even though only processing of Input elements should be available.


## List of Known Issues for version 2025.15

### Viewer Issues
- **Y2 Axis Display Problem** - Y2 axis doesn't appear in plot options and changing values in ribbon doesn't work
- **Campbell Plot Display Delay** - Delay in Campbell plot displaying graph in DX+ Offline/Viewer through SQLite file - plots may need to be maximized to update
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
