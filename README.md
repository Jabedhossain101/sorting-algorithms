# Sorting Algorithms in C++

A collection of classic sorting algorithms implemented in C++, sharing a common `main()` and `printArray()` structure. Only the sorting function itself changes between examples.

## Table of Contents

- [Common Project Structure](#common-project-structure)
- [Bubble Sort](#bubble-sort)
- [Selection Sort](#selection-sort)
- [Insertion Sort](#insertion-sort)
- [Merge Sort](#merge-sort)
- [Quick Sort](#quick-sort)
- [Counting Sort](#counting-sort)
- [Master Learning Pattern](#master-learning-pattern)
- [Learning Roadmap](#learning-roadmap)
- [Time Complexity Comparison](#time-complexity-comparison)

---

## Common Project Structure

All sorting algorithms use the same `main()` function and `printArray()` function. Only the sorting function changes.

```cpp
#include <iostream>
using namespace std;

// Sorting Function
// bubbleSort(arr, n);
// selectionSort(arr, n);
// insertionSort(arr, n);
// mergeSort(arr, 0, n - 1);
// quickSort(arr, 0, n - 1);
// countingSort(arr, n);

void printArray(int arr[], int n)
{
    for(int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }

    cout << endl;
}

int main()
{
    int n;

    cout << "Enter Array Size: ";
    cin >> n;

    int arr[n];

    cout << "Enter Array Elements: ";

    for(int i = 0; i < n; i++)
    {
        cin >> arr[i];
    }

    // Call Any Sorting Function Here

    printArray(arr, n);

    return 0;
}
```

---

## Bubble Sort

**Algorithm**
1. Compare adjacent elements.
2. Swap if they are in the wrong order.
3. Repeat until the array is sorted.

**Logic**

```cpp
void bubbleSort(int arr[], int n)
{
    for(int i = 0; i < n - 1; i++)
    {
        for(int j = 0; j < n - i - 1; j++)
        {
            if(arr[j] > arr[j + 1])
            {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}
```

---

## Selection Sort

**Algorithm**
1. Find the minimum element.
2. Swap it with the current position.
3. Repeat for the remaining elements.

**Logic**

```cpp
void selectionSort(int arr[], int n)
{
    for(int i = 0; i < n - 1; i++)
    {
        int minIndex = i;

        for(int j = i + 1; j < n; j++)
        {
            if(arr[j] < arr[minIndex])
            {
                minIndex = j;
            }
        }

        swap(arr[i], arr[minIndex]);
    }
}
```

---

## Insertion Sort

**Algorithm**
1. Take one element at a time.
2. Shift larger elements to the right.
3. Insert the current element into its correct position.

**Logic**

```cpp
void insertionSort(int arr[], int n)
{
    for(int i = 1; i < n; i++)
    {
        int key = arr[i];
        int j = i - 1;

        while(j >= 0 && arr[j] > key)
        {
            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = key;
    }
}
```

---

## Merge Sort

**Algorithm**
1. Divide the array into two halves.
2. Recursively sort each half.
3. Merge the sorted halves.

**Logic**

```cpp
void merge(int arr[], int left, int mid, int right)
{
    int n1 = mid - left + 1;
    int n2 = right - mid;

    int L[n1], R[n2];

    for(int i = 0; i < n1; i++)
        L[i] = arr[left + i];

    for(int i = 0; i < n2; i++)
        R[i] = arr[mid + 1 + i];

    int i = 0;
    int j = 0;
    int k = left;

    while(i < n1 && j < n2)
    {
        if(L[i] <= R[j])
        {
            arr[k++] = L[i++];
        }
        else
        {
            arr[k++] = R[j++];
        }
    }

    while(i < n1)
    {
        arr[k++] = L[i++];
    }

    while(j < n2)
    {
        arr[k++] = R[j++];
    }
}

void mergeSort(int arr[], int left, int right)
{
    if(left < right)
    {
        int mid = (left + right) / 2;

        mergeSort(arr, left, mid);

        mergeSort(arr, mid + 1, right);

        merge(arr, left, mid, right);
    }
}
```

---

## Quick Sort

**Algorithm**
1. Select a pivot element.
2. Partition the array.
3. Recursively sort the left and right partitions.

**Logic**

```cpp
int partition(int arr[], int low, int high)
{
    int pivot = arr[high];

    int i = low - 1;

    for(int j = low; j < high; j++)
    {
        if(arr[j] < pivot)
        {
            i++;

            swap(arr[i], arr[j]);
        }
    }

    swap(arr[i + 1], arr[high]);

    return i + 1;
}

void quickSort(int arr[], int low, int high)
{
    if(low < high)
    {
        int pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);

        quickSort(arr, pi + 1, high);
    }
}
```

---

## Counting Sort

**Algorithm**
1. Find the maximum element.
2. Count the frequency of every value.
3. Reconstruct the original array using the frequency array.

**Logic**

```cpp
void countingSort(int arr[], int n)
{
    int maxValue = arr[0];

    for(int i = 1; i < n; i++)
    {
        if(arr[i] > maxValue)
        {
            maxValue = arr[i];
        }
    }

    int count[maxValue + 1] = {0};

    for(int i = 0; i < n; i++)
    {
        count[arr[i]]++;
    }

    int index = 0;

    for(int i = 0; i <= maxValue; i++)
    {
        while(count[i] > 0)
        {
            arr[index++] = i;

            count[i]--;
        }
    }
}
```

---

## Master Learning Pattern

Every sorting algorithm follows one of these patterns:

| Algorithm | Core Idea |
|---|---|
| Bubble Sort | Compare → Swap |
| Selection Sort | Find Minimum → Swap |
| Insertion Sort | Shift → Insert |
| Merge Sort | Divide → Merge |
| Quick Sort | Pivot → Partition |
| Counting Sort | Count Frequency → Rebuild |

## Learning Roadmap

```
Bubble Sort
      ↓
Selection Sort
      ↓
Insertion Sort
      ↓
Merge Sort
      ↓
Quick Sort
      ↓
Counting Sort
```

## Time Complexity Comparison

| Algorithm | Best | Average | Worst | Space | Stable | In-place |
|---|---|---|---|---|---|---|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ | ✅ |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | ❌ | ✅ |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ | ✅ |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ | ❌ |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) (avg.) | ❌ | ✅ |
| Counting Sort | O(n + k) | O(n + k) | O(n + k) | O(n + k) | ✅* | ❌ |
