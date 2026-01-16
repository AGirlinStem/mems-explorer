# MEMS Ultra-Wideband (UWB) Power Sensor Simulator

## Project Overview
This project is an interactive visualization of a microelectromechanical systems (MEMS) ultra-wideband (UWB) power sensor. It illustrates the conversion of invisible electromagnetic energy into measurable electrical signals through controlled mechanical motion.

**Note:** This simulator is designed as a conceptual and educational tool to illustrate operating principles rather than to function as a fabrication-level or numerical simulation.

## Research Inspiration
The simulator is inspired by published academic research on MEMS ultra-wideband power sensors that integrate a planar loop inductor with a vibrating diaphragm variable capacitor. 

In this architecture:
* **Induction:** Incoming UWB fields induce a voltage in the planar inductor, which acts as an integrated loop antenna.
* **Electrostatic Force:** This induces an electrostatic force across the MEMS capacitor.
* **Deflection:** A thin diaphragm deflects by picometers—one trillionth of a meter.
* **Capacitance Change:** These minute deflections produce measurable changes in capacitance.



## Why Mechanical Sensing?
Unlike conventional solid-state RF power detectors, this MEMS sensor relies on mechanical inertia to achieve a frequency-independent RMS response. Because electromagnetic operating frequencies are significantly higher than the diaphragm’s mechanical resonant frequency, the membrane responds only to the average (RMS) power of the incident field.

## Why a Simulator?
At the physical scale, diaphragm deflections and capacitance changes (measured in attifarads) are impossible to observe directly. This simulator magnifies and visualizes those interactions to make the underlying physics intuitive and accessible, bridging the gap between electromagnetic theory and MEMS mechanics.

## References and Attribution
This project is inspired by the following academic work:
* S. Vejella and S. Chowdhury, "A MEMS Ultra-Wideband (UWB) Power Sensor with a Fe-Co-B Core Planar Inductor and a Vibrating Diaphragm Capacitor," *Sensors*, 2021.

The original device concept and theoretical framework were developed within the **Electrical and Computer Engineering Department, University of Windsor**.

---

### Project Credit
**Visualization, Interface Design, and Conceptual Modeling** **Naimah Ishaque**
