# Assignment 7: Sorting

Lab Assignment 7: Sorting Algorithms

---

## Question 1: Implement Sorting Techniques

**Explanation:** This program implements five fundamental sorting algorithms: Selection Sort, Insertion Sort, Bubble Sort, Merge Sort, and Quick Sort. Each algorithm sorts an array of integers in ascending order.

**Code:**
```cpp
#include <iostream>
using namespace std;

void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIdx]) minIdx = j;
        }
        swap(arr[i], arr[minIdx]);
    }
}

void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    int L[n1], R[n2];
    
    for (int i = 0; i < n1; i++) L[i] = arr[left + i];
    for (int j = 0; j < n2; j++) R[j] = arr[mid + 1 + j];
    
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) arr[k++] = L[i++];
        else arr[k++] = R[j++];
    }
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    int arr1[] = {64, 25, 12, 22, 11};
    int arr2[] = {64, 25, 12, 22, 11};
    int arr3[] = {64, 25, 12, 22, 11};
    int arr4[] = {64, 25, 12, 22, 11};
    int arr5[] = {64, 25, 12, 22, 11};
    int n = 5;
    
    selectionSort(arr1, n);
    cout << "Selection Sort: ";
    printArray(arr1, n);
    
    insertionSort(arr2, n);
    cout << "Insertion Sort: ";
    printArray(arr2, n);
    
    bubbleSort(arr3, n);
    cout << "Bubble Sort: ";
    printArray(arr3, n);
    
    mergeSort(arr4, 0, n - 1);
    cout << "Merge Sort: ";
    printArray(arr4, n);
    
    quickSort(arr5, 0, n - 1);
    cout << "Quick Sort: ";
    printArray(arr5, n);
    
    return 0;
}
```

**Output:**
```
Selection Sort: 11 12 22 25 64 
Insertion Sort: 11 12 22 25 64 
Bubble Sort: 11 12 22 25 64 
Merge Sort: 11 12 22 25 64 
Quick Sort: 11 12 22 25 64 
```

---

## Question 2: Improved Selection Sort

**Explanation:** This is an optimized version of Selection Sort that finds both the minimum and maximum elements in each pass and places them at their correct positions from both ends of the array simultaneously, reducing the number of passes needed.

**Code:**
```cpp
#include <iostream>
using namespace std;

void improvedSelectionSort(int arr[], int n) {
    int left = 0, right = n - 1;
    
    while (left < right) {
        int minIdx = left, maxIdx = left;
        
        for (int i = left; i <= right; i++) {
            if (arr[i] < arr[minIdx]) minIdx = i;
            if (arr[i] > arr[maxIdx]) maxIdx = i;
        }
        
        swap(arr[left], arr[minIdx]);
        
        if (maxIdx == left) maxIdx = minIdx;
        
        swap(arr[right], arr[maxIdx]);
        
        left++;
        right--;
    }
}

void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    int arr[] = {64, 25, 12, 22, 11, 90, 88, 45, 50, 32};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    cout << "Original array: ";
    printArray(arr, n);
    
    improvedSelectionSort(arr, n);
    
    cout << "Sorted array: ";
    printArray(arr, n);
    
    return 0;
}
```

**Output:**
```
Original array: 64 25 12 22 11 90 88 45 50 32 
Sorted array: 11 12 22 25 32 45 50 64 88 90 
```

---

## Conclusion

This assignment provided hands-on experience with various sorting algorithms, each with different time complexities and use cases. Selection Sort, Insertion Sort, and Bubble Sort have O(n²) time complexity and are suitable for small datasets. Merge Sort and Quick Sort are divide-and-conquer algorithms with O(n log n) average time complexity, making them more efficient for larger datasets. The improved Selection Sort demonstrates how optimizations can reduce the number of iterations needed. Understanding these sorting techniques is fundamental to computer science and helps in choosing the right algorithm based on data characteristics and performance requirements.