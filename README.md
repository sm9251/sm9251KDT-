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

// KDT class, represent KD tree
class KDT {
    KTDNode root;  // root of tree
    int d;  // d is n of dimensions 

    // Constructor: Initializes and empty K-D tree 
    // with an specific d
    public KDT(int k) {
        this.k = k;
        this.root = null;  
    }

    // Uses Recursion to build 
    // a K-D tree using list of Word objects
    public KTDNode build(List<Word> words, int depth) {
        // Base case: if list is empty, return null, 
        if (words.isEmpty()) return null;

        // Uses % to generate a number associated to an axis
        // for each level of the recursion
        // Words will be assigned to a different axis
        int axis = depth % d;  

        // Sort a list of the words of the axis used
        words.sort((w1, w2) -> Float.compare(w1.vector[axis], w2.vector[axis]));

        // Get median of list and 
        // Select the word to be
        // the word in the new node
        int medIndex = words.size() / 2;
        Word medWord = words.get(medIndex);

        // Create the node
        KTDNode node = new KTDNode(medWord);

        // Use recursion to build the left and right subtrees
        // Where the words before the median go to the left subtree
        // and the rest to the right 
        node.left = build(words.subList(0, medIndex), depth + 1);
        node.right = build(words.subList(medIndex + 1, words.size()), depth + 1);

        // Return current node 
        return node;
    }


