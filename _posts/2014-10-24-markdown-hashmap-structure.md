---
layout: post
title: HashMap Structure
categories: Language
tags: Java

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>

There are three variables that are relevant to the structure and even the performance of Java.util.HashMap(short as HashMap). Its implementation is based on a bucket table and linkedlists.

1. size, # of key-value pairs hold at a particular moment
2. threshold, the next size value at which to resize
3. capacity, length of the bucket table

where $\frac{size}{capacity}$ is denoted as load factor, which is a tradeoff between time and space complexity.

Declaration:
<pre>
transient Entry[] table;

transient int size;

int threshold;

final float loadFactor;

int capacity() { return table.length; }
</pre>


The following code segment shows how "threshold" works.
<pre>
void addEntry(int hash, K key, V value, int bucketIndex) {
    Entry<K,V> e = table[bucketIndex];
    table[bucketIndex] = new Entry<K,V>(hash, key, value, e);
    if (size++ >= threshold)
       resize(2 * table.length);
}
</pre>

After # of key-value pairs reaches threshold, the size of the bucket table is doubled.


This shows how "resize" function works.
<pre>
void resize(int newCapacity) {
    Entry[] oldTable = table;
    int oldCapacity = oldTable.length;
    if (oldCapacity == MAXIMUM_CAPACITY) {
        threshold = Integer.MAX_VALUE;
        return;
    }

    Entry[] newTable = new Entry[newCapacity];
    transfer(newTable);
    table = newTable;
    threshold = (int)(newCapacity * loadFactor);
}
</pre>

It instantiates a new bucket table with new capacity and assign all entries to the new table. Finally it sets new threshold for feature use.

This is how to assign all entries to a new table.
<pre>
void transfer(Entry[] newTable) {
    Entry[] src = table;
    int newCapacity = newTable.length;
    for (int j = 0; j < src.length; j++) {
        Entry<K,V> e = src[j];
        if (e != null) {
            src[j] = null;
            do {
                Entry<K,V> next = e.next;
                int i = indexFor(e.hash, newCapacity);
                e.next = newTable[i];
                newTable[i] = e;
                e = next;
            } while (e != null);
        }
    }
}
</pre>

Note that

* load factor $\alpha$ actually represents the average length of linkedlists whose heads are hold at buckets. Thus the average retrieval time for a key is O(1 + $\alpha$), where 1 for the computation of hash function and $\alpha$ for searching on a linkedlist.

* capacity is always power of two so that mod operation can be replaced by "&" operation which is more efficient.
<pre>
static int indexFor(int h, int length) {
    return h & (length-1);
}
</pre>

* If capacity is power of two, the probability of collision will be increased. hash function is applied
to avoid this.
<pre>
static int hash(int h) {
    // This function ensures that hashCodes that differ only by
    // constant multiples at each bit position have a bounded
    // number of collisions (approximately 8 at default load factor).
    h ^= (h >>> 20) ^ (h >>> 12);
    return h ^ (h >>> 7) ^ (h >>> 4);
}
</pre>
