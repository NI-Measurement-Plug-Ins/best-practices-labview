# Best Practices for Developing MeasurementLink Plug-Ins with LabVIEW

## Table of Contents
- [Best Practices for Developing MeasurementLink Plug-Ins with LabVIEW](#best-practices-for-developing-measurementlink-plug-ins-with-labview)
  - [Table of Contents](#table-of-contents)
  - [Getting Started With MeasurementLink](#getting-started-with-measurementlink)
  - [Design Considerations](#design-considerations)
    - [UI Interactions](#ui-interactions)
    - [UI Elements](#ui-elements)
    - [UI Style](#ui-style)
    - [TestStand](#teststand)
    - [Datatypes](#datatypes)
    - [Naming](#naming)
    - [Measurement Organization](#measurement-organization)
  - [Development Time](#development-time)
  - [Resources](#resources)

## Getting Started With MeasurementLink
If this is your first time starting with MeasurementLink, start with this training video: [Introduction to MeasurementLink](https://learn.ni.com/learning-paths/introduction-to-measurementlink)

The GitHub repo for MeasurementLink's LabVIEW API has very good step-by-step getting started documentation: [GitHub repo for MeasurementLink LabVIEW API](https://github.com/ni/measurementlink-labview)

For higher level general documentation, check out: [MeasurementLink Product Documentation](https://www.ni.com/docs/en-US/bundle/measurementlink/page/measurementlink.html)

## Design Considerations
### UI Interactions

- Does your plug-in fit the finite (i.e. press Run -> Execute -> Show Results) model that MeasurementLink plug-ins use? If not, does the Run Continuous option work? If neither of these work, you should probably take a step back and evaluate if MeasurementLink is the right fit for the user experience you are designing. Are there other ways to approach the design?
- If your plug-in takes more than 1-2 seconds to execute, consider sending intermediate updates so the user can see progress.
- What size InstrumentStudio panel are you creating? Typically, this will be a large panel, but it is an option to support small panels. The panel size is important when you start to design your LabVIEW front panel.
  
### UI Elements
- Will there be data that is only used for viewing purposes and not part of the measurement result? An example is a time domain waveform for a RMS measurement. In this case, the time domain is a wonderful visual cue for your user but is not required. 
- Will there be any elements which resize and scale with the panel? If so, using splitters is the way to isolate parts of your UI which you want to scale automatically.
- From the UI, there does not need to be a 1:1 ratio between the elements in the Measurement Configuration.ctl and what the user sees. There may be times, when it is more intuitive for the user to interact with the inputs differently than in an automation environment.
- Naming of elements in the UI is very important for MeasurementLink to work properly. The names of the UI elements must match the names in the Measurement Configuration.ctl. Give yourself some flexibility in naming in the UI by showing the element's caption instead of label.
- For numerics, use LabVIEW advanced formatting options to add unit strings where necessary. Also consider the appropriate amount of significant digits or digits of precision to show.

### UI Style 
The goal is to look like a native InstrumentStudio panel. Looks at some of the native panels like DC-Power and Scope to get an idea for the 'look and feel' users are accustomed to. For LabVIEW UI development, the recommendation is to use the Fuse Design System (or NXG style for older versions of LabVIEW) controls and indicators.

### TestStand
You measurement can be called as a step in TestStand. Make sure that when it executes, it will stop even if there are timeouts or errors. If not, your TestStand will hang potentially without any obvious signs of a problem. 

Naming is important. Check out the [Naming](#naming) section.

### Datatypes
Not every datatype is supported so it is important to keep in mind which ones are as you are developing your plug-in: 
[Supported Datatypes](https://www.ni.com/docs/en-US/bundle/measurementlink/page/supported-datatypes.html)

In general, simpler is better.

### Naming
Naming is very important within MeasurementLink. The name of the elements in the Measurement Configuration.ctl and Measurement Results.ctl must match the names used in the UI and TestStand. The UI has some flexibility since you are able to show captions instead of the labels. In TestStand, the variable names will appear unmodified. 

Some recommendations:
- Provide clear unambiguous names.
- If applicable, add units so the user does not have to guess if it is mV or V.
- Use a consistent capitalization scheme.

### Measurement Organization

## Development Time
Here are some recommendations for developing your plug-ins:
- Start with the Measurement Logic.vi. Don't worry about the Measurement Configuration.ctl or Measurement Results.ctl until you have a Measurement Logic.vi that executes the way you like it. It doesn't have to be complete but enough so that's functional before you move on.
- Add the controls you want into the Measurement Configuration.ctl.
- Start creating the Measurement UI.vi and start working on the UI aspects. Start small and iterate. Early on the key is to make sure that you are calling the Measurement Logic.vi correctly and that it works from InstrumentStudio as well.
- Add the indicators you want to the Measurement Results.ctl and update the UI as needed. 
- Continue testing and iterating on the UI design. 
- It is handy to always have the Measurement Logic.vi open when you are testing the UI so that when you run into an error you can catch it.
- When you run into an error, it is easier to just run the Measurement Logic.vi standalone and debug in LabVIEW as opposed to adding the extra step of calling it from InstrumentStudio.
- When you are feeling good about the UI, call the measurement from TestStand.
- Build you're measurement into an .exe and deploy it by copying it to the *C:\ProgramData\National Instruments\MeasurementLink\Services* directory. Test as a deployed .exe.

## Resources
- Check out the examples in this repo. 
- Browse through LabVIEW based measurements on GitHub at [MeasurementLink Plug-In repo](https://github.com/orgs/NI-MeasurementLink-Plug-Ins/repositories) for ideas and inspiration.
