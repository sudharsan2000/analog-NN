# Analog-Neural Network
Training Neural Networks using Analog circuits

## Implementing an Analog ANN
* In the Analog circuit implemented the weights of the network are stored in capacitors in Op-amp integrators.

* For every training data, circuit must directly give a weight combination to make the actual output almost same with the expected output. 

* Then all such weights are combined and stored as a vector. 

* After a number of iterations the average of weights can be treated as an optimal solution.

## Neurons
* The neurons need sum up the input and perform a nonlinear activation function.

* The sum can be achieved with an op-amp adder shown in Fig.

* ReLU function shown in the following graph is considered for the activation function.

* The difference is that the lower limit of our activation function has a small positive offset and there is also a upper limit because of the limit of the supply voltage.

![Buffer](https://i.imgur.com/8fkuBcp.png)   ![ReLU](https://i.imgur.com/JwjPki7.png)

## Synapses 
* The synapses store the weights and multiply them with the outputs of the last neurons. 

* The capacitor in integrator circuit is used to store a voltage level and output of the integrator can be used as the weight.

* In this way the charging speed (and hence training) can be controlled directly by a voltage and a zero input voltage will hold the output.

* Let Vw be the output voltage, Vadjust be the input voltage used to adjust the weight. Then the relation between them can be given by:
![Formula](https://i.imgur.com/M7WikFe.png)


Followed by this multiply operation has to be done. This can be achieved by an analog multiplier circuit. (IC AD633 in this case)

### Synapses Circuit
![img](https://i.imgur.com/iyn5nff.png)

## Feedback circuit
* The neurons and synapses can only perform the feedforward of an ANN. In order to train a network, feedback circuits are needed.

* The way to adjust the weights should be designed to make the feedback end up with the equal between the actual output and the expected output of the ANN. So we can employ a voltage follower.

* The non-inverting input of the op-amp is the expected output of the ANN and the inverting input of the op-amp is the actual output of the ANN. 

* However, with the delay of the op-amp and the ANN circuit, the output of the ANN would be fluctuate around the expected voltage. Specifically, the gain of the op-amp is high, which means a small error would create a big signal to adjust the weights. So we use another feedback to reduce gain of the error along with resistors (R1 and R2) in feedback path to control gain.

* Let  Vadjust be the adjust signal, and Vex    and Vac are the expected output and the actual output. Then the relation between them can be obtained as:
![img](https://i.imgur.com/D5KEhdw.png)

### Feedback Circuit
![img](https://i.imgur.com/2qsd358.png)

Circuit with improved gain control

![img](https://i.imgur.com/eP1nFNx.png)

## Full Circuit
### One Neuron trainer 
![img](https://i.imgur.com/P1xCe4O.png)

Where the "WEIGHT" block is 

![img](https://i.imgur.com/ddtCIo7.png)

## Simulation Results
[LT Spice](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html) was used for all simulations.

![img](https://i.imgur.com/HWsbHeJ.png)

For an input signal of 5v the graph shows:
* The weight calculated for the Neuron (Red curve).
* The expected result (Green curve)
* The obtained result (Blue curve)


So we  observe that the neuron rapidly trains based on the expected signal and input fed for it to calculate weight. 

## References 

* https://ieeexplore.ieee.org/document/9018997
* https://link.springer.com/chapter/10.1007/978-3-642-23866-6_8
* Fundamentals of Microelectronics by Bhezad Razavi






