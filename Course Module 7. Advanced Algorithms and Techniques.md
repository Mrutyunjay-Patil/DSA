---
tags: [DSA Java]
title: Course Module 7. Advanced Algorithms and Techniques
created: '2024-09-17T14:15:07.952Z'
modified: '2024-09-17T14:32:29.175Z'
---

# **Course Module 7. Advanced Algorithms and Techniques**

**Duration:** 2 Weeks

Advanced Algorithms and Techniques build upon the foundational algorithms you've already learned. They tackle more complex problems and introduce specialized methods to solve them efficiently. This module covers advanced dynamic programming approaches, powerful string algorithms, essential computational geometry concepts, efficient bit manipulation techniques, and the intriguing world of randomized algorithms. Each topic is explained in simple terms with practical examples and Java implementations to ensure clear understanding.

---

## **Week 1: Advanced Dynamic Programming and String Algorithms**

### **1. Advanced Dynamic Programming**

Dynamic Programming (DP) is a method for solving complex problems by breaking them down into simpler subproblems. In this section, we explore advanced applications of DP on trees and graphs, as well as techniques like bitmasking that allow DP to handle more intricate scenarios.

#### **1.1 DP on Trees and Graphs**

**Overview:**
While standard DP works well on linear data structures like arrays, DP on trees and graphs involves solving problems where the data is organized hierarchically or interconnectedly. These structures introduce additional challenges, such as handling branching paths and avoiding redundant calculations.

**How It Works:**
- **Trees:** Utilize the hierarchical nature to traverse nodes in a specific order (e.g., post-order) to solve subproblems before combining their results.
- **Graphs:** Handle cycles and multiple connections by using memoization and careful traversal strategies to ensure each subproblem is solved only once.

**Example: Counting the Number of Paths in a Tree**

**Problem:**
Given a tree (a connected acyclic graph) with `N` nodes, count the number of distinct paths between two nodes `u` and `v`.

**Approach:**
- Use DP to store the number of paths from each node to the target node.
- Traverse the tree using DFS, updating the path counts based on child nodes.

**Java Implementation:**

```java
import java.util.*;

public class DPTree {
    static class TreeNode {
        int val;
        List<TreeNode> children;

        TreeNode(int val) {
            this.val = val;
            children = new ArrayList<>();
        }
    }

    // Function to count paths from root to target
    public static int countPaths(TreeNode root, int target, Map<Integer, Integer> dp) {
        if (root == null)
            return 0;
        if (root.val == target)
            return 1;

        if (dp.containsKey(root.val))
            return dp.get(root.val);

        int count = 0;
        for (TreeNode child : root.children) {
            count += countPaths(child, target, dp);
        }

        dp.put(root.val, count);
        return count;
    }

    // Example usage
    public static void main(String[] args) {
        /*
                1
              / | \
             2  3  4
            /      \
           5        6
        */

        TreeNode root = new TreeNode(1);
        TreeNode node2 = new TreeNode(2);
        TreeNode node3 = new TreeNode(3);
        TreeNode node4 = new TreeNode(4);
        TreeNode node5 = new TreeNode(5);
        TreeNode node6 = new TreeNode(6);

        root.children.add(node2);
        root.children.add(node3);
        root.children.add(node4);
        node2.children.add(node5);
        node4.children.add(node6);

        int target = 5;
        Map<Integer, Integer> dp = new HashMap<>();
        int paths = countPaths(root, target, dp);
        System.out.println("Number of paths to " + target + ": " + paths);
        // Output: Number of paths to 5: 1
    }
}
```

**Explanation:**
- **TreeNode Class:** Represents each node in the tree with a value and a list of children.
- **countPaths Function:** Recursively counts the number of paths from the current node to the target node using DP to memoize results.
- **Main Function:** Constructs a sample tree and counts the paths to a specific node.

**Time Complexity:** O(N), where N is the number of nodes in the tree.

**Space Complexity:** O(N) due to the recursion stack and the DP map.

**When to Use:**
- Solving hierarchical problems like organizational charts.
- Analyzing dependencies in project management.
- Navigating file systems or XML/JSON structures.

---

#### **1.2 DP with Bitmasking**

**Overview:**
Bitmasking is a technique that uses bits to represent subsets of a set, allowing efficient storage and manipulation of these subsets. Combining DP with bitmasking enables the solution of problems involving subsets, permutations, and combinations where traditional DP would be inefficient.

**How It Works:**
- **Bitmask Representation:** Use an integer where each bit represents the presence (1) or absence (0) of an element in a subset.
- **DP State:** Define the DP state based on the bitmask, storing information relevant to that subset.
- **Transition:** Update the DP state by flipping bits to include or exclude elements.

**Example: Traveling Salesman Problem (TSP) with Bitmasking**

**Problem:**
Given a list of cities and the distances between each pair of cities, find the shortest possible route that visits each city exactly once and returns to the origin city.

**Approach:**
- Use bitmasking to represent the set of visited cities.
- DP state `dp[mask][i]` represents the minimum cost to reach city `i` with the visited set represented by `mask`.
- Iterate over all subsets and transitions to update the DP table.

**Java Implementation:**

