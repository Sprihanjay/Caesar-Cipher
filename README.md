# Caesar's Cipher
Encoding Plain Text to Cipher and Decoding it


In this programming assignment, you will develop Python programs to encode plain text into cipher text using Caesar's Cipher method ([Wikipedia](https://en.wikipedia.org/wiki/Caesar_cipher)) as well as crack the code using frequency patterns in the English language. We shall encode only lower-case letters, a-z, and leave all other letters and characters as is.

1.  **Encoding:** You should write the following function:
    
    def encode(n,s):
      # this function takes as input n, the shift factor and
      # plain text s and returns the encoded string.
      ???
    
2.  **Cracking the code:** Cracking the code is relatively straightforward using frequency analysis and a bit of statistics. From the analysis of normal English text usage, the following frequency distribution of the individual letters a-z is available for us to use:
    
    def table_from_corpus():
      return [8.1, 1.5, 2.8, 4.2, 12.7, 2.2, 2.0, 6.1, 7.0,
              0.2, 0.8, 4.0, 2.4, 6.7,  7.5, 1.9, 0.1, 6.0,
              6.3, 9.0, 2.8, 1.0, 2.4,  0.2, 2.0, 0.1]
    
    This function, when called, will return a list of 26 frequencies, each expressed as a percentage of overall occurrence for the letters a thru z. For example, in normal English usage, the letter a appears 8.1% of the time, the letter e appears 12.7% of the time, etc. The method to crack the code will involve the following steps:
    -   Determine the frequencies of a-z in the cipher text and store in variable table_from_cipher_text. Here are functions that would be useful for this part:
        
        def count(c,s):
          ## This functions takes as input a character c and a string s and returns the 
          ## the number of times c appears in s
          ???
        
        def num_lower_case(s):
          ## This function takes as input a string s and returns the
          ## number of lower-case letters in s
          ???
        
        def frequencies(s):
          ## This function takes as input a string s and returns the
          ## frequency list for s, containing 26 percentages, one for
          ## each lower-case letter. The percentage should be taken
          ## over the number of lower-case letters in s.
          ???
        
    -   Write a function that determines the Chi-Square statistic by comparing the two frequency distributions, defined by the following formula:
        
        ![](https://tinman.cs.gsu.edu/~raj/1301/f22/p3/chisqr.png)
        
        where os is the observed frequency list obtained from the cipher text and es is the estimated frequency list obtained from the analysis of normal English usage. Write the following function that will compute the chi-square statistic for os and es.
        
        def chisqr(os,es):
          ## returns the chi-square statistic for os and es
          ???
        
    -   By rotating the observed frequency table by different positions (0 to 25), you can get 26 different versions of the frequency table, each corresponding to one of the 26 shift factors that could have been used to encode. The table with the "least" value for the chi-square statistic will correspond to the most likely shift factor that was used to encode. You can then use this shift factor to "crack" the code! Here are few functions to write to implement this part:
        
        def rotate(n,xs):
          ## rotates list xs by n positions
          ???
        
        def chisquare_statistic(os,es):
          ## This computes 26 ch-square statistics in a list, one for each 
          ## list obtained by rotating os by n = 0 to 25.
          ???
        
    -   Finally, write the following function that returns the "cracked" text:
        
        def crack(s):
          # This function takes as input a coded text and returns the plain text
          # for the coded text
          ???
        
        The main function is given below:
        
        def main():
          while True:
            plain = input("\nEnter plain text: ")
            if plain == "exit":
              break
            shift = random.randint(2,25)
            cipher = encode(shift,plain)
            print("Coded text: ",cipher)
            recovered = crack(cipher)
            print("Cracked text: ",recovered)
        
        main() 
        

A sample run of the program to test encoding and cracking the code is shown below:

Mac-mini:01-cipher raj$ python3 Cipher.py 

Enter plain text: hello, how are you
Coded text:  czggj, cjr vmz tjp
Cracked text:  hello, how are you

Enter plain text: what is the time?
Coded text:  grkd sc dro dswo?
Cracked text:  what is the time?

Enter plain text: What is the time, Sam?
Coded text:  Wvoh wg hvs hwas, Soa?
Cracked text:  What is the time, Sam?

Enter plain text: exit
Mac-mini:01-cipher raj$
