Download Link: https://assignmentchef.com/product/solved-comp1130-assignment-2
<br>
Chapter 1

<h1><a name="_Toc17794"></a>Introduction</h1>

<h2><a name="_Toc17795"></a>1.1     Description of the program</h2>

It is an human-computer interaction program and can be divided into two parts. The first part is Conway’s Game of Life. The second part is the custom cellular automaton. Users could manipulate these two automata by keyboards. They can choose to evolve the cells once or as many times as given.

<h2><a name="_Toc17796"></a>1.2     Keyboards binding of the program</h2>

In this program, there are several KeyPress Event. So, pressing a specific key will trigger featured functionality. Pressing”.” will evolve the cells to the next generation. “&lt;Spacebar&gt;” is used for evolving multiple generations of the automata. Keyboard “+” or “-” can increase or decrease the number of generations that &lt;Spacebar&gt; can evolve. Clicking “1” or “2” can load different test patterns of each automaton. Pressing “B” can switch to BZ (Belousov-Zhabotinsky) automaton and “C” can change to Conway’s Game of

Life.

Chapter 2

<h1><a name="_Toc17797"></a>Contents</h1>

<h2><a name="_Toc17798"></a>2.1     Program design</h2>

Design of the program can be divided into four parts, which are “Data declarations”, “Functions”, “Algorithms” and “Integration of the program”.

<h3><a name="_Toc17799"></a>2.1.1    Data declarations</h3>

Before writing functions, we have to consider datatypes that the program depends on.

We need to define datatypes of the possible states of a cell, which are Conway and BZ. We can consider the number of states for each automaton and give each of them a distinguishing constructor.

<h3><a name="_Toc17800"></a>2.1.2    Functions</h3>

There are some significant functions which combine others to fulfill their functionalities.

The allCoords function is defined by using the helper function gridList.

This helper function is written by using another helper function combinationX. So, the allCoords can list all GridCoord in the given width and height.

The functionality of nextGenConway is achieved by using the function newConways, in which function newConway is used recursively. The newConway is defined by using changeState, countaroundAlive, get and deleteMaybe functions. The state of the given cell will change according to the number of alive cells around and its current cellular state. The get function helps extract the state of the chosen cell. The countaroundAlive is written by applying countAliveList and stateInNeigh. It can count the number of ALive cells in neighbours of the given cell. When inputting a coordinate in stateInNeigh, it returns a list of Maybe Conway. Then, use countAliveList to count the number of Just Alive in that list.

In terms of nextGenBZ, it is defined by using newBZs, which is written by applying newBZ recursively. Functions changeBZ, sumEnergyNeigh, deleteMaybe and get are combined to achieve the functionality of newBZ. Function sumEnergyNeigh integrates sumEnergy and stateInNeigh so it can obtain the total energy level around a central cell. Function sumEnergy uses energyLable in recursion and can sum the total energy level in a list of Maybe BZ.

There is one technique used in defining functions to reduce code redundancy. The functions like get, deleteMaybe and stateInNeigh are written in parametric polymorphism.

<h3><a name="_Toc17801"></a>2.1.3    Algorithms</h3>

I will explain the algorithm for Conway’s Game of Life first. Each central cell has eight neighbours. What it will be like depends on its current state and the states of its neighbours. Assume there are exactly three Alive cells around the central cell, then it will be Alive whatever it was initially. If there are exactly two Alive neighbour cells, then the state of the central cell remains the same. All other numbers of Alive neighbour cells will lead to Dead.

Then, I will introduce the algorithm for the BZ automaton. BZ reaction is one famous chemical reaction for its particular shape. How the reaction looks like can be accessed <a href="https://www.rit.edu/spotlights/chemical-waves-belousov-zhabotinsky-bz-reaction">here</a>. The ten varied states of the cells represent different energy levels. We will sum the energy levels of the neighbour cells. When the central cell is S, and if the sum is greater or equal to three then it will become A1. Otherwise, the state of the central cell will change from A1 to E4 step-wisely without any other input (energy level increases gradually). When it reaches E4, it will transform back to S. For example, when the central cell is A5, then it will become E1 in the next generation.

<h3><a name="_Toc17802"></a>2.1.4    Integration of the program</h3>

There are two steps when the program is trying to evaluate what the next generation will be like for each automaton.

In terms of integrating the whole program, we need to investigate functions in

App.hs. All the useful information is stored in Model, for example,

CellGrid. The function applyEvent takes AppEvent and Model as inputs. Different AppEvent will lead to different changes on Model. They are fulfilled mostly by the functions defined in Automata.hs. For example, Step will trigger nextGenConway or nextGenBZ (depends on current

CellGrid). Another function is called parseEvent, it is essential for the

I/O functionality. It takes Model and Event as inputs. When pressing defined keys, it will trigger corresponding AppEvent and cause changes in the Model.

Then, we need to draw our current Grid Conway or Grid BZ in the

CodeWorld. For the first step, we need to extract Grid Conway or Grid BZ from Model. Then, convert them into Pictures by renderConway and renderBZ. Eventually, draw it in Blank Canvas by render function in App.hs.

<h2><a name="_Toc17803"></a>2.2     Assumptions</h2>

One assumption I made is that the switching between the two automata is done by pressing two different keys. Because there is no functionality of displaying the automaton being used. Therefore, it is confusing to users. So, I decided to bind each switching with one specific key, in this case, Conway’s Game of Life with “C” and BZ automaton with “B”.

<h2><a name="_Toc17804"></a>2.3    Testing</h2>

