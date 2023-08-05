# Loihi 2 Scaling Efficiency

This repository includes the extended graphs that were not able to make it to the paper due to space constraints

## Measurement Schemes

Benchmarking is done using a WTA network with different topologies and different neuron models. The network has run in two different configurations. First the scaling of neuron  numbers has been analyzed by scaling up the neuron populations. Lastly we effectively sweep the presynaptic connections of the neurons (K) which can be considered as the sparsity in the connections.

## Loihi 2 Probes

Loihi extension for Lava software, which is for INRC members only, provides probe class that communicates with onboard measurement circuits on the Loihi board for benchmarking. There are power/energy, time, activity and memory probes ready to use. The power probe is capable of measuring static/dynamic power along with neurocore, SRAM and IO power. Execution time probe breaks down each algorithmic time-step into its phases. Activity probe counts the computations happening inside each neurocore such as synaptic operations, dendritic operations and axon spike counts. Memory probe provides SRAM utilization of neurocores.


## Power


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/power.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/power_K.png?raw=true)

## Energy 


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/energy.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/energy_K.png?raw=true)


## Latency


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/latency.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/latency_K.png?raw=true)


## Spiking Activity


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/number_spikes.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/number_spikes_K.png?raw=true)



## Derived Metrics


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Energy_per_neuron.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Energy_per_neuron_K.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Energy_per_neuron_per_spike.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Energy_per_neuron_per_spike_K.png?raw=true)


## Hardware Resources

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/CxStates.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/CxStates_K.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Synapses.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Synapses_K.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Cores.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Cores_K.png?raw=true)