```java
public class TSPBitmask {
    static int N = 4;
    static int INF = 1000000;
    static int[][] dist = {
        {0, 10, 15, 20},
        {10, 0, 35, 25},
        {15, 35, 0, 30},
        {20, 25, 30, 0}
    };

    static int[][] dp = new int[1 << N][N];

    // Function to solve TSP using DP with bitmasking
    public static int tsp(int mask, int pos) {
        if (mask == (1 << N) - 1) {
            return dist[pos][0];
        }

        if (dp[mask][pos] != -1)
            return dp[mask][pos];

        int answer = INF;

        for (int city = 0; city < N; city++) {
            if ((mask & (1 << city)) == 0) {
                int newAns = dist[pos][city] + tsp(mask | (1 << city), city);
                answer = Math.min(answer, newAns);
            }
        }

        return dp[mask][pos] = answer;
    }

    // Example usage
    public static void main(String[] args) {
        // Initialize DP table
        for (int i = 0; i < (1 << N); i++)
            for (int j = 0; j < N; j++)
                dp[i][j] = -1;

        int minCost = tsp(1, 0); // Start with mask=1 (only city 0 visited), at position 0
        System.out.println("Minimum cost of TSP: " + minCost);
        // Output: Minimum cost of TSP: 80
    }
}
```

**Explanation:**
- **dist Array:** Represents the distance between cities.
- **dp Array:** Stores the minimum cost for each subset of cities and current position.
- **tsp Function:** Recursively calculates the minimum cost by exploring all possible next cities using bitmasking to track visited cities.
- **Main Function:** Initializes the DP table and starts the TSP calculation from the first city.

**Time Complexity:** O(2^N * N^2), where N is the number of cities.

**Space Complexity:** O(2^N * N)

**When to Use:**
- Solving problems involving visiting all subsets or permutations.
- Optimizing routes and scheduling tasks.
- Games and puzzles requiring optimal pathfinding.

---

### **2. String Algorithms**

Strings are fundamental in computer science, appearing in tasks like text processing, search engines, and bioinformatics. Efficient string algorithms are essential for handling large volumes of text quickly.

#### **2.1 String Matching Algorithms (KMP, Rabin-Karp)**

**Overview:**
String Matching Algorithms are designed to find occurrences of a "pattern" string within a "text" string efficiently. Two popular algorithms are the Knuth-Morris-Pratt (KMP) and Rabin-Karp algorithms.

---

##### **2.1.1 Knuth-Morris-Pratt (KMP) Algorithm**

**Overview:**
The KMP Algorithm searches for a pattern within a text by preprocessing the pattern to create a "Longest Prefix Suffix" (LPS) array. This preprocessing allows the algorithm to skip unnecessary comparisons, improving efficiency.

**How It Works:**
1. **Preprocess** the pattern to create the LPS array.
2. **Traverse** the text and pattern simultaneously, using the LPS array to avoid re-examining characters.

**Example:**
Search for the pattern "ABABCABAB" in the text "ABABDABACDABABCABAB".

**Java Implementation:**

```java
public class KMPAlgorithm {
    // Function to create LPS array
    public static int[] computeLPSArray(String pattern) {
        int M = pattern.length();
        int[] lps = new int[M];
        int len = 0; // length of the previous longest prefix suffix
        lps[0] = 0; // lps[0] is always 0

        int i = 1;
        while (i < M) {
            if (pattern.charAt(i) == pattern.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            }
            else {
                if (len != 0) {
                    len = lps[len - 1];
                    // Do not increment i here
                }
                else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
        return lps;
    }

    // KMP search function
    public static void KMPSearch(String text, String pattern) {
        int N = text.length();
        int M = pattern.length();

        int[] lps = computeLPSArray(pattern);

        int i = 0; // index for text
        int j = 0; // index for pattern

        while (i < N) {
            if (pattern.charAt(j) == text.charAt(i)) {
                i++;
                j++;
            }

            if (j == M) {
                System.out.println("Found pattern at index " + (i - j));
                j = lps[j - 1];
            }
            else if (i < N && pattern.charAt(j) != text.charAt(i)) {
                if (j != 0)
                    j = lps[j - 1];
                else
                    i++;
            }
        }
    }

    // Example usage
    public static void main(String[] args) {
        String text = "ABABDABACDABABCABAB";
        String pattern = "ABABCABAB";
        KMPSearch(text, pattern);
        // Output: Found pattern at index 10
    }
}
```

**Explanation:**
- **computeLPSArray Function:** Creates the LPS array by finding the longest prefix that is also a suffix for each prefix of the pattern.
- **KMPSearch Function:** Uses the LPS array to efficiently search for the pattern in the text without unnecessary comparisons.
- **Main Function:** Demonstrates searching for a pattern within a text string.

**Time Complexity:** O(N + M), where N is the length of the text and M is the length of the pattern.

**Space Complexity:** O(M) for the LPS array.

**When to Use:**
- Implementing search features in text editors.
- DNA sequence analysis.
- Search engines and pattern recognition.

---

##### **2.1.2 Rabin-Karp Algorithm**

**Overview:**
The Rabin-Karp Algorithm uses hashing to find any one of a set of pattern strings in a text. It is particularly useful for multiple pattern searches and can handle large pattern sets efficiently.

**How It Works:**
1. **Calculate** the hash value of the pattern.
2. **Calculate** the hash value of each substring of the text with the same length as the pattern.
3. **Compare** the hash values; if they match, perform a character-by-character comparison to confirm.

**Example:**
Search for the pattern "ABC" in the text "ABABDABACDABABCABAB".

**Java Implementation:**

