// Part 1

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
