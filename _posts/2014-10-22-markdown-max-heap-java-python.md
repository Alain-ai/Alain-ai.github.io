---
layout: post
title: Max(Priority) Heap in Java and Python
categories: Algorithm
tags: Java Python

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>

## Java
<pre>
public class MaxHeap< T extends Comparable< T >> {

    private List< T > list;
    private int len;
    private List< T > unmodifiedList;

    public MaxHeap(){
        list = new ArrayList< T >();
        len = list.size();
    }

    public MaxHeap(Collection< ? extends T > collection){
        list = new ArrayList<T>(collection);
        len = list.size();
        for (int i = len >> 1; i >= 0 ; --i){
            heapify(i);
        }
    }

    public void insert(T t){
        list.add(t);
        len += 1;
        int i = len - 1;
        while (i != 0){
            int parent = (i - 1) >>> 1;
            if (list.get(i).compareTo(list.get(parent)) > 0){
                Collections.swap(list, i, parent);
                i = parent;
            }
        }
    }

    public T pop(){
        T res = list.get(0);
        Collections.swap(list, 0, len - 1);
        len -= 1;
        heapify(0);
        return res;
    }

    private void heapify(int i ){
        int largeIdx = i;
        int left = (i << 1) + 1, right = (1 << 1) + 2;
        if (left < len){
            if (list.get(left).compareTo(list.get(largeIdx)) > 0){
                largeIdx = left;
            }
        }
        if (right < len){
            if (list.get(right).compareTo(list.get(largeIdx)) > 0){
                largeIdx = right;
            }
        }
        if (largeIdx != i){
            Collections.swap(list, largeIdx, i);
            heapify(i);
        }
    }

    public List< T > showList(){
        return unmodifiedList == null ? Collections.unmodifiableList(list) : unmodifiedList;
    }
}
</pre>


## Python
<pre>
class MaxHeap():
    def __init__(self):
        self.arr = []
        self.len = 0

    def insert(self, val):
        self.arr.append(val)
        self.len += 1
        i = self.len - 1
        while i != 0:
            if self.arr[i] > self.arr[(i-1) >> 1]:
                self.arr[i], self.arr[(i-1) >> 2] = self.arr[(i-1) >> 2], self.arr[i]
                i = (i-1) >> 2
            else:
                break

    def pop(self):
        if not self.len:
            return None
        res = self.arr[0]
        self.arr[0] = self.arr[-1]
        self.len -= 1
        self.heapify(0)
        return res

    def heapify(self, i):
        large_idx = i
        if (i << 1) + 1 < self.len:  # has left child
            large_idx = i if self.arr[i] >= self.arr[(i << 1) + 1] else (i << 1) + 1
        if (i << 1) + 2 < self.len + 1:  # has right child
            large_idx = large_idx if self.arr[large_idx] >= self.arr[(i << 1) + 2] else (i << 1) + 2
        if large_idx and large_idx != i:
            self.arr[i], self.arr[large_idx] = self.arr[large_idx], self.arr[i]
            self.heapify(large_idx)

    @staticmethod
    def build_from_array(arr):
        mp = MaxHeap()
        mp.arr = arr[:]
        mp.len = len(mp.arr)
        for i in xrange(mp.len >> 1, -1, -1):
            mp.heapify(i)
        return mp
</pre>
