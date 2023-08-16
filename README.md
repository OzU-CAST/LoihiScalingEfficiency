# Loihi 2 Scaling Efficiency

This repository includes the extended graphs that were not able to make it to the paper due to space constraints

## Measurement Schemes

Benchmarking is done using a WTA network with different topologies and different neuron models. The network has run in two different configurations. First the scaling of neuron  numbers has been analyzed by scaling up the neuron populations. Lastly we effectively sweep the presynaptic connections of the neurons (K) which can be considered as the sparsity in the connections.

## Loihi 2 Probes

Loihi extension for Lava software, which is for INRC members only, provides probe class that communicates with onboard measurement circuits on the Loihi board for benchmarking. There are power/energy, time, activity and memory probes ready to use. The power probe is capable of measuring static/dynamic power along with neurocore, SRAM and IO power. Execution time probe breaks down each algorithmic time-step into its phases. Activity probe counts the computations happening inside each neurocore such as synaptic operations, dendritic operations and axon spike counts. Memory probe provides SRAM utilization of neurocores.


## Power


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/power.png?raw=true)

In the figure above it can be seen that the power consumption of the network increases linearly as the network scales up. This is mainly due to the fact that the current partitioning algorithm of LAVA compiler for Loihi. The algorithm calculates an unconstrained abstract neurocore for each net object, which is a connection and dendrite process merged, if there are any violations defined by the Loihi constraint database file the algorithm simply divides the resulting neurocore iteratively until constraints are satisfied. This behaviour causes more neurocore allocation as the network grows and overhead of an active neurocore results in higher power consumption.

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/power_K.png?raw=true)

As for the connectivity analysis it must be said that, at the time of this research has been conducted the sparse connectivity was not supported in LAVA compiler. Therefore all the connections of are network are defined as fully connected layers. The Loihi SRAM partition algorithm is capable of compressing similar weights depending on the precision of the synaptic weights. How this compression is applied is unknown to us. The problem with dense connection is the fact that the connection process does not cull the zero weights which results in the same mapping on Loihi regardless of connectivity probability. As a result it is expected to have similar power measurements but there are fluctuations which are caused by synaptic weights precision. Since this network is a balanced network as the connectivity increases to keep the spiking rate stable we scale the weights according to number K so that the weights decrease as more connections are made but Loihi synapses have only so much bits that we can use to represent weights (8 bits at most) and this constraint causes error margins in the weights which causes instability in the spiking rate, and this reflects on the power measurement.

## Latency


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/latency.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/latency_K.png?raw=true)


## Energy 


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/energy.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/energy_K.png?raw=true)



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
