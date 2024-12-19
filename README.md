Classes:
Word: Stores a word and its associated vector. It has two attributes: a string to hold the word and an array of floats that will represent the words as vectors.
KTDNode: Represents a node. They contain a Word object with pointers to its left and right children. The constructor initializes a node with a Word and null children.
KDT: Represents a K-D tree. It depends on 6 methods: build, findNearestNeighbor, calculateHeight, readData, minimalHeight and squaredEuclideanDistance.
Kdnn: Is the “main” method. 
Test:

I used the two files provided to test the right functionality of the code. I also checked how long it took to run and looked at it multiple times to find parts of it that could be made more efficient. I also tested for edge cases like empty or invalid data files and trees with only one node, to ensure the program handles these situations correctly.








