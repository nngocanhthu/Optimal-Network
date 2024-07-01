# Optimal Fulfillment Centers Network

## 1. Objective
This project aims to optimize the fulfillment center network using Linear Programming (LP) and the Facility Location Problem Model, focusing on minimizing operational costs and shipping expenses while meeting customer demand.

## 2. Data Description
The dataset comprises 6 dataframes:
1. **Fulfillment centers**: Potential locations with associated regions and subregions.
2. **Customers**: Demand profiles for each location.
3. **Standard distribution**: Average distribution rates for standard package weights.
4. **Express distribution**: Average distribution rates for express package weights.
5. **Standard rate**: Shipping costs for standard packages.
6. **Express rate**: Shipping costs for express packages.

## 3. Tools
For this project, Python was used along with the following libraries:
- **pandas**: Data manipulation and analysis.
- **numpy**: Numerical computations and array operations.
- **gurobipy**: Optimization solver for LP models.

In additions, Power BI was used to visualize the final outcome.

## 4. Mathematical Model
The project employs a modified Facility Location Problem model [(Holmberg, Rönnqvist & Yuan, 1999)](https://doi.org/10.1016/S0377-2217(98)00008-3) with additional constraints:
- Limited to a maximum of 10 fulfillment centers.
- Ensures each subregion has at least one operational fulfillment center.

The detailed model is as follows:

With $I$ as the collective of n potetial locations for fulfillment centers, $J$ as the collective of n customers groups, $R$ is the collective of region, $IR_r$ is the collective of potential location in region $r$, $T$ is the collective of subregions, and $SR_t$ is the collective of potential locations for fulfillment centers in subregion $ t$. The modified mathematical model is described as below:

Parameters:

$f_i$ is the cost of using facility i in one year.

$c_{ij}$ is the shipping cost from fulfillment center i to customer j per one unit.

$l_{ij}$ is the lead time from fulfillment center i to customer j per one unit.

$d_j$ is the demand of customer j in one year.

$b_i$ is the capacity of fulfillment center i in one year.

Decision variables:

$y_i=1$ if fulfillment center i opens, 0 otherwise.

$x_{ij}=1$ if fulfillment center i serves customer (group) j, 0 otherwise.

Considering the long-term effect, I do not include the fixed cost of opening the fulfillment center into the model. The objective function is to minimize the total effect of operational cost & shipping cost to serve all the demand in one year.

Objective function:

$v^* = \sum_{i=1}^{n} y_i\cdot f_i + \sum_{i=1}^{n} \sum_{j=1}^{m} d_j\cdot c_{ij}\cdot x_{ij}$

Constraints:

(1) Customer demand served by a certain facility does not exceed its capacity

$\sum_{j=1}^{m}d_j\cdot x_{ij} \leq b_i\cdot y_i \text{ } \forall i \in I$

(2) A customer is served by a single source

$\sum_{i=1}^{n}x_{ij} = 1 \text{ } \forall j \in J$

(3) Only 10 fulfillment centers will be opened at max

$\sum_{i=1}^{n} y_i \leq 10$

(4) Each subregion has at least 1 fulfillment center

$\sum_{i \in SR_t} y_i \geq 1 \text{ } \forall t \in T$

## 5. Outcome

The graph below illustrates the distribution of fulfillment centers, where the bubble size corresponds to the customer demand that each facility is designed to accommodate.
