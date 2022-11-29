# Sorting Algorithms Code & Visualizations

## Visualizations

Practice running the visualizations to better understand how mostly sorted versus completely random arrays complete at different times for Bubble sort, Insertion sort, and Merge sort: http://www.sorting-algorithms.com/

1. What do you notice?

2. Which algorithm(s) benefit from arrays that are mostly sorted?

3. Which algorithm(s) stay largely consistent?

4. Why do you think this is?

## Sorting Algorithms Python Code

### Practice Reading Through and Running Algorithms

Read through and practice running each algorithm in the python Jupyter notebook.

You can do this in two ways:

1. You can download the python Jupyter notebook in this repo.

(For help getting started with Jupyter notebooks: https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/execute.html)

2. Run the notebook on Google Colab:

https://colab.research.google.com/drive/1GjOWEjiI96PldK3lO3QhbCVPLmDw_h5c?usp=sharing

### Bubble Sort

```
def bubble_sort(array):
    n = len(array)

    for i in range(n):
        # Create a flag that will allow the function to
        # terminate early if there's nothing left to sort
        already_sorted = True

        # Start looking at each item of the list one by one,
        # comparing it with its adjacent value. With each
        # iteration, the portion of the array that you look at
        # shrinks because the remaining items have already been
        # sorted.
        for j in range(n - i - 1):
            if array[j] > array[j + 1]:
                # If the item you're looking at is greater than its
                # adjacent value, then swap them
                array[j], array[j + 1] = array[j + 1], array[j]

                # Since you had to swap two elements,
                # set the `already_sorted` flag to `False` so the
                # algorithm doesn't finish prematurely
                already_sorted = False

        # If there were no swaps during the last iteration,
        # the array is already sorted, and you can terminate
        if already_sorted:
            break

    return array
```

### Insertion Sort

```
def insertion_sort(array):
    # Loop from the second element of the array until
    # the last element
    for i in range(1, len(array)):
        # This is the element we want to position in its
        # correct place
        key_item = array[i]

        # Initialize the variable that will be used to
        # find the correct position of the element referenced
        # by `key_item`
        j = i - 1

        # Run through the list of items (the left
        # portion of the array) and find the correct position
        # of the element referenced by `key_item`. Do this only
        # if `key_item` is smaller than its adjacent values.
        while j >= 0 and array[j] > key_item:
            # Shift the value one position to the left
            # and reposition j to point to the next element
            # (from right to left)
            array[j + 1] = array[j]
            j -= 1

        # When you finish shifting the elements, you can position
        # `key_item` in its correct location
        array[j + 1] = key_item

    return array
```

### Merge Sort

1. Recursively splits the input in half
2. A function that merges both halves, producing a sorted array

```
def merge_sort(arr):
    if len(arr) > 1:
        left_arr = arr[:len(arr)//2] # split array in half and assign left half to left_arr
        right_arr = arr[len(arr)//2:] # split array in half and assign right half to right_arr
        
        # recursion
        merge_sort(left_arr) # continue splitting in half
        merge_sort(right_arr) # continue splitting in half
        
        # merge
        i = 0 # left_arr index
        j = 0 # right_arr index
        k = 0 # merged array index
        while i < len(left_arr) and j < len(right_arr):
            if left_arr[i] < right_arr[j]: # if the value in the left array is less than the right array
                arr[k] = left_arr[i] # assign value from left array to merged array
                i += 1 # increment i index
            else: # otherwise the value in the right array is less than the left array
                arr[k] = right_arr[j] # assign value from right array to merged array
                j += 1 # increment j index
            k += 1 # increment k index in both cases
        
        # for the cases where there are no more values in the right_arr and you can simply transfer the rest from the left_arr
        while i < len(left_arr): 
            arr[k] = left_arr[i] 
            i += 1
            k += 1

        # for the cases where there are no more values in the left_arr and you can simply transfer the rest from the right_arr
        while j < len(right_arr):
            arr[k] = right_arr[j]
            j += 1
            k += 1
```