```java
public class RabinKarpAlgorithm {
    static final int d = 256; // Number of characters in the input alphabet
    static final int q = 101; // A prime number for modulo

    // Function to perform Rabin-Karp search
    public static void rabinKarpSearch(String text, String pattern) {
        int N = text.length();
        int M = pattern.length();
        int i, j;
        int p = 0; // Hash value for pattern
        int t = 0; // Hash value for text
        int h = 1;

        // The value of h would be "pow(d, M-1)%q"
        for (i = 0; i < M - 1; i++)
            h = (h * d) % q;

        // Calculate the hash value of pattern and first window of text
        for (i = 0; i < M; i++) {
            p = (d * p + pattern.charAt(i)) % q;
            t = (d * t + text.charAt(i)) % q;
        }

        // Slide the pattern over text one by one
        for (i = 0; i <= N - M; i++) {
            // Check the hash values of current window of text and pattern
            if (p == t) {
                // If hash values match, check characters one by one
                boolean match = true;
                for (j = 0; j < M; j++) {
                    if (text.charAt(i + j) != pattern.charAt(j)) {
                        match = false;
                        break;
                    }
                }
                if (match)
                    System.out.println("Pattern found at index " + i);
            }

            // Calculate hash value for next window of text
            if (i < N - M) {
                t = (d * (t - text.charAt(i) * h) + text.charAt(i + M)) % q;
                if (t < 0)
                    t += q;
            }
        }
    }

    // Example usage
    public static void main(String[] args) {
        String text = "ABABDABACDABABCABAB";
        String pattern = "ABC";
        rabinKarpSearch(text, pattern);
        // Output: Pattern found at index 12
    }
}
```

**Explanation:**
- **Hash Calculation:** Computes the hash of the pattern and the initial window in the text.
- **Sliding Window:** Moves the window one character at a time, updating the hash efficiently.
- **Match Verification:** When hash values match, verifies the actual characters to confirm a match.
- **Main Function:** Demonstrates searching for a pattern within a text string.

**Time Complexity:** Average and best case O(N + M), worst case O(N*M).

**Space Complexity:** O(1)

**When to Use:**
- Searching for multiple patterns simultaneously.
- Applications requiring fast substring searches.
- Implementing plagiarism detection tools.

---

#### **2.2 Suffix Trees and Arrays**

**Overview:**
Suffix Trees and Suffix Arrays are data structures that store all the suffixes of a given string. They are powerful tools for solving complex string problems like substring searches, pattern matching, and finding the longest repeated substring efficiently.

**How They Work:**
- **Suffix Tree:** A compressed trie containing all the suffixes of the string. Allows for fast pattern matching and other operations.
- **Suffix Array:** An array of integers representing the starting indices of all suffixes of the string in lexicographical order. More space-efficient than suffix trees.

**Example: Finding the Longest Repeated Substring**

**Problem:**
Find the longest substring that appears at least twice in a given string.

**Approach Using Suffix Array:**
1. Generate all suffixes of the string.
2. Sort the suffixes lexicographically.
3. Find the longest common prefix between consecutive suffixes in the sorted array.

**Java Implementation:**

```java
import java.util.*;

public class SuffixArray {
    // Function to build suffix array
    public static int[] buildSuffixArray(String s) {
        int N = s.length();
        Integer[] suffixes = new Integer[N];
        for (int i = 0; i < N; i++)
            suffixes[i] = i;

        // Sort suffixes using comparator
        Arrays.sort(suffixes, new Comparator<Integer>() {
            public int compare(Integer i1, Integer i2) {
                return s.substring(i1).compareTo(s.substring(i2));
            }
        });

        // Convert Integer[] to int[]
        int[] suffixArr = new int[N];
        for (int i = 0; i < N; i++)
            suffixArr[i] = suffixes[i];
        return suffixArr;
    }

    // Function to find the longest common prefix of two suffixes
    public static int lcp(String s, int i, int j) {
        int length = 0;
        while (i + length < s.length() && j + length < s.length() &&
               s.charAt(i + length) == s.charAt(j + length))
            length++;
        return length;
    }

    // Function to find the longest repeated substring
    public static String longestRepeatedSubstring(String s) {
        int[] suffixArr = buildSuffixArray(s);
        int maxLen = 0;
        int start = -1;

        for (int i = 1; i < s.length(); i++) {
            int len = lcp(s, suffixArr[i - 1], suffixArr[i]);
            if (len > maxLen) {
                maxLen = len;
                start = suffixArr[i];
            }
        }

        if (start != -1)
            return s.substring(start, start + maxLen);
        else
            return "";
    }

    // Example usage
    public static void main(String[] args) {
        String s = "banana";
        String lrs = longestRepeatedSubstring(s);
        System.out.println("Longest Repeated Substring: " + lrs);
        // Output: Longest Repeated Substring: an
    }
}
```

**Explanation:**
- **buildSuffixArray Function:** Generates and sorts all suffixes of the string.
- **lcp Function:** Calculates the longest common prefix between two suffixes.
- **longestRepeatedSubstring Function:** Iterates through the sorted suffix array to find the maximum LCP, identifying the longest repeated substring.
- **Main Function:** Demonstrates finding the longest repeated substring in "banana".

**Time Complexity:** O(N^2 log N) due to the substring comparisons during sorting. Optimized algorithms exist but are more complex.

**Space Complexity:** O(N^2) in the worst case due to storing substrings.

**When to Use:**
- DNA sequence analysis.
- Text editing and compression tools.
- Plagiarism detection.

---

#### **2.3 Trie-based Algorithms**

**Overview:**
A Trie (pronounced "try") is a tree-like data structure that stores a dynamic set of strings, where each node represents a common prefix of some strings. Tries are highly efficient for tasks involving prefix searches, autocomplete systems, and dictionary implementations.

**How They Work:**
- **Nodes:** Each node represents a character and contains pointers to child nodes.
- **Insertion:** Characters of a string are inserted sequentially, creating new nodes as needed.
- **Search:** Traverse the trie based on the characters of the query string.

**Example: Implementing an Autocomplete System**

**Problem:**
Given a list of words, implement an autocomplete feature that suggests words based on a given prefix.

**Approach:**
1. Build a Trie from the list of words.
2. Given a prefix, traverse the Trie to the end of the prefix.
3. Collect all words that start with the given prefix by traversing the subtree.

**Java Implementation:**

