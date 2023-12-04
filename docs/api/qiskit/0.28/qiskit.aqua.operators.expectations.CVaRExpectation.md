# qiskit.aqua.operators.expectations.CVaRExpectation

<span id="undefined" />

`CVaRExpectation(alpha, expectation=None)`

Compute the Conditional Value at Risk (CVaR) expectation value.

The standard approach to calculating the expectation value of a Hamiltonian w\.r.t. a state is to take the sample mean of the measurement outcomes. This corresponds to an estimator of the energy. However in several problem settings with a diagonal Hamiltonian, e.g. in combinatorial optimization where the Hamiltonian encodes a cost function, we are not interested in calculating the energy but in the lowest possible value we can find.

To this end, we might consider using the best observed sample as a cost function during variational optimization. The issue here, is that this can result in a non-smooth optimization surface. To resolve this issue, we can smooth the optimization surface by using not just the best observed sample, but instead average over some fraction of best observed samples. This is exactly what the CVaR estimator accomplishes \[1].

It is empirically shown, that this can lead to faster convergence for combinatorial optimization problems.

Let $\alpha$ be a real number in $[0,1]$ which specifies the fraction of best observed samples which are used to compute the objective function. Observe that if $\alpha = 1$, CVaR is equivalent to a standard expectation value. Similarly, if $\alpha = 0$, then CVaR corresponds to using the best observed sample. Intermediate values of $\alpha$ interpolate between these two objective functions.

## References

**\[1]: Barkoutsos, P. K., Nannicini, G., Robert, A., Tavernelli, I., and Woerner, S.,**

“Improving Variational Quantum Optimization using CVaR” [arXiv:1907.04769](https://arxiv.org/abs/1907.04769)

**Parameters**

*   **alpha** (`float`) – The alpha value describing the quantile considered in the expectation value.
*   **expectation** (`Optional`\[`ExpectationBase`]) – An expectation object to compute the expectation value. Defaults to the PauliExpectation calculation.

**Raises**

**NotImplementedError** – If the `expectation` is an AerPauliExpecation.

<span id="undefined" />

`__init__(alpha, expectation=None)`

**Parameters**

*   **alpha** (`float`) – The alpha value describing the quantile considered in the expectation value.
*   **expectation** (`Optional`\[`ExpectationBase`]) – An expectation object to compute the expectation value. Defaults to the PauliExpectation calculation.

**Raises**

**NotImplementedError** – If the `expectation` is an AerPauliExpecation.

## Methods

|                                                                                                                                                                           |                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| [`__init__`](#qiskit.aqua.operators.expectations.CVaRExpectation.__init__ "qiskit.aqua.operators.expectations.CVaRExpectation.__init__")(alpha\[, expectation])           | **type alpha**`float`                                                        |
| [`compute_variance`](#qiskit.aqua.operators.expectations.CVaRExpectation.compute_variance "qiskit.aqua.operators.expectations.CVaRExpectation.compute_variance")(exp\_op) | Returns the variance of the CVaR calculation                                 |
| [`convert`](#qiskit.aqua.operators.expectations.CVaRExpectation.convert "qiskit.aqua.operators.expectations.CVaRExpectation.convert")(operator)                           | Return an expression that computes the CVaR expectation upon calling `eval`. |

<span id="undefined" />

`compute_variance(exp_op)`

Returns the variance of the CVaR calculation

**Parameters**

**exp\_op** (`OperatorBase`) – The operator whose evaluation yields an expectation of some StateFn against a diagonal observable.

**Return type**

`Union`\[`list`, `float`]

**Returns**

**The variance of the CVaR estimate corresponding to the converted**

exp\_op.

**Raises**

**ValueError** – If the exp\_op does not correspond to an expectation value.

<span id="undefined" />

`convert(operator)`

Return an expression that computes the CVaR expectation upon calling `eval`. :type operator: `OperatorBase` :param operator: The operator to convert.

**Return type**

`OperatorBase`

**Returns**

The converted operator.