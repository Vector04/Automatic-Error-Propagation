# Automatic-Error-Propagation
This module allows you to create variables with uncertainties. Error propagation can be automated using this module.


## The floatE class
Allows for automated error propagation with uncorrelated errors.
All common operations are implemented, and also work with mixed 
floatE and float classes.
Features proper printing (with proper decimal / scientific notation)
Also has a LaTeXify() function that prints the variable in LaTeX code.
Usage: 

    from data_analysis_tools import *

    x = floatE(10, 1)
    y = floatE(2, 0.1)

    # Output: 12.0 ± 1.1
    print(x + y)

    # Output: 100 ± 20
    print(x ** 2)

    # Output: (6.60 ± 0.66)·10⁻³³
    print(x * 6.6e-34)

    # Output: 2.00 \pm 0.10
    print(y.LaTeXify())
    
##### Notes: 
* Sometimes the ascii is printed incorrectly, the ± sign could look like a � sign 
when a floatE variable is printed. To fix this, set fix_ascii (line 5) to true.
* Currently, this modules only propagates uncorrelated errors. This is fine for things like 
dividing two variables that both have an uncertainty, but it can go wrong if the expression is not symplified.
Expressions like `a - a` should give 0 (without uncertainties), but this is not always the case.
## The better_curve_fit() function
An improved version of the scipy.optimize.curve_fit that returns dict of floatE 
variables and a reduced chi squared. This dictionary displays its elements more conveniently.
Example:

    from data_analysis_tools import *
    xs, ys, sigmas = (...)

    def f(x, a, b):
        return x**a + b
    
    params, chi2 = better_curve_fit(f, xs, ys, p0=(1,0), sigma=dys)

    # Try out what happens here:
    print(params)

    # the parameter variables can still be accessed:
    a, b = params['a'], params['b']