```java
import java.util.*;

public class TrieAutocomplete {
    static class TrieNode {
        Map<Character, TrieNode> children = new HashMap<>();
        boolean isEndOfWord;
    }

    static class Trie {
        TrieNode root;

        Trie() {
            root = new TrieNode();
        }

        // Insert a word into the trie
        public void insert(String word) {
            TrieNode node = root;
            for (char ch : word.toCharArray()) {
                node = node.children.computeIfAbsent(ch, c -> new TrieNode());
            }
            node.isEndOfWord = true;
        }

        // Search for a prefix and return the node where the prefix ends
        private TrieNode searchPrefix(String prefix) {
            TrieNode node = root;
            for (char ch : prefix.toCharArray()) {
                node = node.children.get(ch);
                if (node == null)
                    return null;
            }
            return node;
        }

        // Collect all words in the subtree rooted at the given node
        private void collectAllWords(TrieNode node, String prefix, List<String> results) {
            if (node.isEndOfWord)
                results.add(prefix);
            for (Map.Entry<Character, TrieNode> entry : node.children.entrySet()) {
                collectAllWords(entry.getValue(), prefix + entry.getKey(), results);
            }
        }

        // Get autocomplete suggestions for a given prefix
        public List<String> autocomplete(String prefix) {
            List<String> results = new ArrayList<>();
            TrieNode node = searchPrefix(prefix);
            if (node == null)
                return results;
            collectAllWords(node, prefix, results);
            return results;
        }
    }

    // Example usage
    public static void main(String[] args) {
        Trie trie = new Trie();
        String[] words = {"apple", "app", "application", "apt", "bat", "batch", "baton", "banana"};
        for (String word : words)
            trie.insert(word);

        String prefix = "app";
        List<String> suggestions = trie.autocomplete(prefix);
        System.out.println("Autocomplete suggestions for \"" + prefix + "\": " + suggestions);
        // Output: Autocomplete suggestions for "app": [apple, app, application]
    }
}
```

**Explanation:**
- **TrieNode Class:** Represents each node in the Trie with a map of child nodes and a flag indicating the end of a word.
- **Trie Class:** Contains methods to insert words, search for prefixes, collect words, and provide autocomplete suggestions.
- **Main Function:** Builds the Trie with a list of words and demonstrates the autocomplete feature for the prefix "app".

**Time Complexity:**
- **Insertion:** O(M), where M is the length of the word.
- **Search:** O(M), where M is the length of the prefix.
- **Autocomplete:** O(M + K), where K is the number of characters in the subtree.

**Space Complexity:** O(N * M), where N is the number of words and M is the average length of the words.

**When to Use:**
- Implementing autocomplete and spell-check features.
- IP routing and network management.
- Solving word games and puzzles.

---

## **Week 2: Computational Geometry, Bit Manipulation, and Randomized Algorithms**

### **3. Computational Geometry Basics**

Computational Geometry deals with algorithms and data structures for solving geometric problems. It's widely used in computer graphics, robotics, geographic information systems (GIS), and more.

#### **3.1 Convex Hull Algorithms**

**Overview:**
A Convex Hull is the smallest convex polygon that encloses all the given points in a set. Imagine stretching a rubber band around the outermost points; the shape it takes is the convex hull.

**How It Works:**
Several algorithms can compute the convex hull, such as Graham's Scan and Jarvis's March (Gift Wrapping). We'll explore Graham's Scan for its efficiency and simplicity.

**Example: Graham's Scan**

**Problem:**
Given a set of points on a 2D plane, find their convex hull.

**Approach:**
1. **Find the point** with the lowest y-coordinate (and lowest x-coordinate in case of a tie) as the reference point.
2. **Sort** the other points based on the angle they make with the reference point.
3. **Traverse** the sorted points and use a stack to maintain the convex hull, ensuring that we make only left turns.

**Java Implementation:**

```java
import java.util.*;

public class ConvexHullGrahamScan {
    static class Point implements Comparable<Point> {
        int x, y;

        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }

        // Compare points based on polar angle with reference
        public int compareTo(Point p) {
            int orientation = orientation(ConvexHullGrahamScan.reference, this, p);
            if (orientation == 0) {
                // If colinear, the closer point comes first
                return distance(ConvexHullGrahamScan.reference, p) - distance(ConvexHullGrahamScan.reference, this);
            }
            return (orientation == 2) ? -1 : 1;
        }

        // Calculate orientation of ordered triplet (p, q, r)
        // 0 --> colinear, 1 --> clockwise, 2 --> counterclockwise
        static int orientation(Point p, Point q, Point r) {
            int val = (q.y - p.y) * (r.x - q.x) - 
                      (q.x - p.x) * (r.y - q.y);
            if (val == 0)
                return 0;
            return (val > 0) ? 1 : 2;
        }

        // Calculate squared distance between two points
        static int distance(Point p1, Point p2) {
            return (p1.x - p2.x)*(p1.x - p2.x) + 
                   (p1.y - p2.y)*(p1.y - p2.y);
        }

        @Override
        public String toString() {
            return "(" + x + ", " + y + ")";
        }
    }

    static Point reference;

    // Function to compute convex hull using Graham's Scan
    public static List<Point> convexHull(List<Point> points) {
        int N = points.size();
        // Find the reference point
        reference = points.get(0);
        for (Point p : points) {
            if (p.y < reference.y || (p.y == reference.y && p.x < reference.x))
                reference = p;
        }

        // Sort the points based on polar angle with reference
        Collections.sort(points);

        Stack<Point> stack = new Stack<>();
        stack.push(points.get(0));
        stack.push(points.get(1));

        for (int i = 2; i < N; i++) {
            Point top = stack.pop();
            while (!stack.isEmpty() && 
                   Point.orientation(stack.peek(), top, points.get(i)) != 2) {
                top = stack.pop();
            }
            stack.push(top);
            stack.push(points.get(i));
        }

        return new ArrayList<>(stack);
    }

    // Example usage
    public static void main(String[] args) {
        List<Point> points = Arrays.asList(
            new Point(0, 3),
            new Point(2, 2),
            new Point(1, 1),
            new Point(2, 1),
            new Point(3, 0),
            new Point(0, 0),
            new Point(3, 3)
        );

        List<Point> hull = convexHull(new ArrayList<>(points));
        System.out.println("Convex Hull:");
        for (Point p : hull)
            System.out.println(p);
        /*
        Output:
        Convex Hull:
        (0, 0)
        (3, 0)
        (3, 3)
        (0, 3)
        */
    }
}
```

