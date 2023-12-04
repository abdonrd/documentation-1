---
title: PauliFeatureMap
description: API reference for qiskit.circuit.library.PauliFeatureMap
in_page_toc_min_heading_level: 1
python_api_type: class
python_api_name: qiskit.circuit.library.PauliFeatureMap
---

# PauliFeatureMap[¶](#paulifeaturemap "Permalink to this headline")

<span id="qiskit.circuit.library.PauliFeatureMap" />

`PauliFeatureMap(feature_dimension=None, reps=2, entanglement='full', alpha=2.0, paulis=None, data_map_func=None, parameter_prefix='x', insert_barriers=False, name='PauliFeatureMap')`

Bases: [`qiskit.circuit.library.n_local.n_local.NLocal`](qiskit.circuit.library.NLocal "qiskit.circuit.library.n_local.n_local.NLocal")

The Pauli Expansion circuit.

The Pauli Expansion circuit is a data encoding circuit that transforms input data $\vec{x} \in \mathbb{R}^n$ as

$$
U_{\Phi(\vec{x})}=\exp\left(i\sum_{S\subseteq [n]}
\phi_S(\vec{x})\prod_{i\in S} P_i\right)
$$

The circuit contains `reps` repetitions of this transformation. The variable $P_i \in \{ I, X, Y, Z \}$ denotes the Pauli matrices. The index $S$ describes connectivities between different qubits or datapoints: $S \in \{\binom{n}{k}\ combinations,\ k = 1,... n \}$. Per default the data-mapping $\phi_S$ is

$$
\begin{split}\phi_S(\vec{x}) = \begin{cases}
    x_0 \text{ if } k = 1 \\
    \prod_{j \in S} (\pi - x_j) \text{ otherwise }
    \end{cases}\end{split}
$$

For example, if the Pauli strings are chosen to be $P_0 = Z$ and $P_{0,1} = YY$ on 2 qubits and with 1 repetition using the default data-mapping, the Pauli evolution feature map is represented by:

```python
┌───┐┌──────────────┐┌──────────┐                                             ┌───────────┐
┤ H ├┤ U1(2.0*x[0]) ├┤ RX(pi/2) ├──■───────────────────────────────────────■──┤ RX(-pi/2) ├
├───┤├──────────────┤├──────────┤┌─┴─┐┌─────────────────────────────────┐┌─┴─┐├───────────┤
┤ H ├┤ U1(2.0*x[1]) ├┤ RX(pi/2) ├┤ X ├┤ U1(2.0*(pi - x[0])*(pi - x[1])) ├┤ X ├┤ RX(-pi/2) ├
└───┘└──────────────┘└──────────┘└───┘└─────────────────────────────────┘└───┘└───────────┘
```

Please refer to [`ZFeatureMap`](qiskit.circuit.library.ZFeatureMap "qiskit.circuit.library.ZFeatureMap") for the case $k = 1$, $P_0 = Z$ and to [`ZZFeatureMap`](qiskit.circuit.library.ZZFeatureMap "qiskit.circuit.library.ZZFeatureMap") for the case $k = 2$, $P_0 = Z$ and $P_{0,1} = ZZ$.

## Examples

```python
>>> prep = PauliFeatureMap(2, reps=1, paulis=['ZZ'])
>>> print(prep)
     ┌───┐
q_0: ┤ H ├──■───────────────────────────────────────■──
     ├───┤┌─┴─┐┌─────────────────────────────────┐┌─┴─┐
q_1: ┤ H ├┤ X ├┤ U1(2.0*(pi - x[0])*(pi - x[1])) ├┤ X ├
     └───┘└───┘└─────────────────────────────────┘└───┘
```

