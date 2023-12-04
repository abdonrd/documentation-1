---
title: QFI
description: API reference for qiskit.algorithms.gradients.QFI
in_page_toc_min_heading_level: 1
python_api_type: class
python_api_name: qiskit.algorithms.gradients.QFI
---

# QFI[¶](#qfi "Permalink to this headline")

<span id="qiskit.algorithms.gradients.QFI" />

`QFI(qgt, options=None)`

Bases: `abc.ABC`

Computes the Quantum Fisher Information (QFI) given a pure, parameterized quantum state. QFI is defined as:

$$
\mathrm{QFI}_{ij}= 4 \mathrm{Re}[\langle \partial_i \psi | \partial_j \psi \rangle
- \langle\partial_i \psi | \psi \rangle \langle\psi | \partial_j \psi \rangle].
$$

**Parameters**

*   **qgt** ([*BaseQGT*](qiskit.algorithms.gradients.BaseQGT "qiskit.algorithms.gradients.BaseQGT")) – The quantum geometric tensor used to compute the QFI.
*   **options** ([*Options*](qiskit.providers.Options "qiskit.providers.Options") *| None*) – Backend runtime options used for circuit execution. The order of priority is: options in `run` method > QFI’s default options > primitive’s default setting. Higher priority setting overrides lower priority setting.

## Methods

### run

<span id="qiskit.algorithms.gradients.QFI.run" />

`QFI.run(circuits, parameter_values, parameters=None, **options)`

Run the job of the QFIs on the given circuits.

**Parameters**

*   **circuits** – The list of quantum circuits to compute the QFIs.
*   **parameter\_values** – The list of parameter values to be bound to the circuit.
*   **parameters** – The sequence of parameters to calculate only the QFIs of the specified parameters. Each sequence of parameters corresponds to a circuit in `circuits`. Defaults to None, which means that the QFIs of all parameters in each circuit are calculated.
*   **options** – Primitive backend runtime options used for circuit execution. The order of priority is: options in `run` method > QFI’s default options > QGT’s default setting. Higher priority setting overrides lower priority setting.

**Returns**

The job object of the QFIs of the expectation values. The i-th result corresponds to `circuits[i]` evaluated with parameters bound as `parameter_values[i]`.

### update\_default\_options

<span id="qiskit.algorithms.gradients.QFI.update_default_options" />

`QFI.update_default_options(**options)`

Update the gradient’s default options setting.

**Parameters**

**\*\*options** – The fields to update the default options.

## Attributes

<span id="qiskit.algorithms.gradients.QFI.options" />

### options

Return the union of QGT’s options setting and QFI’s default options, where, if the same field is set in both, the QFI’s default options override the QGT’s default setting.

**Return type**

[`Options`](qiskit.providers.Options "qiskit.providers.options.Options")

**Returns**

The QFI default + QGT options.