**Explanation:**
- **Point Class:** Represents a point with x and y coordinates and includes methods for comparing points based on polar angle and calculating orientation.
- **convexHull Function:** Implements Graham's Scan by sorting points, using a stack to build the hull, and ensuring only left turns are made.
- **Main Function:** Demonstrates finding the convex hull of a set of points.

**Time Complexity:** O(N log N) due to the sorting step.

**Space Complexity:** O(N) for storing the points and the stack.

**When to Use:**
- Computer graphics and image processing.
- Pattern recognition and machine learning.
- Geographic Information Systems (GIS).

---

##### **3.1.2 Line Intersection**

**Overview:**
Determining whether two lines intersect is a fundamental problem in computational geometry. It's essential for applications like computer graphics, collision detection, and geographic mapping.

**How It Works:**
- Use the concept of orientation and the general case of intersection based on the positions of the endpoints.

**Example: Checking if Two Lines Intersect**

**Problem:**
Given two line segments defined by their endpoints, determine if they intersect.

**Approach:**
1. **Calculate orientations** of ordered triplets to understand the relative positions.
2. **General Case:** Two lines intersect if they straddle each other's endpoints.
3. **Special Cases:** Handle colinear and overlapping scenarios.

**Java Implementation:**

```java
public class LineIntersection {
    static class Point {
        int x, y;

        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    // Function to find orientation of ordered triplet (p, q, r)
    // 0 --> colinear, 1 --> clockwise, 2 --> counterclockwise
    public static int orientation(Point p, Point q, Point r) {
        int val = (q.y - p.y)*(r.x - q.x) - 
                  (q.x - p.x)*(r.y - q.y);
        if (val == 0)
            return 0;
        return (val > 0) ? 1 : 2;
    }

    // Function to check if point q lies on line segment pr
    public static boolean onSegment(Point p, Point q, Point r) {
        return q.x <= Math.max(p.x, r.x) && q.x >= Math.min(p.x, r.x) &&
               q.y <= Math.max(p.y, r.y) && q.y >= Math.min(p.y, r.y);
    }

    // Function to check if two line segments intersect
    public static boolean doIntersect(Point p1, Point q1, Point p2, Point q2) {
        // Find the four orientations needed for general and special cases
        int o1 = orientation(p1, q1, p2);
        int o2 = orientation(p1, q1, q2);
        int o3 = orientation(p2, q2, p1);
        int o4 = orientation(p2, q2, q1);

        // General case
        if (o1 != o2 && o3 != o4)
            return true;

        // Special Cases
        // p1, q1 and p2 are colinear and p2 lies on segment p1q1
        if (o1 == 0 && onSegment(p1, p2, q1)) return true;

        // p1, q1 and q2 are colinear and q2 lies on segment p1q1
        if (o2 == 0 && onSegment(p1, q2, q1)) return true;

        // p2, q2 and p1 are colinear and p1 lies on segment p2q2
        if (o3 == 0 && onSegment(p2, p1, q2)) return true;

        // p2, q2 and q1 are colinear and q1 lies on segment p2q2
        if (o4 == 0 && onSegment(p2, q1, q2)) return true;

        // Doesn't fall in any of the above cases
        return false;
    }

    // Example usage
    public static void main(String[] args) {
        Point p1 = new Point(1, 1);
        Point q1 = new Point(10, 1);
        Point p2 = new Point(1, 2);
        Point q2 = new Point(10, 2);

        if (doIntersect(p1, q1, p2, q2))
            System.out.println("Yes");
        else
            System.out.println("No");
        // Output: No

        Point p3 = new Point(10, 0);
        Point q3 = new Point(0, 10);
        Point p4 = new Point(0, 0);
        Point q4 = new Point(10, 10);

        if (doIntersect(p3, q3, p4, q4))
            System.out.println("Yes");
        else
            System.out.println("No");
        // Output: Yes
    }
}
```

**Explanation:**
- **Point Class:** Represents a point with x and y coordinates.
- **orientation Function:** Determines the orientation of three points.
- **onSegment Function:** Checks if a point lies on a given line segment.
- **doIntersect Function:** Uses orientations to determine if two line segments intersect.
- **Main Function:** Tests the intersection of two pairs of line segments.

**Time Complexity:** O(1), constant time for each intersection check.

**Space Complexity:** O(1)

**When to Use:**
- Collision detection in games and simulations.
- Geographic Information Systems (GIS) for map overlays.
- Computer graphics for rendering scenes.

---

### **4. Bit Manipulation Techniques**

**Overview:**
Bit Manipulation involves using bitwise operations to perform computations efficiently. It's a powerful tool for optimizing space and speed, especially in low-level programming and scenarios where resources are constrained.

**How It Works:**
- **Bitwise Operators:** Perform operations like AND (`&`), OR (`|`), XOR (`^`), NOT (`~`), left shift (`<<`), and right shift (`>>`).
- **Bit Tricks:** Utilize properties of bits to solve problems with minimal operations.