```python
>>> prep = PauliFeatureMap(2, reps=1, paulis=['Z', 'XX'])
>>> print(prep)
     ┌───┐┌──────────────┐┌───┐                                             ┌───┐
q_0: ┤ H ├┤ U1(2.0*x[0]) ├┤ H ├──■───────────────────────────────────────■──┤ H ├
     ├───┤├──────────────┤├───┤┌─┴─┐┌─────────────────────────────────┐┌─┴─┐├───┤
q_1: ┤ H ├┤ U1(2.0*x[1]) ├┤ H ├┤ X ├┤ U1(2.0*(pi - x[0])*(pi - x[1])) ├┤ X ├┤ H ├
     └───┘└──────────────┘└───┘└───┘└─────────────────────────────────┘└───┘└───┘
```

```python
>>> prep = PauliFeatureMap(2, reps=1, paulis=['ZY'])
>>> print(prep)
     ┌───┐┌──────────┐                                             ┌───────────┐
q_0: ┤ H ├┤ RX(pi/2) ├──■───────────────────────────────────────■──┤ RX(-pi/2) ├
     ├───┤└──────────┘┌─┴─┐┌─────────────────────────────────┐┌─┴─┐└───────────┘
q_1: ┤ H ├────────────┤ X ├┤ U1(2.0*(pi - x[0])*(pi - x[1])) ├┤ X ├─────────────
     └───┘            └───┘└─────────────────────────────────┘└───┘
```

```python
>>> from qiskit.circuit.library import EfficientSU2
>>> prep = PauliFeatureMap(3, reps=3, paulis=['Z', 'YY', 'ZXZ'])
>>> wavefunction = EfficientSU2(3)
>>> classifier = prep.compose(wavefunction
>>> classifier.num_parameters
27
>>> classifier.count_ops()
OrderedDict([('cx', 39), ('rx', 36), ('u1', 21), ('h', 15), ('ry', 12), ('rz', 12)])
```

## References

**\[1]: Havlicek et al. (2018), Supervised learning with quantum enhanced feature spaces.**

