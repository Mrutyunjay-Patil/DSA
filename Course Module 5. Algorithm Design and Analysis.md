---
tags: [DSA Java]
title: Course Module 5. Algorithm Design and Analysis
created: '2024-09-17T13:58:40.323Z'
modified: '2024-09-17T14:32:24.826Z'
---

# **Course Module 5. Algorithm Design and Analysis**

**Duration:** 3 Weeks

Algorithm Design and Analysis is a cornerstone of computer science and software engineering. Understanding how to design efficient algorithms and analyze their performance is essential for solving complex problems, optimizing solutions, and succeeding in technical interviews at top-tier companies like Microsoft and Google. This module is crafted to demystify challenging concepts, making them accessible even to those without a strong technical background. Through simple language, clear explanations, and practical examples, you'll build the skills necessary to design, implement, and evaluate a wide range of algorithms.

---

## **Week 1: Sorting and Searching Algorithms**

### **1. Sorting Algorithms**

Sorting is the process of arranging data in a particular order, typically in ascending or descending numerical or lexicographical order. Sorting algorithms are fundamental because they improve the efficiency of other algorithms (like search algorithms) and are used in various applications such as databases, graphics, and scientific computing.

#### **1.1 Bubble Sort**

**Overview:**
Bubble Sort is one of the simplest sorting algorithms. It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This process continues until the list is sorted.

**How It Works:**
- Compare each pair of adjacent elements.
- Swap them if they are in the wrong order.
- Repeat the process for the entire list until no swaps are needed.

**Example:**
Sort the array `[5, 2, 9, 1, 5, 6]` in ascending order.

**Steps:**
1. First Pass:
   - Compare 5 and 2 → swap → `[2, 5, 9, 1, 5, 6]`
   - Compare 5 and 9 → no swap → `[2, 5, 9, 1, 5, 6]`
   - Compare 9 and 1 → swap → `[2, 5, 1, 9, 5, 6]`
   - Compare 9 and 5 → swap → `[2, 5, 1, 5, 9, 6]`
   - Compare 9 and 6 → swap → `[2, 5, 1, 5, 6, 9]`
2. Second Pass:
   - Compare 2 and 5 → no swap → `[2, 5, 1, 5, 6, 9]`
   - Compare 5 and 1 → swap → `[2, 1, 5, 5, 6, 9]`
   - Compare 5 and 5 → no swap → `[2, 1, 5, 5, 6, 9]`
   - Compare 5 and 6 → no swap → `[2, 1, 5, 5, 6, 9]`
3. Continue until the array is sorted: `[1, 2, 5, 5, 6, 9]`

**Java Implementation:**

```java
public class BubbleSort {
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;
        // Traverse through all array elements
        for (int i = 0; i < n - 1; i++) {
            swapped = false;
            // Last i elements are already in place
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap arr[j] and arr[j+1]
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }
            // If no two elements were swapped, array is sorted
            if (!swapped)
                break;
        }
    }

    // Utility method to print the array
    public static void printArray(int[] arr) {
        for (int num : arr)
            System.out.print(num + " ");
        System.out.println();
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {5, 2, 9, 1, 5, 6};
        System.out.println("Original array:");
        printArray(arr);

        bubbleSort(arr);

        System.out.println("Sorted array:");
        printArray(arr);
        // Output:
        // Original array:
        // 5 2 9 1 5 6 
        // Sorted array:
        // 1 2 5 5 6 9 
    }
}
```

**Time Complexity:**
- **Best Case:** O(n) (when the array is already sorted)
- **Average Case:** O(n²)
- **Worst Case:** O(n²)

**Space Complexity:** O(1) (in-place sorting)

**When to Use:**
- Suitable for small datasets.
- Not recommended for large datasets due to its inefficiency.

---

#### **1.2 Selection Sort**

**Overview:**
Selection Sort divides the input list into two parts: a sorted sublist of items already sorted and an unsorted sublist of items remaining to be sorted. It repeatedly selects the smallest (or largest) element from the unsorted sublist and moves it to the end of the sorted sublist.

**How It Works:**
- Find the minimum element from the unsorted part.
- Swap it with the first unsorted element.
- Move the boundary of the sorted and unsorted sublists one element to the right.

**Example:**
Sort the array `[64, 25, 12, 22, 11]` in ascending order.

**Steps:**
1. Find the minimum element (11) and swap with the first element (64): `[11, 25, 12, 22, 64]`
2. Find the next minimum element (12) and swap with the second element (25): `[11, 12, 25, 22, 64]`
3. Find the next minimum element (22) and swap with the third element (25): `[11, 12, 22, 25, 64]`
4. The array is now sorted: `[11, 12, 22, 25, 64]`

**Java Implementation:**

```java
public class SelectionSort {
    public static void selectionSort(int[] arr) {
        int n = arr.length;
        // Traverse through all array elements
        for (int i = 0; i < n - 1; i++) {
            // Find the minimum element in unsorted array
            int minIdx = i;
            for (int j = i + 1; j < n; j++)
                if (arr[j] < arr[minIdx])
                    minIdx = j;

            // Swap the found minimum element with the first element
            int temp = arr[minIdx];
            arr[minIdx] = arr[i];
            arr[i] = temp;
        }
    }

    // Utility method to print the array
    public static void printArray(int[] arr) {
        for (int num : arr)
            System.out.print(num + " ");
        System.out.println();
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {64, 25, 12, 22, 11};
        System.out.println("Original array:");
        printArray(arr);

        selectionSort(arr);

        System.out.println("Sorted array:");
        printArray(arr);
        // Output:
        // Original array:
        // 64 25 12 22 11 
        // Sorted array:
        // 11 12 22 25 64 
    }
}
```

**Time Complexity:**
- **Best Case:** O(n²)
- **Average Case:** O(n²)
- **Worst Case:** O(n²)

**Space Complexity:** O(1) (in-place sorting)

**When to Use:**
- Useful when memory writes are expensive since it makes the minimum number of swaps.
- Not suitable for large datasets due to its inefficiency.

---

#### **1.3 Insertion Sort**

**Overview:**
Insertion Sort builds the final sorted array one element at a time. It is much less efficient on large lists compared to more advanced algorithms but has several advantages, such as simple implementation and efficient performance on small or nearly sorted datasets.

**How It Works:**
- Start with the second element; assume the first element is sorted.
- Compare the current element with the sorted elements and insert it into the correct position.
- Repeat until the entire array is sorted.

**Example:**
Sort the array `[12, 11, 13, 5, 6]` in ascending order.

**Steps:**
1. Start with 11: `[11, 12, 13, 5, 6]`
2. Next, 13 remains in place: `[11, 12, 13, 5, 6]`
3. Insert 5: `[5, 11, 12, 13, 6]`
4. Insert 6: `[5, 6, 11, 12, 13]`

**Java Implementation:**

```java
public class InsertionSort {
    public static void insertionSort(int[] arr) {
        int n = arr.length;
        // Traverse from 1 to n
        for (int i = 1; i < n; ++i) {
            int key = arr[i];
            int j = i - 1;

            // Move elements of arr[0..i-1], that are greater than key, to one position ahead
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
        }
    }

    // Utility method to print the array
    public static void printArray(int[] arr) {
        for (int num : arr)
            System.out.print(num + " ");
        System.out.println();
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {12, 11, 13, 5, 6};
        System.out.println("Original array:");
        printArray(arr);

        insertionSort(arr);

        System.out.println("Sorted array:");
        printArray(arr);
        // Output:
        // Original array:
        // 12 11 13 5 6 
        // Sorted array:
        // 5 6 11 12 13 
    }
}
```

**Time Complexity:**
- **Best Case:** O(n) (when the array is already sorted)
- **Average Case:** O(n²)
- **Worst Case:** O(n²)