**Example: Common Bit Tricks**

---

#### **4.1 Common Bit Tricks**

**1. Check if a Number is Even or Odd**

- **Even:** Last bit is 0.
- **Odd:** Last bit is 1.

**Java Implementation:**

```java
public class BitTricks {
    public static boolean isEven(int n) {
        return (n & 1) == 0;
    }

    public static void main(String[] args) {
        int num = 4;
        if (isEven(num))
            System.out.println(num + " is even.");
        else
            System.out.println(num + " is odd.");
        // Output: 4 is even.
    }
}
```

**2. Toggle a Bit at a Given Position**

**Problem:**
Toggle (flip) the bit at a specific position in an integer.

**Java Implementation:**

```java
public class BitTricks {
    // Toggle bit at position pos
    public static int toggleBit(int n, int pos) {
        return n ^ (1 << pos);
    }

    public static void main(String[] args) {
        int num = 5; // Binary: 0101
        int pos = 1;
        int toggled = toggleBit(num, pos);
        System.out.println("Original: " + Integer.toBinaryString(num));
        System.out.println("Toggled: " + Integer.toBinaryString(toggled));
        // Output:
        // Original: 101
        // Toggled: 111
    }
}
```

**3. Count the Number of Set Bits (1s) in an Integer**

**Java Implementation:**

```java
public class BitTricks {
    // Count set bits using Brian Kernighan’s Algorithm
    public static int countSetBits(int n) {
        int count = 0;
        while (n > 0) {
            n &= (n - 1);
            count++;
        }
        return count;
    }

    public static void main(String[] args) {
        int num = 15; // Binary: 1111
        int setBits = countSetBits(num);
        System.out.println("Number of set bits in " + num + " is " + setBits);
        // Output: Number of set bits in 15 is 4
    }
}
```

**Explanation:**
- **n &= (n - 1):** Removes the lowest set bit from `n`.
- **Loop:** Counts how many times we can remove a set bit until `n` becomes zero.

**Time Complexity:** O(k), where k is the number of set bits.

**Space Complexity:** O(1)

**When to Use:**
- Optimizing space for storing flags or small integers.
- Implementing low-level protocols and hardware interfaces.
- Solving combinatorial problems efficiently.

---

#### **4.2 Applications in Problem Solving**

**1. Finding a Missing Number in a Sequence**

**Problem:**
Given an array containing `n-1` distinct numbers from `1` to `n`, find the missing number.

**Approach:**
Use XOR to cancel out pairs, leaving the missing number.

**Java Implementation:**

```java
public class BitTricks {
    public static int findMissingNumber(int[] arr, int n) {
        int x1 = 1;
        for (int i = 2; i <= n; i++)
            x1 ^= i;

        int x2 = arr[0];
        for (int i = 1; i < arr.length; i++)
            x2 ^= arr[i];

        return x1 ^ x2;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 4, 5, 6};
        int n = 6;
        int missing = findMissingNumber(arr, n);
        System.out.println("Missing number is " + missing);
        // Output: Missing number is 3
    }
}
```

**Explanation:**
- **x1:** XOR of all numbers from 1 to n.
- **x2:** XOR of all elements in the array.
- **Result:** XOR of x1 and x2 gives the missing number.

**2. Checking if a Number is a Power of Two**

**Problem:**
Determine if a given integer is a power of two.

**Approach:**
A number is a power of two if it has exactly one set bit.

**Java Implementation:**

```java
public class BitTricks {
    public static boolean isPowerOfTwo(int n) {
        if (n <= 0)
            return false;
        return (n & (n - 1)) == 0;
    }

    public static void main(String[] args) {
        int num = 16;
        if (isPowerOfTwo(num))
            System.out.println(num + " is a power of two.");
        else
            System.out.println(num + " is not a power of two.");
        // Output: 16 is a power of two.
    }
}
```

**Explanation:**
- **n & (n - 1):** Removes the lowest set bit. If the result is zero, there's only one set bit.

**3. Swapping Two Numbers Without Temporary Variable**

**Problem:**
Swap two integers without using a temporary variable.

**Approach:**
Use XOR to swap the values.

**Java Implementation:**

```java
public class BitTricks {
    public static void swap(int a, int b) {
        System.out.println("Before Swap: a = " + a + ", b = " + b);
        a = a ^ b;
        b = a ^ b; // Now b = a
        a = a ^ b; // Now a = b
        System.out.println("After Swap: a = " + a + ", b = " + b);
    }

    public static void main(String[] args) {
        int a = 5, b = 10;
        swap(a, b);
        /*
        Output:
        Before Swap: a = 5, b = 10
        After Swap: a = 10, b = 5
        */
    }
}
```

**Explanation:**
- **Step 1:** `a = a ^ b`
- **Step 2:** `b = a ^ b` results in `b = a`
- **Step 3:** `a = a ^ b` results in `a = b`

**When to Use:**
- Optimizing memory usage in low-level programming.
- Solving problems where space optimization is critical.
- Understanding fundamental bitwise operations.

---

### **4. Randomized Algorithms**

**Overview:**
Randomized Algorithms use random numbers at some point during their execution to make decisions. They are often simpler and faster than their deterministic counterparts and can provide good average-case performance even in the worst-case scenarios.

#### **4.1 Monte Carlo and Las Vegas Algorithms**

**Monte Carlo Algorithms:**
- Provide correct results with a certain probability.
- Have a fixed runtime but may occasionally produce incorrect results.
- Example: Probabilistic primality testing.

**Las Vegas Algorithms:**
- Always produce correct results.
- The runtime is random but with an expected value.
- Example: Randomized Quick Sort.

**Example: Randomized Primality Test (Monte Carlo)**

