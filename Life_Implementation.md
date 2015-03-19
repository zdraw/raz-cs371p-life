We are creating the game of Life which is a simple simulation of cell automation.

# Introduction #

The purpose of this assignment is to create a Life board that can take Cell objects or Handles to those Cells. This involves creating a Handle class, Abstract class, and children of the Abstract class.


# Details #

We have 5 main classes in the project.
  * A Life`<T>` board
  * A ConwayCell class
  * A FredkinCell class
  * An AbstractCell class
  * A Cell class

The Life`<T>` board is created with a given number of rows and columns and populated with T objects. The generation is originally at 0 and the Life object can call a method that increases it by one. In doing so Life makes two passes through it's board. The first pass finds the number of living neighbors for each cell. The second pass then updates each cell based on those numbers. This gives the generation increase some air of concurrency. The board can set spaces to be a given cell. We also overloaded << so that we just say cout << Life`<T>` to print out the current state of the board, the generation, and current population.

The AbstractCell class is a basic pure class that ConwayCell and FredkinCell will derive from. It contains two private variables, _living and_neighbors. There is a method to return the _living variable and the derived xCell classes will need to define their own clone function, update function, and addNeighbor function._

The ConwayCell class derives from Abstract cell. The footprint of the class is no different than it's parent, but it has different member functions. Clone returns a new ConwayCell object. Since Conway cell have neighbors in a circle around the cell, the addNeighbor function with recalculate its neighbor variable based on that circle. When a Conway Cell updates with 3 neighbors, it becomes/stays living. Otherwise the Conway cell changes it's _living variable to false._

The FredkinCell class derives from Abstract cell. The footprint of the class is the same as AbstractCell with an added _age variable. Clone returns a new FredkinCell object. It defines neighbors as only directly above, below, left, and right so it's addNeighbors function reflects that.  When a FredkinCell updates, if it has an even number of neighbors, if becomes dead. Otherwise it becomes living and it's age increases._

The Cell class is a handle containing an AbstractCell object so it can hold either a Conway or Fredkin cell. It has a default constructor to set the pointer to null. The copy constructor copies the pointer if it's null otherwise it clones the other Cell. The destructor deletes the pointer if it's not null. The assignment operator swaps the pointers of the lhs and rhs. The Cell class also implements the public functions of AbstractCell which are living(), addNeighbor(int row, int col), and update().

Using these 5 classes we were able to create our simulator. New xCells can be created if they derive from AbstractCell and define the necessary functions.