# Hippocampal Network Simulation

## Overview
This project provides a NEURON-based simulation of hippocampal networks, focusing on the interaction between pyramidal cells and interneurons. The model simulates key aspects of hippocampal circuit dynamics including recurrent excitation and feedback inhibition.

## Requirements
- Python 3.6+
- NEURON simulator (version 8.0+)
- NumPy
- Matplotlib

## Installation

1. Install NEURON following instructions at [https://neuron.yale.edu/neuron/download](https://neuron.yale.edu/neuron/download)

2. Install Python dependencies:
```bash
pip install numpy matplotlib
```

3. Confirm NEURON is properly installed and accessible from Python:
```python
from neuron import h
print(h.version)
```

## Files
- `hippocampal_network.py`: Main simulation script containing the network model
- `README.md`: This documentation file

## Usage

Run the simulation with default parameters:
```bash
python hippocampal_network.py
```

### Customizing the Simulation

The simulation can be modified by changing parameters in the main script:

```python
# Create network with custom number of cells
network = HippocampalNetwork(n_pyr=10, n_int=4)  # 10 pyramidal cells, 4 interneurons

# Customize stimulus parameters
network.add_stimulus(
    target_cells="pyr",  # Target population ("pyr" or "int")
    start=5,             # Start time (ms)
    interval=20,         # Average interval between spikes (ms)
    number=5,            # Number of spikes
    noise=0.2            # Noise/randomness factor (0-1)
)

# Run for longer duration
network.run_simulation(duration=500)  # 500 ms simulation
```

## Model Details

### Pyramidal Cell Model
- Multi-compartmental model with soma, dendrites, and apical dendrite
- Hodgkin-Huxley channels in the soma for action potential generation
- Passive properties in dendrites

### Interneuron Model
- Fast-spiking basket cell-inspired model
- Higher sodium conductance for fast-spiking behavior
- Faster synaptic dynamics than pyramidal cells

### Network Connectivity
- Excitatory connections from pyramidal cells to interneurons (60% probability)
- Inhibitory feedback connections from interneurons to pyramidal cells (70% probability)
- Synaptic delays of 1 ms

## Output
The simulation generates a figure showing voltage traces for all cells, saved as "hippocampal_network_activity.png".

## Extending the Model
For more biophysically detailed simulations, consider:

1. Adding calcium dynamics by compiling appropriate mod files:
   - Download calcium channel mechanisms from ModelDB
   - Compile with `nrnivmodl`
   - Update the model code to use these mechanisms

2. Adding h-current (Ih) to dendrites:
   - Essential for realistic hippocampal behavior
   - Available in many neuron model packages

3. Incorporating more complex morphologies:
   - The current model uses simplified geometry
   - Realistic morphologies can be imported from neuromorpho.org

## References
1. Cutsuridis, V., Graham, B. P., Cobb, S., & Vida, I. (Eds.). (2010). Hippocampal microcircuits: A computational modeler's resource book. Springer.
2. Bezaire, M. J., & Soltesz, I. (2013). Quantitative assessment of CA1 local circuits: Knowledge base for interneuron-pyramidal cell connectivity. Hippocampus, 23(9), 751-785.
