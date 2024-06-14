------------------------------------------------------------------------
# BEP Metamaterial

Code of the geometrical optimisation of a metamaterial to obtain quasi-zero-stiffness.

------------------------------------------------------------------------
## Table of Contents
1. [Installation](#installation)
2. [Usage](#usage)
3. [Features](#features)
4. [Contributing](#contributing)
5. [Acknowledgements](#acknowledgements)

------------------------------------------------------------------------

## 1. Installation <a name="installation"></a>

1.1 Prerequisites: Python 3.8 & Pycharm 2024.1.3.

1.2 Open documents: It is recommended to open both documents in Pycharm.

## 2. Usage <a name="usage"></a>

2.1: Running the code: press on the 2 green arrows to run the whole code at once, or press on the single green arrow to run only one cell at once.

2.2: Altering the code is at your own risk. More info in #features section.

## 3. Features <a name="features"></a>

3.1: This code can optimise a set of parameters to create quasi-zero stiffness. At the end, the optimised parameters are printed as well as the size of one side of the full-sized geometry, the length of the QZS region and the QZS percentage over the possible compression range.  

3.2: Here, an in-depth manual is written on how the Python code was constructed and why certain choices were made.

After importing the necessary libraries, the normalised initial guesses are defined. These guesses are good by hand-determined values for the parameters. Consequently, the bounds for the parameters are determined and normalised after. Next, the number of iterations and the temperature of the basinhopping are set.

The bounds of the four optimised values are mainly based on manufacturing and structural limits. The lower limit of $t$, the space between the holes, is 1 mm due to manufacturing limits. The upper limit is 1 cm because if $t$ is larger than that the structure is not thin-walled anymore. The smallest value was calculated for a tension bar with $\alpha$ equal to 1 mm and $\beta$ equal to 5 mm. This is the manufacturing limit of 1mm and the 5 mm was to ensure that the tension bar would not break because a 1x1 mm tension bar would have been a big risk. The upper and lower limits of the holes (5mm - 5cm) were set to limit the total size of a four (2x2) and sixteen (4x4) hole metamaterial. All of these bounds are normalised in order to ensure proper functionality of the basin hopping optimiser. The optimiser uses a 'temperature' parameter to characterise the size of the jumps it takes between iterations. Having large differences in the size of these parameters by not normalising them means that large parameters are only changed marginally or small parameters are changed an extreme amount, depending on the set temperature.

The next step is to define all geometric variables and energy equations. The force and stiffness equations are then derived from the energy equations. All important equations are now defined, only the parameters need to be denormalised to use in these equations. This is done by linearly interpolating every parameter. Using these parameters the model variables are calculated.

Consequently the model is constructed. The model first retrieves all variables, parameters and equations. Then converts the Sympy functions into functions that allow numeric evaluation by the command lambdify. The functions were earlier written with Sympy because this is faster for deriving the energy equations. Last but not least the minimal value of the stiffness is calculated. This value is the inclination point of the force function. The point is defined as one where the difference between the previous step and the next step is greater than the value of the point itself. If for some reason this never happens in the function, the value of the inclination point is set to be the first step value. By doing this, the result is the same as a penalty, because it automatically translates into a small QZS region.

The force bounds are calculated by finding the corresponding force to the inclination point. A 0.5\% margin is used to define the flatness of the graph. The intersection between these bounds and the force-compression graph is then used to calculate the length of the QZS plateau. The length of this plateau is the horizontal distance between the two intersection points. If one of the bounds does not have an intersection with the force function, a penalty is issued. Another penalty is issued when the force function crosses the upper bound before the lower bound. This only happens when the metamaterial has a negative stiffness at the start. It was observed that a negative stiffness within the bounds of compression did not interfere with the functioning of the metamaterial and is therefore not penalised. These two penalties have different low values for the length, this is done to be able to see when which penalty is due.

Starting the definition of the cost function requires determining allowed jumps for the basin hopping optimiser as this is not built-in functionality, if the optimiser makes an illegal jump according to the set bounds it gets penalised. After this, the force bounds are inserted into the code and the number of intersections between the force bounds and the force function is checked and a penalty is applied if this is anything other than one intersection with the bottom bound and one intersection with the top bound. The final penalties are based on the behaviour of the force graph, the first occurs if the stiffness graph starts positive as starting with negative stiffness gave unexpected unwanted behaviour. The last penalty is to make sure the radius with the tension bar is bigger than the radius without a tension bar. This is needed so that the holes of the metamaterial deflect in the correct directions. Ultimately the actual cost function can be defined. It is defined as the total length of compression divided by the distance between the intersections of the bounds and the force graph. This is one over the desired length as this function is to be minimised
 
The cost function is expected to look like a smooth function with spikes induced by the added penalties, therefore the function is not Lipschitz continuous [1] this impedes the convergence of most global optimisation methods. Therefore the optimisation is done with Basin-hopping. Basin-hopping is essentially a simple quasi-random optimisation method. The method works by guessing a random point, this random point is checked to lie between the set bounds. After the guess is validated the local optimisation method is applied; the trust-constraint optimiser, since it was found to be the most stable. The combination of these two optimisation algorithms is chosen for their ability to find the global minimum of the applied cost function in a time-efficient manner and their compliance with the model.

Finally, after an optimum is found the values for the parameters are implemented in the variables and equations. Thereafter, the following plots are made with these optimised values: summation of the potential energy to the compression, summation of the force to the compression, force-compression, stiffness-compression and the linkage model of the geometry.

[1] Wikipedia contributors, “Lipschitz continuity,” Wikipedia, Jun. 04, 2024. https://en.wikipedia.org/wiki/Lipschitz_continuity

3.3: The main thing a user can alter, are the initial values, so the user can experiment with the code. These can be found in the second line of the second cell. Further, values of stepsize (5th line, second cell), bounds of the optimisable parameters (lines 8-12, second cell), as well as the type of optimiser within basinhopping (1st line, 12th cell) can be changed. However, this will drastically alter the code's behaviour. This is fully at the risk of the user. It is recommended to have a copy of the original code before altering the code.

3.4: the code, named "Silicone optimisation", can be used for the optimisation when silicone bulk is preferred, the other code, named "TPC optimisation", can be used for the optimisation when Thermoplastic copolymer bulk is preferred.


Note: In this code, "linear spring" and "tension bar" are interchangeably used. In the research paper, it is referred to as "tension bar".

## 4. Contributing <a name="contributing"></a>

4.1: This code can be used at your own risk. If this code is used to conduct further research or to be used for commercial purposes, it must be reported to one or more authors of the code.

## 5. Acknowledgements <a name="acknowledgements"></a>

We would like to express our gratitude to our supervisor Freek Broeren for his invaluable contribution throughout this research endeavour.


Authors:

Tom Krom, BSc student Mechanical Engineering at TU Delft (studentnumber 5635683): www.linkedin.com/in/tom-krom-a19831253/

Thomas Paddeu, BSc student Mechanical Engineering at TU Delft (studentnumber 5607663): www.linkedin.com/in/thomaspaddeu/

Luc Pijnenburg, BSc student Mechanical Engineering at TU Delft (studentnumber 5593344): www.linkedin.com/in/LucPijnenburg/

Florian Simor, BSc student Mechanical Engineering at TU Delft (studentnumber 5628733): www.linkedin.com/in/florian-simor/

------------------------------------------------------------------------
