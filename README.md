Download Link: https://assignmentchef.com/product/solved-cs261-assignment-6-hash-table-implementation-and-concordance
<br>
There are three parts to this assignment. In the first two parts, you will complete the implementation of a <strong>hash map </strong>and a <strong>concordance program</strong>. In the third part, you will <strong>answer a number of questions </strong>using the concordance program.

<h1>Hash map</h1>

First complete the hash map implementation in hashMap.c. This hash map uses a table of buckets, each containing a linked list of hash links. Each hash link stores the key-value pair (string and integer in this case) and a pointer to the next link in the list. See hashMap.h and the accompanied drawing posted with this assignment for clarification. You must implement each function in hashMap.c with the // FIXME: implement comment.

At the top of hashMap.h you should see two macros: HASH_FUNCTION and MAX_TABLE_LOAD. You are free to change their definitions but know that the default values will be used when grading. HASH_FUNCTION is the name of the hash function you want to use. You will change this when answering the written part of the assignment. <strong>Make sure </strong>everywhere in your implementation to use HASH_FUNCTION(key) instead of directly calling a hash function. MAX_TABLE_LOAD is the table load threshold on which you should resize the table.

A number of tests for the hash map are included in tests.c. Each one of these test cases use several or all of the hash map functions, so don’t expect tests to pass until you implement all of them. Each test case is slightly more thorough than the one before it and there is a lot of redundancy to better ensure correctness. Use these tests to help you debug your hash map implementation. They will also help your TA grade your submission. You can build the tests with make tests or make and run them with ./tests.

<h1>Concordance</h1>

The concordance counts how many times each word occurs in a document. You will implement a concordance using the hash map implementation from the previous part. Each hash link in the table will store a word from the document as the key and the number of times the word appeared as the value. You must finish the concordance implementation in main.c.

You are provided with a function nextWord() which takes a FILE*, allocates memory for the next word in the file, and returns the word. If the end of the file is reached, nextWord() will return NULL. It is your job to open the file using fopen(), populate the concordance with the words, and close the file with fclose(). The file name to open should be given as a command line argument when running the program. It will

default to input1.txt if no file name is provided.

Your concordance code should loop over the words until the end of the file is reached, doing the following steps each iteration:

<ol>

 <li>Get the next word with getWord.</li>

 <li>If the word is already in the hash map, then increment its number of occurrences.</li>

 <li>Otherwise, put the word in the hash map with a count of 1.</li>

 <li>Free the word.</li>

</ol>

After processing the text file, print all words and occurrence counts in the hash map. Please print them in the format of the following example above the call to hashMapPrint():

best: 1 It: 2 was: 2 the: 2 of: 2 worst: 1 times: 2

You can build the program with make prog or make and run it with ./prog &lt;filename&gt;, where &lt;filename&gt; is the name of a text file like input1.txt.

<h1>Written</h1>

Submit a pdf or text file answering the following questions:

<ol>

 <li>Give an example of two words that would hash to the same value using hashFunction1 but would not using hashFunction2.</li>

 <li>Why does the above observation make hashFunction2 superior to hashFunction1?</li>

 <li>When you run your program on the same input file once with hashFunction1 and once with hashFunction2, is it possible for your hashMapSize function to return different values?</li>

 <li>When you run your program on the same input file once with hashFunction1 and once with hashFunction2, is it possible for your hashMapTableLoad function to return different values?</li>

 <li>When you run your program on the same input file once with hashFunction1 and once with hashFunction2, is it possible for your hashMapEmptyBuckets function to return different values?</li>

 <li>Is there any difference in the number of empty buckets when you change the table size from an even number like 1000 to a prime like 997?</li>

</ol>

<h1>Extra credit</h1>

There are a lot of uses for a hash map, and one of them is implementing a spell checker. All you need to get started is a dictionary, which is provided in dictionary.txt. In spellChecker.c you will find some code to get you started with the spell checker. It is fairly similar to the code in main.c.

You can build the program with make spellChecker.

FYI:

The spellchecker program flow should as following –




<ol>

 <li>The user types in a word</li>

 <li>Potential matches are outputted Like “Did you mean…?” etc</li>

 <li>Continue to prompt user for word until they type quit</li>

</ol>




The best way to implement a dictionary that’s used for a spellchecker would probably be to design it with that purpose in mind from the beginning, i.e. associating a similarity for each word to some base word (maybe “abcdefghijklmnopqrstuvwyz”) and then incorporating that into the hash function. There are better ways ( https://en.wikipedia.org/wiki/Levenshtein_distance)  to establish similarity than computing the cosine of the angle between two vectors (strings) to create a list of candidates and further winnowed that list according to substring comparisons.




So, I would say calculating the Levenshtein distance between the misspelled word and all strings in the dictionary, create 5/6 best candidates and print them as suggestion.