**Space Complexity:** O(1) (in-place sorting)

**When to Use:**
- Efficient for small or nearly sorted datasets.
- Preferred when memory usage is a concern.

---

#### **1.4 Merge Sort**

**Overview:**
Merge Sort is a divide-and-conquer algorithm that divides the array into smaller subarrays, sorts them, and then merges them back together. It is highly efficient and has a consistent performance regardless of the input data.

**How It Works:**
- **Divide:** Split the array into two halves.
- **Conquer:** Recursively sort both halves.
- **Combine:** Merge the two sorted halves into a single sorted array.

**Example:**
Sort the array `[38, 27, 43, 3, 9, 82, 10]` in ascending order.

**Steps:**
1. Divide into `[38, 27, 43, 3]` and `[9, 82, 10]`
2. Further divide into `[38, 27]`, `[43, 3]`, `[9, 82]`, `[10]`
3. Sort each subarray: `[27, 38]`, `[3, 43]`, `[9, 82]`, `[10]`
4. Merge to form `[3, 27, 38, 43]` and `[9, 10, 82]`
5. Finally, merge to form `[3, 9, 10, 27, 38, 43, 82]`

**Java Implementation:**

```java
public class MergeSort {
    // Merge two subarrays of arr[]
    private static void merge(int[] arr, int l, int m, int r) {
        // Sizes of two subarrays to be merged
        int n1 = m - l + 1;
        int n2 = r - m;

        /* Create temporary arrays */
        int[] L = new int[n1];
        int[] R = new int[n2];

        /* Copy data to temp arrays */
        for (int i = 0; i < n1; ++i)
            L[i] = arr[l + i];
        for (int j = 0; j < n2; ++j)
            R[j] = arr[m + 1 + j];

        /* Merge the temp arrays */

        // Initial indexes of first and second subarrays
        int i = 0, j = 0;

        // Initial index of merged subarray
        int k = l;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            }
            else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        /* Copy remaining elements of L[] if any */
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        /* Copy remaining elements of R[] if any */
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    // Main function that sorts arr[l..r] using merge()
    public static void mergeSort(int[] arr, int l, int r) {
        if (l < r) {
            // Find the middle point
            int m = l + (r - l) / 2;

            // Sort first and second halves
            mergeSort(arr, l, m);
            mergeSort(arr, m + 1, r);

            // Merge the sorted halves
            merge(arr, l, m, r);
        }
    }

    // Utility method to print the array
    public static void printArray(int[] arr) {
        for (int num : arr)
            System.out.print(num + " ");
        System.out.println();
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {38, 27, 43, 3, 9, 82, 10};
        System.out.println("Original array:");
        printArray(arr);

        mergeSort(arr, 0, arr.length - 1);

        System.out.println("Sorted array:");
        printArray(arr);
        // Output:
        // Original array:
        // 38 27 43 3 9 82 10 
        // Sorted array:
        // 3 9 10 27 38 43 82 
    }
}
```

**Time Complexity:**
- **Best Case:** O(n log n)
- **Average Case:** O(n log n)
- **Worst Case:** O(n log n)

**Space Complexity:** O(n) (additional space for temporary arrays)