**Problem:**
Determine if a number is prime using a probabilistic method.

**Approach:**
Use the Fermat primality test, which relies on Fermat's Little Theorem.

**Java Implementation:**

```java
import java.util.Random;

public class MonteCarloPrimality {
    // Function to perform Fermat's primality test
    public static boolean isPrime(int n, int k) {
        if (n <= 1 || n == 4)
            return false;
        if (n <= 3)
            return true;

        Random rand = new Random();

        // Repeat the test k times
        while (k > 0) {
            // Pick a random number in [2, n-2]
            int a = 2 + rand.nextInt(n - 4);

            // Fermat's little theorem
            if (power(a, n - 1, n) != 1)
                return false;

            k--;
        }

        return true;
    }

    // Function to perform modular exponentiation
    public static int power(int a, int b, int mod) {
        int res = 1;
        a = a % mod;
        while (b > 0) {
            if ((b & 1) == 1)
                res = (res * a) % mod;
            b = b >> 1;
            a = (a * a) % mod;
        }
        return res;
    }

    // Example usage
    public static void main(String[] args) {
        int n = 19;
        int k = 5; // Number of trials
        if (isPrime(n, k))
            System.out.println(n + " is probably prime.");
        else
            System.out.println(n + " is composite.");
        // Output: 19 is probably prime.
    }
}
```

**Explanation:**
- **isPrime Function:** Performs the Fermat primality test `k` times with random bases.
- **power Function:** Efficiently computes `(a^b) % mod` using modular exponentiation.
- **Main Function:** Tests if the number 19 is prime.

**Time Complexity:** O(k log n), where `k` is the number of trials.

**Space Complexity:** O(1)

**When to Use:**
- Quickly testing large numbers for primality.
- Cryptographic applications.
- Situations where a small probability of error is acceptable.

---

#### **4.2 Randomized Quick Sort**

**Overview:**
Quick Sort is a popular sorting algorithm, and its randomized version selects a pivot randomly to improve performance, especially in the average case. Randomization helps avoid the worst-case scenario where the pivot selection leads to unbalanced partitions.

**How It Works:**
1. **Select a pivot** randomly from the array.
2. **Partition** the array into elements less than the pivot and greater than the pivot.
3. **Recursively** apply the same strategy to the subarrays.
4. **Combine** the sorted subarrays.

**Java Implementation:**

```java
import java.util.Random;

public class RandomizedQuickSort {
    // Function to perform randomized quicksort
    public static void randomizedQuickSort(int[] arr, int low, int high) {
        if (low < high) {
            // Partition the array and get pivot index
            int pi = randomizedPartition(arr, low, high);

            // Recursively sort elements before and after partition
            randomizedQuickSort(arr, low, pi - 1);
            randomizedQuickSort(arr, pi + 1, high);
        }
    }

    // Function to choose a random pivot and partition the array
    public static int randomizedPartition(int[] arr, int low, int high) {
        Random rand = new Random();
        int pivotIndex = low + rand.nextInt(high - low + 1);
        swap(arr, pivotIndex, high); // Move pivot to end
        return partition(arr, low, high);
    }

    // Standard partition function
    public static int partition(int[] arr, int low, int high) {
        int pivot = arr[high];
        int i = low - 1; // Index of smaller element

        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                i++;
                swap(arr, i, j);
            }
        }

        swap(arr, i + 1, high);
        return i + 1;
    }

    // Utility function to swap two elements
    public static void swap(int[] arr, int i, int j) {
        if (i == j)
            return;
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Function to print the array
    public static void printArray(int[] arr) {
        for (int num : arr)
            System.out.print(num + " ");
        System.out.println();
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {10, 7, 8, 9, 1, 5};
        System.out.println("Original array:");
        printArray(arr);

        randomizedQuickSort(arr, 0, arr.length - 1);

        System.out.println("Sorted array:");
        printArray(arr);
        /*
        Possible Output:
        Original array:
        10 7 8 9 1 5 
        Sorted array:
        1 5 7 8 9 10 
        */
    }
}
```

**Explanation:**
- **randomizedQuickSort Function:** Recursively sorts the array by partitioning it around a randomly chosen pivot.
- **randomizedPartition Function:** Selects a random pivot to enhance performance and avoid worst-case scenarios.
- **partition Function:** Rearranges elements based on the pivot.
- **swap Function:** Exchanges two elements in the array.
- **Main Function:** Demonstrates sorting an array using randomized Quick Sort.

**Time Complexity:**
- **Average Case:** O(N log N)
- **Worst Case:** O(N^2) (rare due to randomization)

**Space Complexity:** O(log N) due to recursion stack.

**When to Use:**
- General-purpose sorting when average performance is desired.
- Applications where avoiding worst-case scenarios is critical.
- Situations requiring efficient in-place sorting.

---

## **Summary and Exercises**

### **Summary:**

In this module, you've explored a variety of advanced algorithms and techniques that extend the capabilities of standard algorithmic approaches:

- **Advanced Dynamic Programming:** Learned how to apply DP to complex structures like trees and graphs, and utilized bitmasking for efficient subset handling.
  
- **String Algorithms:** Mastered powerful string matching algorithms (KMP and Rabin-Karp), and delved into advanced data structures like suffix trees, suffix arrays, and tries for efficient string processing.
  
- **Computational Geometry:** Gained insights into fundamental geometric algorithms, including constructing convex hulls and detecting line intersections, essential for spatial problem-solving.
  
- **Bit Manipulation Techniques:** Discovered common bit tricks and their applications in optimizing problem-solving tasks, enhancing both speed and space efficiency.
  
- **Randomized Algorithms:** Explored probabilistic methods like Monte Carlo and Las Vegas algorithms, and implemented randomized Quick Sort to achieve improved average-case performance.

