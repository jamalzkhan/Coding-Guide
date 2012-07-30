## Sorting & Searching

### Binary Search
- Complexity is O(n)

Solution

~~~~ {.java .highlighting}
int bSearch(int n, int [] array, int start, int end){
  
  if (start < end){
    int middle = (start + end) / 2;
    if (array[middle] == n)
      return middle;
    else if (array[middle] < n)
      bSearch(n, array, middle+1, end);
    else
      bSearch(n, array, start, middle-1);
  }
  return -1
  
}
~~~~

### Merge Sort
- Complexity is 0(n*log(n))

~~~~ {.python}

def mergeSort(array):
  
  if (len(array)) == 1):
    return array
  
  half = len(array)/2
  left = []
  right = []
  
  for i in range(0, half):
    left.append(array[i])
  
  for i in range(half, len(A)):
    right.append(array[i])
  
  return merge(mergeSort(left), mergeSort(right))
  
def merge(left, right):
  
  result = []
  
  while len(left) > 0 || len(right) >0:
    if len(left) > 0 && len(right) > 0:
      if left[0] > right[0]:
        result.append(left[0])
        left = left[1:]
      else:
        result.append(right[0])
        right = right[1:]
    elif len(left) > 0:
      result.append(left[0])
      left = left[1:]
    else
      result.append(right[0])
      right = right[1:]
      
  return result

~~~~

### Insertion Sort

~~~~ {.python}

def insertionSort(a):
  for i in range (1, len(a)):
    value = a[i]
    j = i - 1
    done = False
    while done == False:
      if a[j] > a[j+1]:
        a[j+1] = a[j]
        j = j - 1
        if j < 0:
          done = True
      else:
        done = True
      a[j+1] = value
  return a

~~~~


### Quick Sort


~~~~ {.python}

def quickSort(a, start, end):

  if (start < end):
    pivot = a[end]
    p = start
    for i in range(start, end):
      if a[i] < pivot:
        swap(a, i, p)
        p = p + 1
        swap(a, p, end)
  
      quickSort(a, start, p-1)
      quickSort(a, p+1, end)
  
  return a
  
def swap(a, i, j):
  n = a[i]
  a[i] = a[j]
  a[j] = n

~~~~

