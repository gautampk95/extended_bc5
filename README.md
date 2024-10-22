# Extended BC5: A Comparison of Results Produced by Python and R Implementations

In my master's thesis, I developed an extension of the well-known Dose-Response (DR) curve method, introducing a model capable of incorporating multiple explanatory variables. This new approach, termed the "Extended BC.5 method," was shown to be applicable not only in Toxicology but also across various other fields. The original work was implemented in R due to the comprehensive DR modeling capabilities of its libraries. Recently, I translated this work into Python by developing a [library](https://github.com/gautampk95/drm_basic) that supports common DR models, successfully replicating the thesis results in a more widely adopted programming environment.

This project primarily focuses on the key results obtained from my thesis work in R, comparing them with the implementations in Python as demonstrated throughout this project.

## Proposed Extended BC.5 method
In the thesis work, the extended BC.5 method comprised 5 functions in its formulation, as shown below:

$$ f(x_i; u_i, v_i, ...) = c(u_i, v_i, ...) + \frac{d(u_i, v_i, ...) - c(u_i, v_i, ...) + f(u_i, v_i, ...)x_i}{1+ \text{exp}(b(u_i, v_i, ...)(\log(x_i) - \log(e(u_i, v_i, ...))))} $$

After finding the variable "Pressure", denoted as $p$, to include in all the functions of the proposed method, the extended BC.5 is formulated as:

$$  f(x_i, p_i) = c(p_i) + \frac{d(p_i) - c(p_i) + f(p_i)x_i}{1 + \text{exp}(b(p_i)(\log(x_i) - \log(e(p_i))))} $$

Here, $x$ is the time variable.The initial intercept values are crucial for identifying local minima. These values are calculated based on the estimates for the parameters $b, c, d, e$ and $f$, as demonstrated in the Jupyter notebook.

## Optimization: BFGS

The models are constructed separately for the training data associated with different gases.

| Gas      | RMSE | MAE  |
|:----------:|:----:|:-----------:|
| CO<sub>2</sub>  | 9.9047  | 7.1199  |
| Helium  | 43.0169  | 26.5585    |
| Air (Luft) | 14.2676  | 7.6325      |

**Table 1**: Results obtained from Python implementation.

| Gas      | RMSE | MAE  |
|:----------:|:----:|:-----------:|
| CO<sub>2</sub>  | 11.9659  | 8.5416  |
| Helium  | 43.0170  | 26.5588    |
| Air (Luft) | 14.2680  | 7.6332      |

**Table 2**: Results obtained from R implementation.

From Tables 1 and 2, the following observations can be drawn regarding the model fits in both programming environments:
* The Extended BC.5 model developed for CO<sub>2</sub> demonstrates a good fit in the Python implementation.
* The models for Helium and Air yield similar fits in the Python implementation compared to those in the R implementation.


## Optimization: Nelder-Mead

| Gas      | RMSE | MAE  |
|:----------:|:----:|:-----------:|
| CO<sub>2</sub>  | 13.8964  | 10.5373  |
| Helium  | 44.3025  | 29.7143    |
| Air (Luft) | 20.1633  | 12.9566      |

**Table 3**: Results obtained from Python implementation.

| Gas      | RMSE | MAE  |
|:----------:|:----:|:-----------:|
| CO<sub>2</sub>  | 12.2258  | 9.2776  |
| Helium  | 43.8554  | 29.2820    |
| Air (Luft) | 23.0343  | 15.1110      |

**Table 4**: Results obtained from R implementation.

From Tables 3 and 4, the following observations can be drawn regarding the model fits in both programming environments:
* Although the Nelder-Mead optimization method is not ideal for this modeling case, the R implementation achieved slightly better results for the models built using data from CO<sub>2</sub> and Helium.
* Interestingly, for the model developed using Air data, the Python implementation produces better results.

## Non-linear functions in the model function. Optimization: BFGS

| Gas      | RMSE | MAE  |
|:----------:|:----:|:-----------:|
| CO<sub>2</sub>  | 8.0685  | 5.6333  |
| Helium  | 52.1970  | 30.3804    |
| Air (Luft) | 14.2676  | 7.6326      |

**Table 5**: Results obtained from Python implementation.

| Gas      | RMSE | MAE  |
|:----------:|:----:|:-----------:|
| CO<sub>2</sub>  | 8.0684  | 5.6332  |
| Helium  | 52.2065  | 30.3850    |
| Air (Luft) | 13.8897  | 7.2445      |

**Table 6**: Results obtained from R implementation.

## Conclusions
**Note**: The R implementation utilized powerful server nodes to obtain results, while the Python implementation was executed on a local machine equipped with an Intel Core i7 9th generation processor. Surprisingly, the Python implementation is faster, and its time complexity is comparable to that of the server nodes supporting R.