The testing of the program can be divided into two parts.

The first part is testing the program holistically. Run Cabal v2-run automata in the terminal to load the program. Then, check whether we can change between two automata by clicking “B” and “C”. Next, check if pressing on the cells can change their states. Test whether clicking “1” or “2” can load two test patterns for each automaton. Also, test if “+” and “-” could modify the jump size of evolveConway and evolveBZ. Finally, we try to evolve each automaton for different generations and check them with our expectation.

The second part is to run AutomataTest.hs by running cabal v2-test in the terminal. All important functions in Automata.hs have been covered in the tests. There are eighteen tests in total and details can found in the test file. Almost all possible cases have been tested for each function. So that the possibility for functions to work improperly is very low.

Besides, we can also load codes in GHCI by running cabal v2-repl comp1100-assignment2 in the terminal. Then, import any module we defined. For example, type import Automata in GHCI. Then we can check each individual functions in Automata.hs by giving them some inputs.

The program can be compiled without error or warning. All the above tests pass and functions work properly.

<h2><a name="_Toc17805"></a>2.4     Inspiration</h2>

The algorithm for the BZ automaton was inspired by an article released by Cornell University. When I access the <a href="http://instruct1.cit.cornell.edu/courses/bionb441/CA/">original</a> <a href="http://instruct1.cit.cornell.edu/courses/bionb441/CA/">webpage</a> on 1st, May 2020, the contents cannot be found. But I discovered the saved <a href="http://read.pudn.com/downloads657/sourcecode/others/2670100/CA%2Bmatlab/CA%20matlab/CA.htm__.htm">HTML</a> <a href="http://read.pudn.com/downloads657/sourcecode/others/2670100/CA%2Bmatlab/CA%20matlab/CA.htm__.htm">file</a> of it. The algorithm of BZ automaton comes from the “BZ reaction or heart”.

<h2><a name="_Toc17806"></a>2.5     Change on the program</h2>

I made two changes in my program to optimize it.

The first one is that when I tried to compile the program in GHCI, I found one warning in Testing.hs. It was caused by the redundant import of the CodeWorld. So, I decided to add a pair of brackets. It refers that we haven’t used any individual function from the CodeWorld. Then, the warning disappeared.

The second one is that I tried to simulate the fluorescence effect in the BZ automaton. But the texts at the upper-left corner will become invisible because there is a large area of black rectangles. So, I change the text colour orange.

Chapter 3

<h1><a name="_Toc17807"></a>Reflection</h1>

<h2><a name="_Toc17808"></a>3.1     Conceptual and technical issues</h2>

One technical issue happened when I was trying to run AutomataTest.hs. After I ran cabal v2-test in the terminal, it said that there was no instance for Eq. So, I check my Automata.hs file. I found we need to consider the typeclass of certain datatypes. Because the function type of assertEqual has the constrains of (Eq a, Show a). So, the datatypes we define should include deriving (Show, Eq), or there will be some errors when we try to run our tests.

Another technical issue happened when I was defining nextGenConway and nextGenBZ functions. It is extremely challenging to write them in a single function definition because of their complexity. So, I decided to use helper functions to simplify both coding and conceptual complexity. I sliced problems into several sub-problems. Each helper function solves single sub-problem and then integrate them in the main function. Besides, it will be much easier for programmers to fix the errors if we use several helper functions.

Code redundancy was also one issue happened. In the beginning, I wrote functions with specified datatype. For example, in stateInNeigh, it initially worked only for Conway. When I move onto Task 3, I found there were functions can be applied in both Conway’s Game of Life and BZ automaton. So, I rewrote them in parametric polymorphism and this made my code simpler.

<h2><a name="_Toc17809"></a>3.2     Something to do differently next time</h2>

If I have more time and can show my creativity. I would like to import a new functionality. It can randomly generate test patterns with random scale and random list. Then, bind this functionality to a keyboard Event. Each time this key is pressed, the program will load random test patterns in Model.

I will also use some higher order functions to reduce the complexity of my code. For example, use foldr or foldl functions to replace recursions if possible.

<h2><a name="_Toc17810"></a>3.3     Collaboration with others</h2>

When I was doing Task 1, I stuck on allCoords. Then, I discussed it with

Yiran Wang (u7079256). However, we did not come up with anything useful. Then, I studied the previous labs again and found a similar function exercise in the extension1 of Lab05. After that, I successfully defined my allCoords function.

Chapter 4

<h1><a name="_Toc17811"></a>References</h1>

<ul>

 <li>Kingston, T. (2015). Chemical waves in a Belousov-Zhabotinsky (BZ) Reaction. Retrieved on 1 May 2020 from: <a href="https://www.rit.edu/spotlights/chemical-waves-belousov-zhabotinsky-bz-reaction">https:</a>//www.rit.edu/spotlights/chemical -waves-belousov-zhabotinsky-bz-reaction</li>

 <li>Cornell University (2006). Cellular Automata in Matlab. Original URL: <a href="https://courses.cit.cornell.edu/bionb441/CA/">https://courses.cit.cornell.edu/bionb441/CA/</a> (invalid)</li>

 <li>Cornell University (2006). Cellular Automata in Matlab. Retrieved on 1 May</li>

</ul>

2020 from: <a href="http://read.pudn.com/downloads657/sourcecode/others/2670100/CA%2Bmatlab/CA%20matlab/CA.htm__.htm">http://read.pudn.com/downloads657/so</a>urcecode/others/2670

100/CA%2Bmatlab/CA%20matlab/CA.htm__.htm