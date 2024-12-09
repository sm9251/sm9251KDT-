// Part 1

import java.util.*;
import java.io.*;

// represents a Word and its associated vector in the K-D tree

class Word {
    String word;  // The word/identifier
    float[] vector;  //  vector of word (Array of floats)

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
    int d;  // d is the number of dimensions
    
    // Constructor: Initializes an empty K-D tree 
    // with a specific dimensionality d
    public KDT(int d) {
        this.d = d;  // Assign the d value here
        this.root = null;  // root is initially null
    }

    // Uses recursion to build a K-D tree using list of Word objects
    public KTDNode build(List<Word> words, int depth) {
        if (words.isEmpty()) return null;  // Base case: empty list means no node

        // Calculate the axis based on depth (recursive traversal)
        int axis = depth % d;  

        // Sort words by the value of the current axis
        words.sort((w1, w2) -> Float.compare(w1.vector[axis], w2.vector[axis]));

        // Find the median word (the pivot for this level of the tree)
        int medIndex = words.size() / 2;
        Word medWord = words.get(medIndex);

        // Create the node and recursively build subtrees
        KTDNode node = new KTDNode(medWord);
        node.left = build(words.subList(0, medIndex), depth + 1);
        node.right = build(words.subList(medIndex + 1, words.size()), depth + 1);

        return node;
    }

    // Print tree in order to validate structure
    public void printTree(KTDNode node) {
        if (node != null) {
            System.out.println(node.word.word + " " + Arrays.toString(node.word.vector)); // print word and vector
            printTree(node.left);  // Left subtree
            printTree(node.right); // Right subtree
        }
    }


// Reads data to create a list of words from the file
public static List<Word> readData(String filePath, KDT kdTree) throws IOException {
    // Create BufferedReader 
    BufferedReader reader = new BufferedReader(new FileReader(filePath));
    
    // List to store Word objects 
    List<Word> words = new ArrayList<>();

    // Read first line to get dimensions and n of words
    String line = reader.readLine();  // Reads first line
    String[] firstLine = line.split(" ");  // Split first line into array
    // of substrings

    // Read rest of lines
    while ((line = reader.readLine()) != null) {
        // Split the lines 
        String[] parts = line.split(" "); 

        // first part of line is the word 
        String word = parts[0];  

        // array to hold the vector. 
        float[] vector = new float[kdTree.d];  // length determined by d from KDT 
        
        // Fill the vector array with vectors from other parts
        for (int i = 1; i <= kdTree.d; i++) {
            // Convert strings in parts[i] to a float and store in vector array
            vector[i - 1] = Float.parseFloat(parts[i]);  
        }
        
        // Create Word object with parsed word and its vector 
        // then add it to the list
        words.add(new Word(word, vector));
    }

    reader.close();  // Close the reader when done reading the file
    
    // Return the list of Word objects
    return words;  
}
}

// Main function to run the K-D tree program
public static void main(String[] args) {
    // Check if exactly one argument is passed (the path to the input data file)
    if (args.length != 1) {
        System.err.println("Usage: java Kdnn <data-file>");
        return;  // Exit if incorrect number of arguments
    }

    try {
        // Assume we know the number of dimensions (30, for example), and pass it along to readData()
        int dimensions = 30; // This is the dimension 'd' we are working with
        // Read the input data file (the file passed as argument)
        List<Word> words = readData(args[0], dimensions);

        // Create a new K-D tree with the number of dimensions (e.g., 30)
        KDT kdTree = new KDT(dimensions);

        // Build the K-D tree using the list of words
        kdTree.root = kdTree.build(words, 0);  // Start building from the root with depth 0

        // Print the tree to validate that all the words are correctly inserted into the tree
        kdTree.printTree(kdTree.root);

    } catch (IOException e) {
        // Handle file reading errors (e.g., if the file doesn't exist or can't be opened)
        System.err.println("Error reading file: " + e.getMessage());
    }
}