**When to Use:**
- Efficient for large datasets.
- Suitable for linked lists and external sorting (sorting data that doesn't fit into memory).

---

#### **1.5 Quick Sort**

**Overview:**
Quick Sort is another divide-and-conquer algorithm that selects a 'pivot' element and partitions the array around the pivot, ensuring that elements less than the pivot are on its left, and those greater are on its right. It then recursively applies the same strategy to the subarrays.

**How It Works:**
- **Choose a Pivot:** Select an element as the pivot (commonly the last element).
- **Partitioning:** Rearrange the array so that all elements less than the pivot come before it, and all greater elements come after it.
- **Recursion:** Apply the same process to the left and right subarrays.

**Example:**
Sort the array `[10, 7, 8, 9, 1, 5]` in ascending order.

**Steps:**
1. Choose pivot as 5.
2. Partition the array: `[1, 5, 8, 9, 10, 7]`
3. Recursively sort `[1]` and `[8, 9, 10, 7]`
4. Choose pivot as 7 for the second subarray.
5. Partition: `[1, 5, 7, 9, 10, 8]`
6. Recursively sort `[1, 5, 7]` and `[9, 10, 8]`
7. Continue until fully sorted: `[1, 5, 7, 8, 9, 10]`

**Java Implementation:**

```java
public class QuickSort {
    // Function to perform Quick Sort
    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            // pi is partitioning index, arr[pi] is now at right place
            int pi = partition(arr, low, high);

            // Recursively sort elements before and after partition
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }

    // This function takes last element as pivot, places it at correct position, and places smaller to left and greater to right
    private static int partition(int[] arr, int low, int high) {
        int pivot = arr[high];
        int i = (low - 1); // Index of smaller element

        for (int j = low; j <= high - 1; j++) {
            // If current element is smaller than or equal to pivot
            if (arr[j] <= pivot) {
                i++; // Increment index of smaller element
                swap(arr, i, j);
            }
        }
        swap(arr, i + 1, high);
        return (i + 1);
    }

    // Utility method to swap two elements in the array
    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Utility method to print the array
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

        quickSort(arr, 0, arr.length - 1);

        System.out.println("Sorted array:");
        printArray(arr);
        // Output:
        // Original array:
        // 10 7 8 9 1 5 
        // Sorted array:
        // 1 5 7 8 9 10 
    }
}
```

**Time Complexity:**
- **Best Case:** O(n log n)
- **Average Case:** O(n log n)
- **Worst Case:** O(n²) (when the smallest or largest element is always chosen as the pivot)

**Space Complexity:** O(log n) (due to recursion stack)

**When to Use:**
- Efficient for large datasets.
- In-place sorting with lower space requirements compared to Merge Sort.
- Preferred when average performance is crucial and worst-case scenarios are rare or handled.

---

#### **1.6 Heap Sort**

**Overview:**
Heap Sort is a comparison-based sorting algorithm that utilizes a binary heap data structure. It can be thought of as an improved selection sort that uses the heap to find the maximum or minimum element efficiently.

**How It Works:**
- **Build a Heap:** Convert the array into a max-heap (for ascending order sort).
- **Extract Elements:** Repeatedly remove the largest element from the heap and place it at the end of the array.
- **Heapify:** Restore the heap property after each extraction.

**Example:**
Sort the array `[12, 11, 13, 5, 6, 7]` in ascending order.

**Steps:**
1. Build a max-heap: `[13, 12, 7, 5, 6, 11]`
2. Swap the first element with the last: `[11, 12, 7, 5, 6, 13]`
3. Heapify the reduced heap `[11, 12, 7, 5, 6]`: `[12, 11, 7, 5, 6, 13]`
4. Repeat until the array is sorted: `[5, 6, 7, 11, 12, 13]`

**Java Implementation:**

```java
public class HeapSort {
    // Main function to sort an array using Heap Sort
    public static void heapSort(int[] arr) {
        int n = arr.length;

        // Build a maxheap
        for (int i = n / 2 - 1; i >= 0; i--)
            heapify(arr, n, i);

        // One by one extract elements from heap
        for (int i = n - 1; i > 0; i--) {
            // Move current root (largest) to end
            swap(arr, 0, i);

            // Call heapify on the reduced heap
            heapify(arr, i, 0);
        }
    }

    // To heapify a subtree rooted with node i which is an index in arr[] and n is size of heap
    private static void heapify(int[] arr, int n, int i) {
        int largest = i;        // Initialize largest as root
        int left = 2 * i + 1;   // left child index
        int right = 2 * i + 2;  // right child index

        // If left child is larger than root
        if (left < n && arr[left] > arr[largest])
            largest = left;

        // If right child is larger than largest so far
        if (right < n && arr[right] > arr[largest])
            largest = right;

        // If largest is not root
        if (largest != i) {
            swap(arr, i, largest);

            // Recursively heapify the affected sub-tree
            heapify(arr, n, largest);
        }
    }

    // Utility method to swap two elements in the array
    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Utility method to print the array
    public static void printArray(int[] arr) {
        for (int num : arr)
            System.out.print(num + " ");
        System.out.println();
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {12, 11, 13, 5, 6, 7};
        System.out.println("Original array:");
        printArray(arr);

        heapSort(arr);

        System.out.println("Sorted array:");
        printArray(arr);
        // Output:
        // Original array:
        // 12 11 13 5 6 7 
        // Sorted array:
        // 5 6 7 11 12 13 
    }
}
```

**Time Complexity:**
- **Best Case:** O(n log n)
- **Average Case:** O(n log n)
- **Worst Case:** O(n log n)

**Space Complexity:** O(1) (in-place sorting)

**When to Use:**
- Efficient for large datasets.
- Suitable when space is limited since it sorts in place.
- Preferred when consistent performance is needed regardless of input data.

---

#### **1.7 Counting Sort**

**Overview:**
Counting Sort is a non-comparison-based sorting algorithm that works by counting the number of objects that have distinct key values. It is efficient when the range of input data (k) is not significantly greater than the number of objects to be sorted (n).

**How It Works:**
- **Count Occurrences:** Count the number of occurrences of each unique element.
- **Cumulative Count:** Modify the count array to store the cumulative count.
- **Place Elements:** Place the elements into the output array based on the cumulative count.

**Example:**
Sort the array `[4, 2, 2, 8, 3, 3, 1]` in ascending order.

**Steps:**
1. Find the maximum element (8).
2. Create a count array of size `max + 1 = 9`: `[0, 0, 0, 0, 0, 0, 0, 0, 0]`
3. Count occurrences:
   - Increment count[4], count[2], count[2], count[8], count[3], count[3], count[1]
   - Count array: `[0, 1, 2, 2, 1, 0, 0, 0, 1]`
4. Cumulative count:
   - `[0, 1, 3, 5, 6, 6, 6, 6, 7]`
5. Place elements into output array using the cumulative count:
   - Output: `[1, 2, 2, 3, 3, 4, 8]`

**Java Implementation:**

```java
import java.util.Arrays;

public class CountingSort {
    public static void countingSort(int[] arr) {
        int n = arr.length;

        // Find the maximum element to know the range of count array
        int max = Arrays.stream(arr).max().getAsInt();

        // Initialize count array
        int[] count = new int[max + 1];

        // Store the count of each element
        for (int num : arr)
            count[num]++;

        // Modify the count array by adding the previous counts (cumulative count)
        for (int i = 1; i <= max; i++)
            count[i] += count[i - 1];

        // Build the output array
        int[] output = new int[n];
        // To make it stable, iterate from end
        for (int i = n - 1; i >= 0; i--) {
            output[count[arr[i]] - 1] = arr[i];
            count[arr[i]]--;
        }

        // Copy the sorted elements back to original array
        System.arraycopy(output, 0, arr, 0, n);
    }

    // Utility method to print the array
    public static void printArray(int[] arr) {
        for (int num : arr)
            System.out.print(num + " ");
        System.out.println();
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {4, 2, 2, 8, 3, 3, 1};
        System.out.println("Original array:");
        printArray(arr);

        countingSort(arr);

        System.out.println("Sorted array:");
        printArray(arr);
        // Output:
        // Original array:
        // 4 2 2 8 3 3 1 
        // Sorted array:
        // 1 2 2 3 3 4 8 
    }
}
```

**Time Complexity:**
- **Best Case:** O(n + k)
- **Average Case:** O(n + k)
- **Worst Case:** O(n + k)

**Space Complexity:** O(n + k) (additional space for count and output arrays)

**When to Use:**
- When the range of input data (k) is not significantly larger than the number of elements (n).
- Suitable for sorting integers or objects with integer keys.
- Not ideal for sorting data with a large range of key values due to high space requirements.

---

#### **1.8 Radix Sort**

**Overview:**
Radix Sort is a non-comparison-based sorting algorithm that sorts numbers digit by digit, starting from the least significant digit to the most significant digit (LSD). It leverages Counting Sort as a subroutine to sort digits.

**How It Works:**
- **Determine the maximum number** to know the number of digits.
- **Iterate through each digit** from least significant to most significant.
- **Use Counting Sort** to sort based on the current digit.

**Example:**
Sort the array `[170, 45, 75, 90, 802, 24, 2, 66]` in ascending order.

**Steps:**
1. Maximum number is 802, which has 3 digits.
2. **First Pass (Ones place):**
   - Sort based on the digit in the ones place.
   - Sorted array: `[170, 90, 802, 2, 24, 45, 75, 66]`
3. **Second Pass (Tens place):**
   - Sort based on the digit in the tens place.
   - Sorted array: `[170, 90, 802, 2, 24, 45, 75, 66]` → `[170, 90, 802, 2, 24, 45, 66, 75]`
4. **Third Pass (Hundreds place):**
   - Sort based on the digit in the hundreds place.
   - Sorted array: `[2, 24, 45, 66, 75, 90, 170, 802]`

**Java Implementation:**

```java
public class RadixSort {
    // A utility function to get maximum value in arr[]
    private static int getMax(int[] arr) {
        int max = arr[0];
        for (int num : arr)
            if (num > max)
                max = num;
        return max;
    }

    // A function to do counting sort of arr[] according to the digit represented by exp
    private static void countingSort(int[] arr, int exp) {
        int n = arr.length;
        int[] output = new int[n]; // Output array
        int[] count = new int[10];
        Arrays.fill(count, 0);

        // Store count of occurrences in count[]
        for (int num : arr)
            count[(num / exp) % 10]++;

        // Change count[i] so that count[i] contains the actual position of this digit in output[]
        for (int i = 1; i < 10; i++)
            count[i] += count[i - 1];

        // Build the output array by traversing from end to maintain stability
        for (int i = n - 1; i >= 0; i--) {
            int digit = (arr[i] / exp) % 10;
            output[count[digit] - 1] = arr[i];
            count[digit]--;
        }

        // Copy the output array to arr[], so that arr[] now contains sorted numbers according to current digit
        System.arraycopy(output, 0, arr, 0, n);
    }

    // The main function to sort arr[] using Radix Sort
    public static void radixSort(int[] arr) {
        // Find the maximum number to know the number of digits
        int m = getMax(arr);

        // Do counting sort for every digit. Note that instead of passing digit number, exp is passed
        // which is 10^i where i is current digit number
        for (int exp = 1; m / exp > 0; exp *= 10)
            countingSort(arr, exp);
    }

    // Utility method to print the array
    public static void printArray(int[] arr) {
        for (int num : arr)
            System.out.print(num + " ");
        System.out.println();
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {170, 45, 75, 90, 802, 24, 2, 66};
        System.out.println("Original array:");
        printArray(arr);

        radixSort(arr);

        System.out.println("Sorted array:");
        printArray(arr);
        // Output:
        // Original array:
        // 170 45 75 90 802 24 2 66 
        // Sorted array:
        // 2 24 45 66 75 90 170 802 
    }
}
```

**Time Complexity:**
- **Best Case:** O(nk)
- **Average Case:** O(nk)
- **Worst Case:** O(nk)
  - Where `n` is the number of elements and `k` is the number of digits in the largest number.

**Space Complexity:** O(n + k) (additional space for output and count arrays)

**When to Use:**
- Effective for sorting large numbers where the number of digits (`k`) is not significantly large.
- Suitable for data with fixed-length keys or where the range of keys is large but the number of digits is small.

---

### **2. Searching Algorithms**

Searching algorithms are used to find specific elements within data structures. Efficient searching is critical for performance optimization in applications such as databases, operating systems, and web services.

#### **2.1 Linear Search**

**Overview:**
Linear Search is the simplest searching algorithm that checks every element in the list until the desired element is found or the list ends.

**How It Works:**
- Start from the first element.
- Compare each element with the target.
- If a match is found, return the index.
- If the end of the list is reached without finding the target, return -1.

**Example:**
Search for the number `5` in the array `[1, 3, 5, 7, 9]`.

**Steps:**
1. Compare 1 with 5 → not a match.
2. Compare 3 with 5 → not a match.
3. Compare 5 with 5 → match found at index 2.

**Java Implementation:**

```java
public class LinearSearch {
    // Function to perform linear search
    public static int linearSearch(int[] arr, int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target)
                return i; // Return the index if target is found
        }
        return -1; // Return -1 if target is not found
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {1, 3, 5, 7, 9};
        int target = 5;

        int result = linearSearch(arr, target);

        if (result != -1)
            System.out.println("Element " + target + " found at index " + result);
        else
            System.out.println("Element " + target + " not found in the array.");
        // Output:
        // Element 5 found at index 2
    }
}
```

**Time Complexity:**
- **Best Case:** O(1) (if the target is the first element)
- **Average Case:** O(n)
- **Worst Case:** O(n) (if the target is the last element or not present)

**Space Complexity:** O(1) (no additional space required)

**When to Use:**
- Suitable for small or unsorted datasets.
- When simplicity is more important than efficiency.

---

#### **2.2 Binary Search and Variants**

**Overview:**
Binary Search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing the search interval in half, comparing the target value to the middle element of the interval.

**How It Works:**
- Start with the entire array.
- Find the middle element.
- If the middle element is the target, return its index.
- If the target is less than the middle element, repeat the search on the left subarray.
- If the target is greater, repeat the search on the right subarray.
- Continue until the target is found or the subarray size becomes zero.

**Example:**
Search for the number `7` in the sorted array `[1, 3, 5, 7, 9]`.

**Steps:**
1. Middle element is `5` at index `2`.
2. `7` > `5`, search in the right subarray `[7, 9]`.
3. Middle element is `7` at index `3`.
4. `7` == `7`, target found at index `3`.

**Java Implementation:**

```java
public class BinarySearch {
    // Iterative Binary Search
    public static int binarySearchIterative(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            // Check if target is present at mid
            if (arr[mid] == target)
                return mid;

            // If target greater, ignore left half
            if (arr[mid] < target)
                left = mid + 1;

            // If target is smaller, ignore right half
            else
                right = mid - 1;
        }

        // Target not found
        return -1;
    }

    // Recursive Binary Search
    public static int binarySearchRecursive(int[] arr, int target, int left, int right) {
        if (left > right)
            return -1; // Base case: target not found

        int mid = left + (right - left) / 2;

        // Check if target is present at mid
        if (arr[mid] == target)
            return mid;

        // If target greater, ignore left half
        if (arr[mid] < target)
            return binarySearchRecursive(arr, target, mid + 1, right);

        // If target is smaller, ignore right half
        return binarySearchRecursive(arr, target, left, mid - 1);
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {1, 3, 5, 7, 9};
        int target = 7;

        // Iterative Binary Search
        int resultIterative = binarySearchIterative(arr, target);
        if (resultIterative != -1)
            System.out.println("Element " + target + " found at index " + resultIterative + " using Iterative Binary Search.");
        else
            System.out.println("Element " + target + " not found in the array using Iterative Binary Search.");

        // Recursive Binary Search
        int resultRecursive = binarySearchRecursive(arr, target, 0, arr.length - 1);
        if (resultRecursive != -1)
            System.out.println("Element " + target + " found at index " + resultRecursive + " using Recursive Binary Search.");
        else
            System.out.println("Element " + target + " not found in the array using Recursive Binary Search.");
        // Output:
        // Element 7 found at index 3 using Iterative Binary Search.
        // Element 7 found at index 3 using Recursive Binary Search.
    }
}
```

**Time Complexity:**
- **Best Case:** O(1) (if the target is the middle element)
- **Average Case:** O(log n)
- **Worst Case:** O(log n)

**Space Complexity:**
- **Iterative:** O(1)
- **Recursive:** O(log n) (due to recursion stack)

**When to Use:**
- Efficient for large, sorted datasets.
- Preferred when search operations are frequent and the dataset is static or rarely changes.

**Variants of Binary Search:**

1. **Finding the First Occurrence:**
   - Useful when there are duplicate elements.
   - Modify the algorithm to continue searching in the left subarray even after finding the target.

2. **Finding the Last Occurrence:**
   - Similar to finding the first occurrence but search in the right subarray after finding the target.

3. **Finding the Insert Position:**
   - Determine where a target should be inserted in a sorted array to maintain order.

**Java Implementation for Finding First and Last Occurrence:**

```java
public class BinarySearchVariants {
    // Find the first occurrence of target
    public static int firstOccurrence(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;
        int result = -1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] == target) {
                result = mid;
                right = mid - 1; // Continue searching in the left half
            }
            else if (arr[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }

        return result;
    }

    // Find the last occurrence of target
    public static int lastOccurrence(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;
        int result = -1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] == target) {
                result = mid;
                left = mid + 1; // Continue searching in the right half
            }
            else if (arr[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }

        return result;
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {1, 2, 2, 2, 3, 4, 5};
        int target = 2;

        int first = firstOccurrence(arr, target);
        int last = lastOccurrence(arr, target);

        System.out.println("First occurrence of " + target + " is at index " + first);
        System.out.println("Last occurrence of " + target + " is at index " + last);
        // Output:
        // First occurrence of 2 is at index 1
        // Last occurrence of 2 is at index 3
    }
}
```

---

## **Summary of Week 1: Sorting and Searching Algorithms**

In this week, you've explored various sorting algorithms, understanding how they work, their implementations in Java, and their time and space complexities. You also delved into searching algorithms, particularly Linear Search and Binary Search, learning how to implement them and understand their efficiencies.

### **Key Takeaways:**
- **Sorting Algorithms:** Understand the differences between simple sorting algorithms (Bubble, Selection, Insertion) and more efficient ones (Merge, Quick, Heap, Counting, Radix).
- **Choosing the Right Sort:** Selection of sorting algorithms depends on the dataset size, whether it's partially sorted, and memory constraints.
- **Searching Algorithms:** Linear Search is straightforward but inefficient for large datasets, whereas Binary Search offers logarithmic time complexity but requires a sorted array.
- **Implementations:** Mastery of implementing these algorithms in Java enhances your problem-solving toolkit for technical interviews.

### **Exercises:**

1. **Bubble Sort:**
   - Modify the Bubble Sort implementation to sort the array in descending order.
   - Analyze how the number of swaps changes with different input arrays.

2. **Selection Sort:**
   - Implement a version of Selection Sort that sorts strings lexicographically.
   - Compare the performance of Selection Sort with Bubble Sort on large datasets.

3. **Insertion Sort:**
   - Implement Insertion Sort for a linked list instead of an array.
   - Explore how Insertion Sort can be used to sort a deck of playing cards.

4. **Merge Sort:**
   - Implement Merge Sort to sort a linked list.
   - Analyze the space complexity of Merge Sort and discuss ways to optimize it.

5. **Quick Sort:**
   - Implement Quick Sort with a randomized pivot to improve performance on average.
   - Discuss the scenarios where Quick Sort might perform poorly and how to mitigate them.

6. **Heap Sort:**
   - Modify Heap Sort to sort an array of objects based on a specific attribute.
   - Compare Heap Sort with Merge Sort in terms of performance and space usage.

7. **Counting Sort:**
   - Implement Counting Sort for sorting characters in a string.
   - Discuss the limitations of Counting Sort when dealing with negative numbers.

8. **Radix Sort:**
   - Extend Radix Sort to sort floating-point numbers.
   - Explore how Radix Sort can be adapted to sort strings.

9. **Linear Search:**
   - Implement a Linear Search that returns all indices where the target is found.
   - Compare the performance of Linear Search and Binary Search on unsorted and sorted arrays.

10. **Binary Search Variants:**
    - Implement a function to find the first missing positive integer in a sorted array using Binary Search.
    - Use Binary Search to find the square root of a number up to a specified precision.

---

## **Week 2: Recursion, Backtracking, and Dynamic Programming**

### **3. Recursion and Backtracking**

Recursion is a method of solving problems where the solution depends on solutions to smaller instances of the same problem. Backtracking is a refined form of recursion used for solving constraint satisfaction problems by trying partial solutions and abandoning them if they do not lead to a valid solution.

#### **3.1 Recursive Problem Solving Techniques**

**Overview:**
Recursion involves functions calling themselves to break down complex problems into simpler subproblems. Understanding recursion is crucial for solving problems related to tree traversals, combinatorics, and more.

**How It Works:**
- **Base Case:** The condition under which the recursion stops.
- **Recursive Case:** The part of the function where it calls itself with a smaller or simpler input.

**Example: Calculating Factorial**

**Problem:**
Calculate the factorial of a number `n` (denoted as `n!`), which is the product of all positive integers up to `n`.

**Formula:**
- `n! = n * (n-1)!`
- `0! = 1` (Base Case)

**Java Implementation:**

```java
public class RecursionExample {
    // Recursive function to calculate factorial
    public static int factorial(int n) {
        if (n == 0) // Base case
            return 1;
        else
            return n * factorial(n - 1); // Recursive call
    }

    // Example usage
    public static void main(String[] args) {
        int num = 5;
        int result = factorial(num);
        System.out.println("Factorial of " + num + " is " + result);
        // Output: Factorial of 5 is 120
    }
}
```

**Explanation:**
- **Base Case:** When `n` is 0, return 1.
- **Recursive Case:** Multiply `n` by the factorial of `n-1`.

**Visualization:**
```
factorial(5)
= 5 * factorial(4)
= 5 * (4 * factorial(3))
= 5 * (4 * (3 * factorial(2)))
= 5 * (4 * (3 * (2 * factorial(1))))
= 5 * (4 * (3 * (2 * (1 * factorial(0)))))
= 5 * 4 * 3 * 2 * 1 * 1
= 120
```

**Time Complexity:** O(n)

**Space Complexity:** O(n) (due to recursion stack)

---

#### **3.2 Backtracking Algorithms (N-Queens, Sudoku Solver)**

**Overview:**
Backtracking is a technique for solving problems recursively by trying to build a solution incrementally and abandoning a solution (backtracking) as soon as it determines that the solution cannot be completed.

**How It Works:**
- **Choose:** Select a possible option.
- **Explore:** Recursively explore further options.
- **Unchoose:** If a solution is not possible, backtrack and try the next option.

**Example 1: N-Queens Problem**

**Problem:**
Place `N` queens on an `N×N` chessboard so that no two queens threaten each other (no two queens share the same row, column, or diagonal).

**Java Implementation:**

```java
public class NQueens {
    int N;

    public NQueens(int N) {
        this.N = N;
    }

    // Function to solve the N-Queens problem
    public void solveNQueens() {
        int[] queens = new int[N]; // queens[i] = column position of queen in row i
        placeQueens(queens, 0);
    }

    // Recursive function to place queens
    private void placeQueens(int[] queens, int row) {
        if (row == N) {
            printSolution(queens);
            return;
        }

        for (int col = 0; col < N; col++) {
            if (isSafe(queens, row, col)) {
                queens[row] = col; // Place queen
                placeQueens(queens, row + 1); // Recurse for next row
            }
        }
    }

    // Check if placing a queen at (row, col) is safe
    private boolean isSafe(int[] queens, int row, int col) {
        for (int i = 0; i < row; i++) {
            int placedCol = queens[i];
            // Check same column
            if (placedCol == col)
                return false;
            // Check diagonals
            if (Math.abs(placedCol - col) == Math.abs(i - row))
                return false;
        }
        return true;
    }

    // Print the board configuration
    private void printSolution(int[] queens) {
        for (int row = 0; row < N; row++) {
            for (int col = 0; col < N; col++) {
                if (queens[row] == col)
                    System.out.print("Q ");
                else
                    System.out.print(". ");
            }
            System.out.println();
        }
        System.out.println();
    }

    // Example usage
    public static void main(String[] args) {
        int N = 4;
        NQueens nq = new NQueens(N);
        nq.solveNQueens();
        /*
        Output:
        . Q . . 
        . . . Q 
        Q . . . 
        . . Q . 

        . . Q . 
        Q . . . 
        . . . Q 
        . Q . . 
        */
    }
}
```

**Explanation:**
- **Queens Array:** `queens[i]` represents the column position of the queen in row `i`.
- **isSafe Method:** Checks if placing a queen at a specific row and column is safe by ensuring no other queens threaten it.
- **Backtracking:** If a queen cannot be safely placed in any column of a row, the algorithm backtracks to the previous row and tries a different position.

**Time Complexity:** O(N!) (factorial time)

**Space Complexity:** O(N) (due to recursion stack and queens array)

---

**Example 2: Sudoku Solver**

**Problem:**
Fill a 9×9 Sudoku board so that each row, each column, and each of the nine 3×3 subgrids contain all digits from 1 to 9 exactly once.

**Java Implementation:**

```java
public class SudokuSolver {
    public boolean solveSudoku(char[][] board) {
        for (int row = 0; row < board.length; row++) {
            for (int col = 0; col < board[0].length; col++) {
                // Find an empty cell
                if (board[row][col] == '.') {
                    // Try digits 1-9
                    for (char num = '1'; num <= '9'; num++) {
                        if (isValid(board, row, col, num)) {
                            board[row][col] = num; // Place the number

                            // Recurse to solve the rest
                            if (solveSudoku(board))
                                return true;
                            else
                                board[row][col] = '.'; // Backtrack
                        }
                    }
                    return false; // Trigger backtracking
                }
            }
        }
        return true; // Solved
    }

    // Check if placing num at (row, col) is valid
    private boolean isValid(char[][] board, int row, int col, char num) {
        // Check row and column
        for (int i = 0; i < 9; i++) {
            if (board[row][i] == num || board[i][col] == num)
                return false;
        }

        // Check 3x3 subgrid
        int startRow = row - row % 3;
        int startCol = col - col % 3;
        for (int i = startRow; i < startRow + 3; i++)
            for (int j = startCol; j < startCol + 3; j++)
                if (board[i][j] == num)
                    return false;

        return true;
    }

    // Utility method to print the Sudoku board
    public void printBoard(char[][] board) {
        for (int row = 0; row < 9; row++) {
            if (row % 3 == 0 && row != 0)
                System.out.println("------+-------+------");
            for (int col = 0; col < 9; col++) {
                if (col % 3 == 0 && col != 0)
                    System.out.print("| ");
                System.out.print(board[row][col] + " ");
            }
            System.out.println();
        }
    }

    // Example usage
    public static void main(String[] args) {
        SudokuSolver solver = new SudokuSolver();
        char[][] board = {
            {'5','3','.','.','7','.','.','.','.'},
            {'6','.','.','1','9','5','.','.','.'},
            {'.','9','8','.','.','.','.','6','.'},
            {'8','.','.','.','6','.','.','.','3'},
            {'4','.','.','8','.','3','.','.','1'},
            {'7','.','.','.','2','.','.','.','6'},
            {'.','6','.','.','.','.','2','8','.'},
            {'.','.','.','4','1','9','.','.','5'},
            {'.','.','.','.','8','.','.','7','9'}
        };

        System.out.println("Original Sudoku Board:");
        solver.printBoard(board);

        if (solver.solveSudoku(board)) {
            System.out.println("\nSolved Sudoku Board:");
            solver.printBoard(board);
        } else {
            System.out.println("No solution exists.");
        }
    }
}
```

**Explanation:**
- **Backtracking Approach:** The solver tries to place digits 1-9 in empty cells, checking for validity. If a placement leads to a dead end, it backtracks and tries a different digit.
- **isValid Method:** Ensures that placing a digit doesn't violate Sudoku rules in the current row, column, or 3×3 subgrid.
- **Termination:** The algorithm terminates when all cells are filled correctly or determines that no solution exists.

**Time Complexity:** O(9^(n)) where `n` is the number of empty cells.

**Space Complexity:** O(n) (due to recursion stack)

---

### **4. Dynamic Programming**

Dynamic Programming (DP) is a method for solving complex problems by breaking them down into simpler subproblems. It is applicable when the problem exhibits overlapping subproblems and optimal substructure properties.

#### **4.1 Principles of Optimal Substructure and Overlapping Subproblems**

**Optimal Substructure:**
A problem has an optimal substructure if an optimal solution to the problem contains optimal solutions to its subproblems.

**Overlapping Subproblems:**
A problem has overlapping subproblems if the same subproblems are solved multiple times during the computation.

**Example: Fibonacci Sequence**

Calculating the nth Fibonacci number is a classic example where both optimal substructure and overlapping subproblems are present.

**Recursive Definition:**
- `fib(n) = fib(n-1) + fib(n-2)`
- `fib(0) = 0`
- `fib(1) = 1`

**Dynamic Programming Approach:**
Store the results of subproblems to avoid redundant calculations.

**Java Implementation:**

```java
public class FibonacciDP {
    // Recursive approach without memoization
    public static int fibRecursive(int n) {
        if (n <= 1)
            return n;
        return fibRecursive(n - 1) + fibRecursive(n - 2);
    }

    // Dynamic Programming approach using memoization
    public static int fibMemoization(int n, int[] memo) {
        if (n <= 1)
            return n;
        if (memo[n] != -1)
            return memo[n];
        memo[n] = fibMemoization(n - 1, memo) + fibMemoization(n - 2, memo);
        return memo[n];
    }

    // Dynamic Programming approach using tabulation
    public static int fibTabulation(int n) {
        if (n <= 1)
            return n;
        int[] table = new int[n + 1];
        table[0] = 0;
        table[1] = 1;
        for (int i = 2; i <= n; i++)
            table[i] = table[i - 1] + table[i - 2];
        return table[n];
    }

    // Example usage
    public static void main(String[] args) {
        int n = 10;

        // Recursive approach
        System.out.println("Fibonacci number (Recursive) for n = " + n + " is " + fibRecursive(n));

        // Dynamic Programming with memoization
        int[] memo = new int[n + 1];
        Arrays.fill(memo, -1);
        System.out.println("Fibonacci number (Memoization) for n = " + n + " is " + fibMemoization(n, memo));

        // Dynamic Programming with tabulation
        System.out.println("Fibonacci number (Tabulation) for n = " + n + " is " + fibTabulation(n));
        // Output:
        // Fibonacci number (Recursive) for n = 10 is 55
        // Fibonacci number (Memoization) for n = 10 is 55
        // Fibonacci number (Tabulation) for n = 10 is 55
    }
}
```

**Explanation:**
- **Recursive Approach:** Solves the problem by breaking it down into subproblems but has exponential time complexity due to redundant calculations.
- **Memoization:** Stores the results of subproblems in an array (`memo`) to avoid recalculating them, reducing time complexity to O(n).
- **Tabulation:** Builds up the solution iteratively from the base cases, also achieving O(n) time complexity.

**Advantages of DP:**
- Efficiently solves problems with overlapping subproblems and optimal substructure.
- Reduces time complexity by storing and reusing subproblem results.

---

#### **4.2 Memoization and Tabulation Techniques**

**Memoization:**
Memoization is a top-down approach where you solve the problem recursively and store the results of subproblems to avoid redundant computations.

**Example: Memoized Fibonacci**

(Refer to the `fibMemoization` method in the previous section.)

**Tabulation:**
Tabulation is a bottom-up approach where you iteratively solve all subproblems and store their results, building up to the final solution.

**Example: Tabulated Fibonacci**

(Refer to the `fibTabulation` method in the previous section.)

**Java Implementation: Fibonacci with Both Techniques**

(Refer to the `FibonacciDP` class in the previous section.)

---

#### **4.3 Classic DP Problems (Knapsack, Longest Common Subsequence)**

**Example 1: Knapsack Problem**

**Problem:**
Given a set of items, each with a weight and a value, determine the number of each item to include in a collection so that the total weight is less than or equal to a given limit and the total value is as large as possible.

**Types:**
- **0/1 Knapsack:** Each item can be included at most once.
- **Unbounded Knapsack:** Each item can be included multiple times.

**Java Implementation: 0/1 Knapsack**

```java
public class Knapsack {
    // Function to solve 0/1 Knapsack problem using DP
    public static int knapsack(int W, int[] weights, int[] values, int n) {
        int[][] dp = new int[n + 1][W + 1];

        // Build table dp[][] in bottom-up manner
        for (int i = 0; i <= n; i++) {
            for (int w = 0; w <= W; w++) {
                if (i == 0 || w == 0)
                    dp[i][w] = 0;
                else if (weights[i - 1] <= w)
                    dp[i][w] = Math.max(values[i - 1] + dp[i - 1][w - weights[i - 1]],
                                        dp[i - 1][w]);
                else
                    dp[i][w] = dp[i - 1][w];
            }
        }

        return dp[n][W];
    }

    // Example usage
    public static void main(String[] args) {
        int[] values = {60, 100, 120};
        int[] weights = {10, 20, 30};
        int W = 50;
        int n = values.length;

        int maxValue = knapsack(W, weights, values, n);
        System.out.println("Maximum value in Knapsack = " + maxValue);
        // Output: Maximum value in Knapsack = 220
    }
}
```

**Explanation:**
- **DP Table:** `dp[i][w]` represents the maximum value achievable with the first `i` items and a weight limit `w`.
- **Decision:** For each item, decide whether to include it or not based on its weight and value.

**Time Complexity:** O(nW)

**Space Complexity:** O(nW)

**Example 2: Longest Common Subsequence (LCS)**

**Problem:**
Given two sequences, find the length of the longest subsequence present in both of them. A subsequence is a sequence that appears in the same relative order but not necessarily contiguous.

**Java Implementation:**

```java
public class LongestCommonSubsequence {
    // Function to find LCS using DP
    public static int lcs(String X, String Y) {
        int m = X.length();
        int n = Y.length();
        int[][] dp = new int[m + 1][n + 1];

        // Build the dp table from bottom up
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0 || j == 0)
                    dp[i][j] = 0;
                else if (X.charAt(i - 1) == Y.charAt(j - 1))
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                else
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
            }
        }

        return dp[m][n];
    }

    // Example usage
    public static void main(String[] args) {
        String X = "AGGTAB";
        String Y = "GXTXAYB";
        System.out.println("Length of LCS is " + lcs(X, Y));
        // Output: Length of LCS is 4
    }
}
```

**Explanation:**
- **DP Table:** `dp[i][j]` represents the length of LCS of `X[0..i-1]` and `Y[0..j-1]`.
- **Decision:** If characters match, extend the LCS; otherwise, take the maximum from previous subproblems.

**Time Complexity:** O(mn)

**Space Complexity:** O(mn)

---

## **Summary of Week 2: Recursion, Backtracking, and Dynamic Programming**

In this week, you've delved into the powerful techniques of Recursion and Backtracking, mastering how to solve problems by breaking them down into simpler subproblems and exploring possible solutions systematically. You also explored Dynamic Programming, learning how to optimize recursive solutions by storing and reusing results of subproblems. Through classic problems like the N-Queens, Sudoku Solver, Knapsack, and Longest Common Subsequence, you've built a robust foundation in algorithm design and problem-solving.

### **Key Takeaways:**
- **Recursion:** Understand how to approach problems by defining base and recursive cases.
- **Backtracking:** Learn to explore all possible solutions and backtrack when a partial solution cannot lead to a valid outcome.
- **Dynamic Programming:** Master the principles of optimal substructure and overlapping subproblems to optimize recursive solutions using memoization and tabulation.
- **Classic Problems:** Gain hands-on experience by implementing solutions to well-known problems, enhancing your problem-solving skills.

### **Exercises:**

1. **Recursion:**
   - Implement a recursive function to generate all permutations of a string.
   - Solve the Tower of Hanoi problem using recursion and visualize the moves.

2. **Backtracking:**
   - Extend the N-Queens problem to display all possible solutions for a given `N`.
   - Implement a backtracking algorithm to solve the Knight’s Tour problem on a chessboard.

3. **Dynamic Programming:**
   - Implement the Coin Change problem using both memoization and tabulation.
   - Solve the Edit Distance problem, determining the minimum number of operations required to convert one string into another.

4. **Knapsack Problem:**
   - Modify the 0/1 Knapsack implementation to return the list of items included in the optimal solution.
   - Implement the Unbounded Knapsack problem where each item can be selected multiple times.

5. **Longest Common Subsequence:**
   - Extend the LCS implementation to return the actual subsequence, not just its length.
   - Solve the Shortest Common Supersequence problem using Dynamic Programming.

6. **Combination of Techniques:**
   - Use backtracking to solve the Subset Sum problem and then optimize it using Dynamic Programming.
   - Implement a memoized solution for the Fibonacci sequence and compare its performance with the recursive approach.

---

## **Week 3: Greedy Algorithms and Divide and Conquer**

### **5. Greedy Algorithms**

Greedy algorithms build up a solution piece by piece, always choosing the next piece that offers the most immediate benefit. While they do not always provide the optimal solution for all problems, they are efficient and work well for problems where greedy choices lead to an optimal solution.

#### **5.1 Greedy Choice Property**

**Overview:**
The Greedy Choice Property ensures that a locally optimal choice at each step leads to a globally optimal solution. Understanding when a problem possesses this property is crucial for applying greedy algorithms effectively.

**Example: Activity Selection Problem**

**Problem:**
Given a set of activities with start and finish times, select the maximum number of activities that don't overlap.

**How It Works:**
- Sort activities by their finish times.
- Select the first activity.
- For each subsequent activity, if its start time is after or equal to the finish time of the last selected activity, select it.

**Java Implementation:**

```java
import java.util.Arrays;
import java.util.Comparator;

public class ActivitySelection {
    // Activity class
    static class Activity {
        int start;
        int finish;

        Activity(int start, int finish) {
            this.start = start;
            this.finish = finish;
        }

        @Override
        public String toString() {
            return "(" + start + ", " + finish + ")";
        }
    }

    // Function to select maximum number of activities
    public static void selectActivities(Activity[] activities) {
        // Sort activities based on finish time
        Arrays.sort(activities, Comparator.comparingInt(a -> a.finish));

        System.out.println("Selected activities:");
        // The first activity is always selected
        int lastSelected = 0;
        System.out.println(activities[lastSelected]);

        // Iterate through remaining activities
        for (int i = 1; i < activities.length; i++) {
            if (activities[i].start >= activities[lastSelected].finish) {
                System.out.println(activities[i]);
                lastSelected = i;
            }
        }
    }

    // Example usage
    public static void main(String[] args) {
        Activity[] activities = {
            new Activity(1, 4),
            new Activity(3, 5),
            new Activity(0, 6),
            new Activity(5, 7),
            new Activity(3, 9),
            new Activity(5, 9),
            new Activity(6, 10),
            new Activity(8, 11),
            new Activity(8, 12),
            new Activity(2, 13),
            new Activity(12, 14)
        };

        selectActivities(activities);
        /*
        Output:
        Selected activities:
        (1, 4)
        (5, 7)
        (8, 11)
        (12, 14)
        */
    }
}
```

**Explanation:**
- **Sorting:** Activities are sorted based on their finish times to ensure that selecting the earliest finishing activity leaves maximum room for subsequent activities.
- **Selection:** Start with the first activity and select subsequent activities that start after or at the finish time of the last selected activity.

**Time Complexity:** O(n log n) due to sorting.

**Space Complexity:** O(1) (excluding space used for sorting)

---

**Example 2: Huffman Coding**

**Problem:**
Huffman Coding is a compression algorithm that assigns variable-length codes to characters based on their frequencies. Characters with higher frequencies are assigned shorter codes, resulting in efficient data compression.

**Java Implementation:**

```java
import java.util.PriorityQueue;

public class HuffmanCoding {
    // Huffman tree node
    static class Node implements Comparable<Node> {
        char data;
        int freq;
        Node left, right;

        Node(char data, int freq) {
            this.data = data;
            this.freq = freq;
            left = right = null;
        }

        // Compare nodes based on frequency
        public int compareTo(Node o) {
            return this.freq - o.freq;
        }
    }

    // Function to build Huffman Tree
    public static Node buildHuffmanTree(char[] data, int[] freq) {
        PriorityQueue<Node> pq = new PriorityQueue<>();

        // Create leaf nodes and add to priority queue
        for (int i = 0; i < data.length; i++)
            pq.add(new Node(data[i], freq[i]));

        // Iterate until the queue has only one node
        while (pq.size() > 1) {
            // Remove two nodes with the lowest frequency
            Node left = pq.poll();
            Node right = pq.poll();

            // Create a new internal node with these two nodes as children
            // and with frequency equal to the sum of the two nodes
            Node sum = new Node('-', left.freq + right.freq);
            sum.left = left;
            sum.right = right;
            pq.add(sum);
        }

        // The remaining node is the root of the Huffman Tree
        return pq.poll();
    }

    // Function to print Huffman codes
    public static void printCodes(Node root, String s) {
        if (root.left == null && root.right == null && Character.isLetter(root.data)) {
            System.out.println(root.data + ": " + s);
            return;
        }
        if (root.left != null)
            printCodes(root.left, s + "0");
        if (root.right != null)
            printCodes(root.right, s + "1");
    }

    // Example usage
    public static void main(String[] args) {
        char[] data = {'a', 'b', 'c', 'd', 'e', 'f'};
        int[] freq = {5, 9, 12, 13, 16, 45};

        Node root = buildHuffmanTree(data, freq);

        System.out.println("Huffman Codes:");
        printCodes(root, "");
        /*
        Output:
        a: 1100
        b: 1101
        c: 100
        d: 101
        e: 111
        f: 0
        */
    }
}
```

**Explanation:**
- **Node Class:** Represents each character and its frequency. Internal nodes have a frequency that is the sum of their children's frequencies.
- **Priority Queue:** Ensures that the two nodes with the lowest frequencies are always selected first to build the tree.
- **Huffman Codes:** Traverse the tree from root to leaves, assigning '0' for left edges and '1' for right edges. The path to each leaf node represents its unique code.

**Time Complexity:** O(n log n) due to the priority queue operations.

**Space Complexity:** O(n) (for storing the Huffman Tree)

---

## **Summary of Week 3: Greedy Algorithms and Divide and Conquer**

This week, you explored Greedy Algorithms and the Divide and Conquer paradigm, two fundamental strategies for designing efficient algorithms. Greedy algorithms make the optimal choice at each step with the hope of finding the global optimum, while Divide and Conquer breaks down problems into smaller, manageable subproblems, solves them independently, and combines their solutions.

### **Key Takeaways:**
- **Greedy Algorithms:** Understand how making locally optimal choices can lead to globally optimal solutions for specific problems.
- **Common Greedy Problems:** Master problems like Activity Selection and Huffman Coding, which effectively utilize greedy strategies.
- **Divide and Conquer:** Learn how to decompose problems, solve subproblems recursively, and combine solutions, enhancing your ability to tackle complex tasks.
- **Master Theorem:** Grasp the Master Theorem to analyze the time complexity of Divide and Conquer algorithms.
- **Real-World Applications:** Recognize how these algorithms are applied in various domains, from data compression to computational geometry.

### **Exercises:**

1. **Greedy Algorithms:**
   - Implement the Greedy algorithm for the Coin Change problem and discuss its limitations.
   - Solve the Fractional Knapsack problem using a Greedy approach.

2. **Huffman Coding:**
   - Extend the Huffman Coding implementation to encode and decode a given string.
   - Compare the compression ratio of Huffman Coding with other compression algorithms.

3. **Divide and Conquer:**
   - Implement the Closest Pair of Points algorithm using Divide and Conquer and analyze its time complexity.
   - Solve the Merge Sort problem using the Divide and Conquer strategy and compare it with other sorting algorithms.

4. **Master Theorem:**
   - Apply the Master Theorem to determine the time complexity of the Quick Sort algorithm.
   - Analyze the time complexity of the Fast Fourier Transform (FFT) using the Divide and Conquer approach.

5. **Karatsuba Multiplication:**
   - Implement the Karatsuba algorithm for multiplying large numbers and compare its performance with the standard multiplication method.
   - Explore how Karatsuba’s algorithm reduces the number of multiplications required.

6. **Additional Problems:**
   - Use Greedy algorithms to solve the Minimum Spanning Tree problem using Kruskal’s and Prim’s algorithms.
   - Implement a Divide and Conquer algorithm to calculate the maximum subarray sum.

---

## **Final Summary and Comprehensive Exercises**

### **Overall Module Summary:**

Throughout this module on Algorithm Design and Analysis, you've acquired essential skills in designing and analyzing algorithms crucial for efficient problem-solving:

- **Sorting Algorithms:** Learned both simple (Bubble, Selection, Insertion) and efficient (Merge, Quick, Heap, Counting, Radix) sorting techniques, understanding their implementations, use-cases, and performance.
  
- **Searching Algorithms:** Mastered Linear Search and Binary Search, including their variants, to efficiently locate elements within data structures.
  
- **Recursion and Backtracking:** Developed the ability to solve problems recursively and employ backtracking to explore and abandon partial solutions, handling complex constraint-based problems like N-Queens and Sudoku.
  
- **Dynamic Programming:** Grasped the principles of breaking down problems into overlapping subproblems and optimal substructures, optimizing solutions through memoization and tabulation with applications in the Knapsack and Longest Common Subsequence problems.
  
- **Greedy Algorithms:** Understood the Greedy Choice Property and applied greedy strategies to solve the Activity Selection and Huffman Coding problems effectively.
  
- **Divide and Conquer:** Learned to decompose problems, solve subproblems recursively, and combine solutions, using the Master Theorem to analyze algorithmic time complexities, and implemented algorithms like Karatsuba Multiplication and the Closest Pair of Points.

### **Comprehensive Exercises:**

1. **Sorting Algorithms:**
   - **Compare Sorting Algorithms:** Implement Bubble Sort, Selection Sort, Insertion Sort, Merge Sort, Quick Sort, Heap Sort, Counting Sort, and Radix Sort. Compare their performance on various datasets (small, large, sorted, reverse-sorted).
   - **Stability Check:** Determine which sorting algorithms are stable and which are not. Modify an unstable sort to make it stable.

2. **Searching Algorithms:**
   - **Search in Rotated Array:** Implement Binary Search to find an element in a sorted and rotated array.
   - **Search in 2D Matrix:** Given a 2D matrix where each row is sorted, implement an efficient search algorithm to find a target value.

3. **Recursion and Backtracking:**
   - **Permutations:** Write a recursive function to generate all permutations of a given array.
   - **Sudoku Validator:** Implement a function to validate whether a completed Sudoku board is valid.

4. **Dynamic Programming:**
   - **Longest Increasing Subsequence:** Implement a DP solution to find the length of the longest increasing subsequence in an array.
   - **Matrix Chain Multiplication:** Determine the most efficient way to multiply a given sequence of matrices.

5. **Greedy Algorithms:**
   - **Job Sequencing Problem:** Given jobs with deadlines and profits, schedule them to maximize profit using a Greedy approach.
   - **Interval Scheduling Maximization:** Implement an algorithm to maximize the number of non-overlapping intervals.

6. **Divide and Conquer:**
   - **Binary Search Tree Operations:** Implement insertion, deletion, and search operations using the Divide and Conquer approach.
   - **Exponentiation:** Implement fast exponentiation (power) using Divide and Conquer to compute `x^n` efficiently.

7. **Advanced Problems:**
   - **Dynamic Programming with Bitmasking:** Solve the Traveling Salesman Problem (TSP) using DP with bitmasking.
   - **Backtracking with Pruning:** Implement a solver for the Word Search problem on a 2D grid.

8. **Combined Techniques:**
   - **Optimal Binary Search Trees:** Use Dynamic Programming to construct an optimal binary search tree given frequencies of access.
   - **Edit Distance with Backtracking:** Implement the Edit Distance problem and reconstruct the sequence of operations.

### **Further Reading and Resources:**

- **Books:**
  - *Introduction to Algorithms* by Cormen, Leiserson, Rivest, and Stein.
  - *Algorithms* by Robert Sedgewick and Kevin Wayne.
  - *The Algorithm Design Manual* by Steven S. Skiena.

- **Online Tutorials:**
  - [GeeksforGeeks Algorithm Tutorials](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)
  - [LeetCode](https://leetcode.com/) for practicing algorithmic problems.
  - [HackerRank](https://www.hackerrank.com/domains/algorithms) for algorithm challenges.

- **Video Lectures:**
  - [MIT OpenCourseWare - Introduction to Algorithms](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/)
  - [Stanford University - CS 161: Design and Analysis of Algorithms](https://www.youtube.com/playlist?list=PLoROMvodv4rO1NB9TD4iUZ3qghGEGtqNX)
  - [Harvard's CS50 on YouTube](https://www.youtube.com/user/cs50tv)

- **Interactive Platforms:**
  - [VisuAlgo](https://visualgo.net/en) for visualizing data structures and algorithms.
  - [Algorithm Visualizer](https://algorithm-visualizer.org/) for step-by-step algorithm execution.
  - [CodeSignal](https://codesignal.com/) and [Codewars](https://www.codewars.com/) for coding practice.

---

By completing this module, you have equipped yourself with essential algorithm design and analysis skills. These skills are not only fundamental for technical interviews but also for real-world problem-solving in software development and engineering roles. Continue practicing and exploring these concepts through the exercises and resources provided to deepen your understanding and enhance your proficiency.
