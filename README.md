# Exp-11--Record-IMPLEMENTATION-OF-HUFFMAN-CODING-Completion-requirements

## Huffman-Coding

## Aim
To implement Huffman coding to compress the data using Python.

## Software Required
1. Anaconda - Python 3.7

## Algorithm:
### Step 1:

Get the input string from the user.

### Step 2:

Calculate the frequency of occurrence of each character in the input string.

### Step 3:

Create tree nodes for each character and construct the Huffman tree by repeatedly combining the two nodes with the lowest frequencies.

### Step 4:

Traverse the Huffman tree to generate binary codes for each character (0 for left and 1 for right).

### Step 5:

Print the characters and their corresponding Huffman codes.
 
## Program:

``` Python
import heapq

class Node:
    def __init__(self, char, freq):
        self.char = char
        self.freq = freq
        self.left = None
        self.right = None

def huffmanCoding(string):
    freq = {}

    for char in string:
        freq[char] = freq.get(char, 0) + 1

    heap = []
    count = 0

    for char, frequency in freq.items():
        heapq.heappush(heap, (frequency, count, Node(char, frequency)))
        count += 1

    while len(heap) > 1:
        freq1, _, node1 = heapq.heappop(heap)
        freq2, _, node2 = heapq.heappop(heap)

        newNode = Node(None, freq1 + freq2)
        newNode.left = node1
        newNode.right = node2

        heapq.heappush(heap, (newNode.freq, count, newNode))
        count += 1

    root = heap[0][2]
    codes = {}

    def generateCodes(node, code):
        if node.char is not None:
            codes[node.char] = code if code else "0"
            return

        generateCodes(node.left, code + "0")
        generateCodes(node.right, code + "1")

    generateCodes(root, "")

    print("Character and Huffman Code")

    for char, code in codes.items():
        print(repr(char), ":", code)

string = input("Enter the string: ")
huffmanCoding(string)
```

## Output:

<img width="473" height="426" alt="image" src="https://github.com/user-attachments/assets/067726fa-2388-4125-bd76-3e971897d9de" />

## Result
Thus the huffman coding was implemented to compress the data using python programming.