[arXiv:1804.11326](https://arxiv.org/abs/1804.11326)

Create a new Pauli expansion circuit.

**Parameters**

*   **feature\_dimension** (`Optional`\[`int`]) – Number of qubits in the circuit.
*   **reps** (`int`) – The number of repeated circuits.
*   **entanglement** (`Union`\[`str`, `List`\[`List`\[`int`]], `Callable`\[\[`int`], `List`\[`int`]]]) – Specifies the entanglement structure. Refer to [`NLocal`](qiskit.circuit.library.NLocal "qiskit.circuit.library.NLocal") for detail.
*   **alpha** (`float`) – The Pauli rotation factor, multiplicative to the pauli rotations
*   **paulis** (`Optional`\[`List`\[`str`]]) – A list of strings for to-be-used paulis. If None are provided, `['Z', 'ZZ']` will be used.
*   **data\_map\_func** (`Optional`\[`Callable`\[\[`ndarray`], `float`]]) – A mapping function for data x which can be supplied to override the default mapping from `self_product()`.
*   **parameter\_prefix** (`str`) – The prefix used if default parameters are generated.
*   **insert\_barriers** (`bool`) – If True, barriers are inserted in between the evolution instructions and hadamard layers.

## Methods Defined Here

### pauli\_block

<span id="qiskit.circuit.library.PauliFeatureMap.pauli_block" />

`PauliFeatureMap.pauli_block(pauli_string)`

Get the Pauli block for the feature map circuit.

### pauli\_evolution

<span id="qiskit.circuit.library.PauliFeatureMap.pauli_evolution" />

`PauliFeatureMap.pauli_evolution(pauli_string, time)`

Get the evolution block for the given pauli string.

## Attributes

<span id="qiskit.circuit.library.PauliFeatureMap.alpha" />

### alpha

The Pauli rotation factor (alpha).

**Return type**

`float`

**Returns**

The Pauli rotation factor.

<span id="qiskit.circuit.library.PauliFeatureMap.ancillas" />

### ancillas

Returns a list of ancilla bits in the order that the registers were added.

**Return type**

`List`\[[`AncillaQubit`](qiskit.circuit.AncillaQubit "qiskit.circuit.quantumregister.AncillaQubit")]

<span id="qiskit.circuit.library.PauliFeatureMap.calibrations" />

### calibrations

Return calibration dictionary.

The custom pulse definition of a given gate is of the form `{'gate_name': {(qubits, params): schedule}}`

**Return type**

`dict`

<span id="qiskit.circuit.library.PauliFeatureMap.clbits" />

### clbits

Returns a list of classical bits in the order that the registers were added.

**Return type**

`List`\[[`Clbit`](qiskit.circuit.Clbit "qiskit.circuit.classicalregister.Clbit")]

<span id="qiskit.circuit.library.PauliFeatureMap.data" />

### data

<span id="qiskit.circuit.library.PauliFeatureMap.entanglement" />

### entanglement

Get the entanglement strategy.

**Return type**

`Union`\[`str`, `List`\[`str`], `List`\[`List`\[`str`]], `List`\[`int`], `List`\[`List`\[`int`]], `List`\[`List`\[`List`\[`int`]]], `List`\[`List`\[`List`\[`List`\[`int`]]]], `Callable`\[\[`int`], `str`], `Callable`\[\[`int`], `List`\[`List`\[`int`]]]]

**Returns**

The entanglement strategy, see `get_entangler_map()` for more detail on how the format is interpreted.

<span id="qiskit.circuit.library.PauliFeatureMap.entanglement_blocks" />

### entanglement\_blocks

<span id="qiskit.circuit.library.PauliFeatureMap.extension_lib" />

### extension\_lib

`= 'include "qelib1.inc";'`

<span id="qiskit.circuit.library.PauliFeatureMap.feature_dimension" />

### feature\_dimension

Returns the feature dimension (which is equal to the number of qubits).

**Return type**

`int`

**Returns**

The feature dimension of this feature map.

<span id="qiskit.circuit.library.PauliFeatureMap.global_phase" />

### global\_phase

Return the global phase of the circuit in radians.

**Return type**

`Union`\[[`ParameterExpression`](qiskit.circuit.ParameterExpression "qiskit.circuit.parameterexpression.ParameterExpression"), `float`]

<span id="qiskit.circuit.library.PauliFeatureMap.header" />

### header

`= 'OPENQASM 2.0;'`

<span id="qiskit.circuit.library.PauliFeatureMap.initial_state" />

### initial\_state

Return the initial state that is added in front of the n-local circuit.

**Return type**

[`QuantumCircuit`](qiskit.circuit.QuantumCircuit "qiskit.circuit.quantumcircuit.QuantumCircuit")

**Returns**

The initial state.

<span id="qiskit.circuit.library.PauliFeatureMap.insert_barriers" />

### insert\_barriers

If barriers are inserted in between the layers or not.

**Return type**

`bool`

**Returns**

`True`, if barriers are inserted in between the layers, `False` if not.

<span id="qiskit.circuit.library.PauliFeatureMap.instances" />

### instances

`= 2144`

<span id="qiskit.circuit.library.PauliFeatureMap.metadata" />

### metadata

The user provided metadata associated with the circuit

The metadata for the circuit is a user provided `dict` of metadata for the circuit. It will not be used to influence the execution or operation of the circuit, but it is expected to be passed between all transforms of the circuit (ie transpilation) and that providers will associate any circuit metadata with the results it returns from execution of that circuit.

**Return type**

`dict`

<span id="qiskit.circuit.library.PauliFeatureMap.num_ancillas" />

### num\_ancillas

Return the number of ancilla qubits.

**Return type**

`int`

<span id="qiskit.circuit.library.PauliFeatureMap.num_clbits" />

### num\_clbits

Return number of classical bits.

**Return type**

`int`

<span id="qiskit.circuit.library.PauliFeatureMap.num_layers" />

### num\_layers

Return the number of layers in the n-local circuit.

**Return type**

`int`

**Returns**

The number of layers in the circuit.

<span id="qiskit.circuit.library.PauliFeatureMap.num_parameters" />

### num\_parameters

**Return type**

`int`

<span id="qiskit.circuit.library.PauliFeatureMap.num_parameters_settable" />

### num\_parameters\_settable

The number of distinct parameters.

<span id="qiskit.circuit.library.PauliFeatureMap.num_qubits" />

### num\_qubits

Returns the number of qubits in this circuit.

**Return type**

`int`

**Returns**

The number of qubits.

<span id="qiskit.circuit.library.PauliFeatureMap.op_start_times" />

### op\_start\_times

Return a list of operation start times.

This attribute is enabled once one of scheduling analysis passes runs on the quantum circuit.

**Return type**

`List`\[`int`]

**Returns**

List of integers representing instruction start times. The index corresponds to the index of instruction in `QuantumCircuit.data`.

**Raises**

**AttributeError** – When circuit is not scheduled.

<span id="qiskit.circuit.library.PauliFeatureMap.ordered_parameters" />

### ordered\_parameters

The parameters used in the underlying circuit.

This includes float values and duplicates.

## Examples

```python
>>> # prepare circuit ...
>>> print(nlocal)
     ┌───────┐┌──────────┐┌──────────┐┌──────────┐
q_0: ┤ Ry(1) ├┤ Ry(θ[1]) ├┤ Ry(θ[1]) ├┤ Ry(θ[3]) ├
     └───────┘└──────────┘└──────────┘└──────────┘
>>> nlocal.parameters
{Parameter(θ[1]), Parameter(θ[3])}
>>> nlocal.ordered_parameters
[1, Parameter(θ[1]), Parameter(θ[1]), Parameter(θ[3])]
```

**Return type**

`List`\[[`Parameter`](qiskit.circuit.Parameter "qiskit.circuit.parameter.Parameter")]

**Returns**

The parameters objects used in the circuit.

<span id="qiskit.circuit.library.PauliFeatureMap.parameter_bounds" />

### parameter\_bounds

The parameter bounds for the unbound parameters in the circuit.

**Return type**

`Optional`\[`List`\[`Tuple`\[`float`, `float`]]]

**Returns**

A list of pairs indicating the bounds, as (lower, upper). None indicates an unbounded parameter in the corresponding direction. If `None` is returned, problem is fully unbounded.

<span id="qiskit.circuit.library.PauliFeatureMap.parameters" />

### parameters

**Return type**

`ParameterView`

<span id="qiskit.circuit.library.PauliFeatureMap.paulis" />

### paulis

The Pauli strings used in the entanglement of the qubits.

**Return type**

`List`\[`str`]

**Returns**

The Pauli strings as list.

<span id="qiskit.circuit.library.PauliFeatureMap.preferred_init_points" />

### preferred\_init\_points

The initial points for the parameters. Can be stored as initial guess in optimization.

**Return type**

`Optional`\[`List`\[`float`]]

**Returns**

The initial values for the parameters, or None, if none have been set.

<span id="qiskit.circuit.library.PauliFeatureMap.prefix" />

### prefix

`= 'circuit'`

<span id="qiskit.circuit.library.PauliFeatureMap.qregs" />

### qregs

A list of the quantum registers associated with the circuit.

<span id="qiskit.circuit.library.PauliFeatureMap.qubits" />

### qubits

Returns a list of quantum bits in the order that the registers were added.

**Return type**

`List`\[[`Qubit`](qiskit.circuit.Qubit "qiskit.circuit.quantumregister.Qubit")]

<span id="qiskit.circuit.library.PauliFeatureMap.reps" />

### reps

The number of times rotation and entanglement block are repeated.

**Return type**

`int`

**Returns**

The number of repetitions.

<span id="qiskit.circuit.library.PauliFeatureMap.rotation_blocks" />

### rotation\_blocks

The blocks in the rotation layers.

**Return type**

`List`\[[`Instruction`](qiskit.circuit.Instruction "qiskit.circuit.instruction.Instruction")]

**Returns**

The blocks in the rotation layers.
