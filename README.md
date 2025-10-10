<h1>ExpNo 8 : Solve Cryptarithmetic Problem,a CSP(Constraint Satisfaction Problem) using Python</h1> 
<h3>Name:     MADHULEHA K          </h3>
<h3>Register Number/Staff Id:   212224060140    </h3>
<H3>Aim:</H3>
<p>
    To solve Cryptarithmetic Problem,a CSP(Constraint Satisfaction Problem) using Python
</p>
<h3>Procedure:</h3>
Input and Output
<br>Input:
This algorithm will take three words.
<br> B A S E<br>
    B A L L<br>
           ----------<br>
           G A M E S<br>

Output:
It will show which letter holds which number from 0 – 9.
For this case it is like this.

              B A S E                         2 4 6 1
              B A L L                         2 4 5 5
             ---------                       ---------
            G A M E S                       0 4 9 1 6
Algorithm
For this problem, we will define a node, which contains a letter and its corresponding values.<br>

isValid(nodeList, count, word1, word2, word3)<br>

Input − A list of nodes, the number of elements in the node list and three words.<br>

Output − True if the sum of the value for word1 and word2 is same as word3 value.<br>

Begin<br>
   m := 1<br>
   for each letter i from right to left of word1, do<br>
      ch := word1[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>
      val1 := val1 + (m * nodeList[j].value)<br>
      m := m * 10<br>
   done<br>

   m := 1<br>
   for each letter i from right to left of word2, do<br>
      ch := word2[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>

      val2 := val2 + (m * nodeList[j].value)
      m := m * 10
   done<br>

   m := 1<br>
   for each letter i from right to left of word3, do<br>
      ch := word3[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>

      val3 := val3 + (m * nodeList[j].value)
      m := m * 10
   done<br>

   if val3 = (val1 + val2), then<br>
      return true<br>
   return false<br>
End<br>
from itertools import permutations

# Function to check if a given assignment of letters to digits satisfies the equation
def is_valid(word1, word2, word3, mapping):
    # Convert each word to its numerical value using the mapping
    def word_to_number(word):
        return int(''.join(str(mapping[ch]) for ch in word))
    
    # Convert words to numbers
    num1 = word_to_number(word1)
    num2 = word_to_number(word2)
    num3 = word_to_number(word3)
    
    # Check if the sum holds true
    return num1 + num2 == num3

# Solve the cryptarithmetic puzzle
def solve_cryptarithmetic(word1, word2, word3):
    # Extract all unique characters
    letters = list(set(word1 + word2 + word3))
    
    # There are at most 10 unique digits (0-9)
    if len(letters) > 10:
        print("Too many unique letters (more than 10) — cannot solve.")
        return

    # Generate all possible assignments of digits 0–9 for these letters
    for perm in permutations(range(10), len(letters)):
        mapping = dict(zip(letters, perm))
        
        # Leading letters of any word cannot be 0
        if mapping[word1[0]] == 0 or mapping[word2[0]] == 0 or mapping[word3[0]] == 0:
            continue
        
        # Check if this mapping satisfies the equation
        if is_valid(word1, word2, word3, mapping):
            print("✅ Solution Found!")
            print()
            for ch in sorted(mapping.keys()):
                print(f"{ch} = {mapping[ch]}")
            print()
            print(f"{word1} = {''.join(str(mapping[ch]) for ch in word1)}")
            print(f"{word2} = {''.join(str(mapping[ch]) for ch in word2)}")
            print("-" * 25)
            print(f"{word3} = {''.join(str(mapping[ch]) for ch in word3)}")
            return mapping

    print("❌ No solution found.")

# -------------------------
# MAIN PROGRAM
# -------------------------
if __name__ == "__main__":
    print("=== Cryptarithmetic Problem Solver ===")
    print("Example 1: BASE + BALL = GAMES")
    solve_cryptarithmetic("BASE", "BALL", "GAMES")

    print("\nExample 2: SEND + MORE = MONEY")
    solve_cryptarithmetic("SEND", "MORE", "MONEY")

<hr>
<h2>Sample Input and Output:</h2>
SEND = 9567<br>
MORE = 1085<br>
<hr>
MONEY = 10652<br>
<hr>
<h2>Result:</h2>
<p> Thus a Cryptarithmetic Problem was solved using Python successfully</p>