### **Key Takeaways:**

- **Advanced DP:** Enhances problem-solving by efficiently handling complex data structures and large subsets.
  
- **String Processing:** Enables fast and efficient search, pattern matching, and manipulation of textual data.
  
- **Geometry Algorithms:** Essential for applications requiring spatial analysis and graphical computations.
  
- **Bit Manipulation:** Offers low-level optimization techniques that can significantly speed up computations.
  
- **Randomization:** Provides flexibility and efficiency in algorithms, especially when deterministic methods are too slow or complex.

### **Exercises:**

#### **1. Advanced Dynamic Programming:**

**a. DP on Trees:**
- **Problem:** Given a tree where each node has a value, find the maximum path sum between any two nodes.
- **Task:** Implement a DP solution that traverses the tree and calculates the maximum path sum.

**b. DP with Bitmasking:**
- **Problem:** Solve the "Travelling Salesman Problem" for a set of cities using DP with bitmasking.
- **Task:** Modify the provided TSP example to also return the path taken.

#### **2. String Algorithms:**

**a. KMP Algorithm:**
- **Problem:** Implement the KMP algorithm to find all occurrences of a pattern in a text.
- **Task:** Modify the KMP implementation to return a list of all starting indices where the pattern is found.

**b. Rabin-Karp Algorithm:**
- **Problem:** Use the Rabin-Karp algorithm to find multiple patterns in a text.
- **Task:** Extend the Rabin-Karp implementation to handle multiple patterns and return their respective indices.

**c. Suffix Trees and Arrays:**
- **Problem:** Implement a suffix array construction and use it to find the longest repeated substring in a larger text.
- **Task:** Optimize the suffix array implementation to handle strings of up to 10^5 characters efficiently.

**d. Trie-based Algorithms:**
- **Problem:** Implement a spell-checker using a trie that suggests corrections for misspelled words.
- **Task:** Enhance the trie to handle wildcard characters (e.g., '?') in the search queries.

#### **3. Computational Geometry:**

**a. Convex Hull Algorithms:**
- **Problem:** Implement Jarvis's March (Gift Wrapping) algorithm and compare it with Graham's Scan in terms of performance.
- **Task:** Modify the convex hull implementation to visualize the hull by printing the sequence of points.

**b. Line Intersection:**
- **Problem:** Given a set of line segments, find all pairs that intersect.
- **Task:** Optimize the intersection check to handle up to 10^5 line segments efficiently.

#### **4. Bit Manipulation Techniques:**

**a. Common Bit Tricks:**
- **Problem:** Implement a function to determine if two integers have opposite signs using bit manipulation.
- **Task:** Write a function that swaps the even and odd bits of an integer using bitwise operations.

**b. Applications in Problem Solving:**
- **Problem:** Given an array of integers where every number appears twice except for two unique numbers, find those two unique numbers.
- **Task:** Use bit manipulation to solve the problem with O(N) time and O(1) space complexity.

#### **5. Randomized Algorithms:**

**a. Monte Carlo and Las Vegas Algorithms:**
- **Problem:** Implement the Miller-Rabin primality test as a Monte Carlo algorithm.
- **Task:** Compare its performance and accuracy with the deterministic sieve of Eratosthenes for large numbers.

**b. Randomized Quick Sort:**
- **Problem:** Modify the randomized Quick Sort to count the number of comparisons made during sorting.
- **Task:** Analyze the average number of comparisons for different array sizes and contents.

#### **6. Combined Techniques:**

**a. Bitmasking and DP:**
- **Problem:** Solve the "Subset Sum Problem" using DP with bitmasking to represent subsets.
- **Task:** Optimize the solution to handle subsets of size up to 20 efficiently.

**b. String and Bit Manipulation:**
- **Problem:** Implement a function that compresses a string by removing consecutive duplicate characters using bit manipulation.
- **Task:** Extend the function to handle case-insensitive duplicates and preserve the original case in the output.

### **Further Reading and Resources:**

- **Books:**
  - *Introduction to Algorithms* by Cormen, Leiserson, Rivest, and Stein.
  - *Algorithms* by Robert Sedgewick and Kevin Wayne.
  - *Competitive Programming* by Steven Halim and Felix Halim.

- **Online Tutorials:**
  - [GeeksforGeeks Advanced Algorithms](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)
  - [Khan Academy - Algorithms](https://www.khanacademy.org/computing/computer-science/algorithms)
  - [VisuAlgo](https://visualgo.net/en) for visualizing complex algorithms.

- **Video Lectures:**
  - [MIT OpenCourseWare - Advanced Algorithms](https://ocw.mit.edu/courses/6-854j-advanced-algorithm-design-and-analysis-fall-2005/)
  - [Stanford University - CS 161: Design and Analysis of Algorithms](https://www.youtube.com/playlist?list=PLoROMvodv4rO1NB9TD4iUZ3qghGEGtqNX)
  - [Harvard's CS50 on YouTube](https://www.youtube.com/user/cs50tv)

- **Interactive Platforms:**
  - [LeetCode](https://leetcode.com/) and [HackerRank](https://www.hackerrank.com/domains/algorithms) for practicing advanced algorithmic problems.
  - [Codeforces](https://codeforces.com/) for competitive programming challenges.
  - [GeeksforGeeks Playground](https://practice.geeksforgeeks.org/) for hands-on coding practice.

---

By completing this module on Advanced Algorithms and Techniques, you've expanded your problem-solving toolkit to include sophisticated methods that tackle complex scenarios efficiently. These skills are invaluable for tackling challenging technical interviews, optimizing software performance, and solving real-world computational problems. Continue practicing through the exercises and utilize the provided resources to deepen your understanding and mastery of advanced algorithmic concepts.
