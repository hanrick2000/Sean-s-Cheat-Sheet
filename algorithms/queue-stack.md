# Queue & Stack

_Reference: Laioffer Class 3_

- __Queue__ - FIFO (First in first out)
- __Stack__ - FILO (First in last out)
- __Deque__ - 左右都可以进出的队列

## Ascending Stack

### Q1: find max rectangle in histogram

## Descending Deque

### Q1: keep track of the max element of a sliding window of input stream

- use Descending Deque
- use lazy deletion
    - do not take up too much space. worst case O(k)
- Time for each move
    - worst case O(k)
    - amortised O(1)
- Time for all move O(n)