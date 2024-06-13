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

3.2: The main thing a user can alter, are the initial values, so the user can experiment with the code. These can be found in the second line of the second cell. Further, values of stepsize (5th line, second cell), bounds of the optimisable parameters (lines 8-12, second cell), as well as the type of optimiser within basinhopping (1st line, 12th cell) can be changed. However, this will drastically alter the code's behaviour. This is fully at the risk of the user. It is recommended to have a copy of the original code before altering the code.

3.3: the code, named "Silicone optimisation", can be used for the optimisation when silicone bulk is preferred, the other code, named "TPC optimisation", can be used for the optimisation when Thermoplastic copolymer bulk is preferred.


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
