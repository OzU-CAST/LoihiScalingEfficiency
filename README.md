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

The latency figure when neuron number gets scaled up hints a key property of Loihi. When the partitioning algorithm explained above and the per neurocore neuron numbers are investigated it can be seen that the more neuron the network has which are of the same layer the more spread out it is on the chip which causes the number of neuron per neurocore to decrease. This trend happens for both micro-coded and hard-coded neurons. As the neurons are represented in the dendrite circuit along with CxState field in the SRAM, the decrease in neuron numbers per neurocore explain the decrease in latency since the dendrite circuit prcoess each neuron sequently except it is able to multi-thread but still in the end the neurons in each PE in dendrite circuit work serially. While this explains the behaviour of micro-coded neurons, the hard-coded neurons behave differently as they are all processed at the same time regarldess of the neurons that needs to be processed. This finding makes us believe that the Loihi microarchitecture optimizes the hard-coded neurons to a degree of fully parallel processing of neurons.


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/latency_K.png?raw=true)

In the conectivity test except few outliers we do not recieve any result that is not expected since the synaptic integration is considarbly fast and the dense process results in normally sparse or zero connections to be calculated anyway.
## Energy 


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/energy.png?raw=true)

The energy metric with neuron number scaling up shows that while there are more neurocore overheads with the overly spreaded neurons across neurocores, the latency decrease due to less workload per neurocore accomplishes to decrease overall energy dissipition.

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/energy_K.png?raw=true)

The connectivity results shows a slow fluctuations which may be caused by several reasons depending on the underlying microarchitecure. If Loihi 2 utilizes a zero-skipping algorithm as the non-zero weights decrease with increased connectivity the now computed weights may result in more energy dissipition. Another reason could be the compression of common weights. As the connectivity increases the common weights decrease (zero) which results in more memory usage along with more computation. 


## Spiking Activity


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/number_spikes.png?raw=true)

The spiking activity when the neuron numbers are upscaled since connectivity between spike generators and excitatory layers are fixed. This balance state is also satisfied per individual neuron on inhibitory layer. There is an expected exponential increase.

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/number_spikes_K.png?raw=true)

When the neuron number is constant the difference in connectivity as defined by the weight equatons and dynamic relation between connection probability should keep the network stable in terms of spiking rate. From the figure it can be seen that the spiking activity is stable around a point with some fluctuation.



## Derived Metrics


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Energy_per_neuron.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Energy_per_neuron_K.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Energy_per_neuron_per_spike.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Energy_per_neuron_per_spike_K.png?raw=true)


## Hardware Resources


![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/CxStates.png?raw=true)

Comparatmental states (CxStates) are implemented as 64 bit SRAM fields which store dynamic neuron states. Therefore each indiviudal neuron occupies predefined number of CxStates according to their neruon model implementation and the complexity of the model. As it is predefined and constant for a neuron model it is scaled by number of neurons.

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/CxStates_K.png?raw=true)

The conectivity probability under constant neuron number does not effect the SRAM memory needed for the network neurons thus do not incur and change during sweeping of the connectivity parameter.

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Synapses.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Synapses_K.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Cores.png?raw=true)

![alt text](https://github.com/OzU-CAST/LoihiScalingEfficiency/blob/main/Figs/Cores_K.png?raw=true)
