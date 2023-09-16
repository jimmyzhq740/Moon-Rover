# Moon-Rover
The project task involves the design of a remotely-controlled lunar rover with the primary objective of exploring the lunar landscape and identifying a variety of unusual rocks. These rocks exhibit distinctive characteristics, emitting a combination of sinusoidal radio signals modulated with square waves, infrared pulse trains, acoustic signals, and magnetic fields. Additionally, they are equipped with LEDs that emit various colors of light.

My designated role are as follows:
* Demodulating the modulated signals and accurately measuring the frequencies of the radio signals.
* Undertaking the design of the rover's chassis and its integral components.
* Developing a comprehensive program for an FPGA-based camera system with the capability to detect and discern the colors of the rocks.

# Design Specification
## Design:
Rover.stl files shows the design of the rover in stl format. Each component can be 3D printed. 

## Vision: 
This submodule involves the FPGA-based camera system to detect the rock colours. It emphasizes the implementation and visualization aspects of the FPGA. The system utilizes cameras mounted on the rover to detect rocks of three different colors: blue, yellow, and red. 

The top-level design entity for this submodule is stored in 'EEE_IMGPRO.V', which will subsequently instantiate lower-level entities. The top-level entity encompasses the following approaches to facilitate successful color detection:
* Color Thresholding: The system employs customized thresholds to selectively filter out colors other than blue, yellow, and red. This process is designed to concentrate on these specific colors.
* Visual Enhancement: Color thresholding techniques are employed to identify and accentuate crucial areas within the image. These critical areas, representing the rock colors, are highlighted in the image by generating a modified version that emphasizes the detected regions while rendering non-detected areas in grayscale.
* Region Boundary Tracking for Color Detection: Subsequently, the system engages in tracking the boundaries of distinct colors within the image by analyzing pixel traversal. To accomplish this, registers are established to store the minimum and maximum coordinates for each color region. As valid red, blue, or yellow pixels are processed, the corresponding boundary registers are updated. The coordinates of the current pixel are compared with the stored values, and necessary adjustments are made to the boundaries.
* State Machine and First-In-First-Out Write (FIFO): A state machine is constructed to generate output comprising the color ID and the bounding box coordinates for the respective region. Ultimately, these messages are written into a FIFO data structure, which is programmed in 'MSG_FIFO.V'.

## Radio Sensor:
The sensor to detect the radio signal consists of a two stage non-inverting amplifier to amplify the modulated radio wave and an envelop detector to filter the high frequency component of the modulated radio wave. This circuit ensures the signal is demodulated into the original square wave. The radio_sensor.png shows the circuit simulated on LTSpice. 
