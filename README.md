### NAME: SURYA P <br>
### REG NO: 212224230280 <br> 
### Date: 06/02/2026

## EX. No. 3 : Implementation Of GSP Algorithm in Python

### AIM: 
To implement GSP Algorithm In Python.

### DESCRIPTION :

The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.

### STEPS :

1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### PROCEDURE :

<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>

### PROGRAM :

```
from collections import defaultdict
from itertools import combinations

def generate_candidates(dataset, k, min_support):
    candidates = defaultdict(int)
    for seq in dataset:
        flat_seq = [item for itemset in seq for item in itemset]
        for comb in combinations(flat_seq, k):
            candidates[comb] += 1
    return {item: support for item, support in candidates.items() if support >= min_support}

def gsp(dataset, min_support):
    fp = defaultdict(int)
    k = 1
    while True:
        candidates = generate_candidates(dataset, k, min_support)
        if not candidates:
            break
        fp.update(candidates)
        k += 1
    return fp

dataset = [
    [["a","b","c"], ["b","e"], ["c","f","g"], ["a","b","e"]],
    [["a","d"], ["b","c"], ["c"], ["f","g"], ["c","h"]],
    [["b","c"], ["a","d"], ["e","b","f"], ["c","d","f","g","h"]],
    [["c"], ["e","c"], ["e","h"]]
]

min_support = 3

results = gsp(dataset, min_support)
print("Frequent Sequential Patterns:")
if results:
    for pattern, support in results.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")

```

### OUTPUT :

<img width="388" height="785" alt="image" src="https://github.com/user-attachments/assets/df978107-2d27-4b7a-9fc2-507dc32e9461" />
<img width="398" height="760" alt="image" src="https://github.com/user-attachments/assets/fb429c75-3306-4f0a-847f-292e1bf7784d" />

### VISUALIZATION :

```python
import matplotlib.pyplot as plt
def visualize_patterns_line(result):
    if result:
        patterns = [str(pattern) for pattern in result.keys()]
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot(patterns, support, marker='o')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title('Frequent Sequential Patterns')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print("No frequent sequential patterns found.")

visualize_patterns_line(results)
```

### OUTPUT :
<img width="1228" height="726" alt="image" src="https://github.com/user-attachments/assets/f43ba4d0-7b81-4b30-8215-62769ac12d6c" />

### RESULT :
The GSP algorithm in python has been successfully implemented.
