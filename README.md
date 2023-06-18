# Compensation of Accounting Entries
 This code implements an automatic compensation system for financial transactions.
Automatic Compensation Code README
This code implements an automatic compensation system for financial transactions. The compensation is performed based on a grouping criterion defined by the "classification code" column in a CSV input file.

# Requirements
The code requires the following Python libraries:

pandas
pulp
multiprocessing
os
time
Make sure you have these libraries installed before running the code.

# File Structure
The code assumes the following file structure in the working directory:

entries.csv: Input CSV file that contains the financial transaction data. It should have the columns credits, debits, classification code, reference, document, and date.

result.csv: Output CSV file where the compensation results will be stored.

# Code Functionality
The code performs the following steps:

Loads the financial transaction data from the entries.csv file into a DataFrame using the pandas library.

Identifies the distinct classification codes present in the classification code column to determine the grouping criteria.

Creates an empty DataFrame called resultados to store the compensation results.

Uses the multiprocessing library to perform compensation in parallel for each classification code found. This improves performance by leveraging multiple processors.

Within the compensation(c, df) function, filters the financial transactions that correspond to the current classification code. The necessary coefficients are extracted to solve the optimization problem.

Defines the decision variables and formulates the optimization problem using the pulp library. The objective is to maximize the sum of credits while ensuring that the sum of debits equals the sum of credits.

The optimization problem is solved with a time limit of 60 seconds using the PULP_CBC_CMD solving method.

If the time limit is reached, the process is terminated, and the next classification code is processed.

The optimal solution is added to the resultados DataFrame, filtering the rows where the variables x or y have a value of 1.

Upon finishing the processing of all classification codes, the contents of resultados are written to the result.csv file in CSV format.

The total execution time in seconds is printed.

# Execution
To run the code, make sure you have the entries.csv and result.csv files in the same folder as the code file. Then, simply execute the code and observe the results in the result.csv file. The execution time will be displayed in the console.

# Mathematical Problem Description
The mathematical problem behind the code is the well-known "Subset Sum Problem." Given a set of numbers (in this case, the credits and debits of financial transactions), the goal is to find a subset whose sum matches a target value (in this case, the total credits).

In the code, the Subset Sum Problem is formulated as a binary integer linear programming problem. The decision variables, represented by the variables x and y, determine whether a transaction is included in the subset or not. The objective function maximizes the sum of credits, while the constraint ensures that the sum of debits equals the sum of credits.

The code uses the PuLP library to solve the Subset Sum Problem efficiently, finding the optimal combination of transactions that compensates the maximum amount while maintaining balance between credits and debits.

Automating the compensation process using the Subset Sum approach allows for an efficient and systematic way to determine the best subset of transactions to achieve balance in financial operations, saving time and resources for organizations dealing with large amounts of transactional data.

Enjoy using the automatic compensation system for your financial transactions!
