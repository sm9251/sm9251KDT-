// Part 1

import java.util.*;
import java.io.*;

// represents a Word and its associated vector in the K-D tree

class Word {
    String word;  // The word/identifier
    float[] vector;  //  vector of word

    // Initialize a Word object with a word and vector
    public Word(String word, float[] vector) {
        this.word = word; // set
        this.vector = vector; // pointers
    }
}

// KTDNode class
class KTDNode {
    Word word;  // nodes will store a Word object 
    KTDNode left, right;  // Left/Right child pointers 

    // Constructor: Initializes a KTDNode a Word
    // Node has no childs
    public KTDNode(Word word) {
        this.word = word;
        this.left = null;
        this.right = null;
    }
}
