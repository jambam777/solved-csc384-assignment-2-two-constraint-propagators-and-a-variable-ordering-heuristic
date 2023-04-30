Download Link: https://assignmentchef.com/product/solved-csc384-assignment-2-two-constraint-propagators-and-a-variable-ordering-heuristic
<br>
There are two parts to this assignment

<ol>

 <li>the implementation of two constraint propagators and a variable ordering heuristic – a Forward Checking constraint propagator, a Generalized Arc Consistence (GAC) constraint propagator, and the Minimum Remaining Values (MRV) heuristic,</li>

 <li>the encoding of two different CSP models to solve the logic puzzle, Futoshiki, as described below. In one model you will use only binary not-equal constraints, while in the other model you will use 9-ary all-different constraints in addition to binary not-equal constraints.</li>

</ol>

What is supplied:

<ul>

 <li>py – class definitions for the python objects Constraint, Variable, and BT.</li>

 <li>py – starter code for the implementation of your two propagators and variable ordering heuristic. You will modify this file with the addition of three new procedures prop FC, prop GAC, and ord mrv, to realize Forward Checking, GAC and MRV, respectively.</li>

 <li>csp sample run.py – This file contains a sample implementation of two CSP problems.</li>

 <li>futoshiki csp.py – starter code for the two Futoshiki CSP models.</li>

 <li>propagators test.py for testing your code for FC and GAC.</li>

</ul>

<h1>Futoshiki Formal Description</h1>

The Futoshiki puzzle<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> has the following formal description:

<ul>

 <li>The puzzle is played on a grid <em>board </em>with dimensions <em>n </em>rows by <em>n </em> The board is always a square.</li>

 <li>The board has <em>n</em><sup>2 </sup>spaces on it, where each space may take a value between 1 and <em>n </em> You will use a list of lists in order to represent assigned values to the variables on this grid.</li>

 <li>The start state of the puzzle may have some spaces already filled in.</li>

</ul>

Figure 1: An example of a 5×5 Futoshiki grid in its initial state (left) and solution (right).

<ul>

 <li>Additionally, the starting board may have some <em>inequality constraints </em>specified between some of the spaces. These inequality constraints will <em>only </em>apply to two cells that are horizontally adjacent to one another, i.e. the constraints will only apply to rows and not columns. If there is <em>no </em>inequality constraint between two adjacent cells, this will be represented with a dot (i.e., with a ‘.’). For example, consider this 2 x 2 board: [[0<em>,&lt;,</em>0<em>,</em>]<em>,</em>[0<em>,.,</em>0]]. The assignments [[1<em>,&lt;,</em>2<em>,</em>]<em>,</em>[2<em>,.,</em>1]] would satisfy the inequality constraint.</li>

 <li>A puzzle is <em>solved </em>if:

  <ul>

   <li>Every space on the board is given one value between 1 and <em>n </em></li>

   <li>All specified inequality constraints are satisfied.</li>

   <li>No row contains more than one of the same number.</li>

   <li>No column contains more than one of the same number.</li>

  </ul></li>

</ul>

An example of a Futoshiki instance and its solution are depicted in figure 1. You can also play Futoshiki online<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a> but column inequality constraints might be included.

<h1>Question 1: Propagators</h1>

You will implement python functions to realize two constraint propagators – a Forward Checking constraint propagator and a Generalized Arc Consistence (GAC) constraint propagator. These propagators are briefly described below. The files cspbase.py and propagators.py provide the complete input/output specification of the functions you are to implement. In all cases, the CSP object is used to access variables and constraints of the problem, via methods found in cspbase.py.

Brief implementation description:               A Propagator Function takes as input a CSP object csp and (op-

tionally) a variable newVar. The CSP object is used to access the variables and constraints of the problem (via methods found in cspbase.py). A propagator function returns a tuple of (bool,list) where bool is False if and only if a dead-end is found, and list is a list of (Variable, value) tuples that have been pruned by the propagator. ord mrv takes a CSP object csp as input, and returns a Variable object var. You must implement: You must implement:.

prop FC (worth 25/100 marks)

A propagator function that propagates according to the Forward Checking (FC) algorithm that check constraints that have <em>exactly one uninstantiated variable in their scope</em>, and prune appropriately.

If newVar is None, forward check all constraints. Else, if newVar=var only check constraints containing newVar.

prop GAC (worth 25/100 marks)

A propagator function that propagates according to the Generalized Arc Consistency (GAC) algorithm, as covered in lecture. If newVar is None, run GAC on all constraints. Else, if newVar=var only check constraints containing newVar.

ord mrv (worth 10/100 marks)

A variable ordering heuristic that chooses the next variable to be assigned according to the Minimum Remaining Values (MRV) heuristic. ord mrv returns the variable with the most constrained current domain (i.e., the variable with the fewest legal values).

<h1>Question 2: Futoshiki Models</h1>

You will implement two different CSP encodings to solve the logic puzzle, Futoshiki. In one model you will use only binary not-equal constraints, while in the other model you will use n-ary all-different constraints in addition to binary not-equal constraints. These CSP models are briefly described below. The file futoshiki csp.py provides the complete input/output specification for the two CSP encodings you are to implement.

The correct implementation of each encoding is worth 20/100 marks.

Brief implementation description:           A Futoshiki Model takes as input a Futoshiki board, and returns a

CSP object, consisting of a variable corresponding to each cell of the board. The variable domain of that cell is {1<em>,…,n</em>} if the board is unfilled at that position, and equal to <em>i </em>if the board has a fixed number <em>i </em>at that cell. All appropriate constraints will be added to the board as well. You must implement:

futoshiki csp model 1 A model built using only binary not equal constraints for the row and column constraints, and binary inequality constraints.

futoshiki csp model 2 A model built using <em>n</em>-ary all-different constraints for the row and column constraints, and binary inequality constraints.

Caveat: The Futoshiki CSP models you will construct can be space expensive, especially for constraints over many variables, (e.g., those contained in the second Futoshiki CSP model). <em>HINT: Also be mindful of the time complexity of your methods for identifying satisfying tuples, especially when coding the second Futoshiki CSP model.</em>

<a href="#_ftnref1" name="_ftn1">[1]</a> https://en.wikipedia.org/wiki/Futoshiki

<a href="#_ftnref2" name="_ftn2">[2]</a> https://www.futoshiki.org/