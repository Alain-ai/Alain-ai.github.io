---
layout: post
title: Decorator
categories: Design_Pattern
tags: Java

---
<!-- import js for mathjax -->
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>

Let's introduce the requirement for importing decorator design pattern. Say we want to read off from four types of input:

    1. InputStream
    2. File
    3. char array
    4. String

We have a abstract class Reader to outline some basic methods like read, close and skip.

<pre>
public abstract class Reader implements Readable, Closeable {

    protected Object lock;

    protected Reader(Object lock) {
        if (lock == null) {
            throw new NullPointerException();
        }
        this.lock = lock;
     }
 }
</pre>

Then we create four classes which extend Reader. They get direct touch with those four types of input. They are :

    1. InputSteamReader
    2. FileReader
    3. CharArrayReader
    4. StringReader

Additionally, we want other two Readers which provide more efficient methods of reading than those four ground Reader. They are BufferedReader and LineNumberReader. With the combination of the two high level Readers and four low level Readers, we've got 8 classes. They are:

    1. BufferedInputSteamReader
    2. BufferedFileReader
    3. ...
    4. ...
    5. LineNumberInputSteamReader
    6. LineNumberFileReader
    7. ...
    8. ...

With more input types and more high level Readers, we'll create too many Readers(13), which is called class explosion. So, it's a good place to introduce decorator design pattern.

For example, we have created a low level Reader "InputSteamReader" to read from standard input(InputStream System.in).

<pre>
public class InputStreamReader extends Reader {

    private final StreamDecoder sd;

    public InputStreamReader(InputStream in) {
       super(in);
       try {
           sd = StreamDecoder.forInputStreamReader(in, this, (String)null); // ## check lock object
       } catch (UnsupportedEncodingException e) {
           // The default encoding should always be available
           throw new Error(e);
       }
    }
}
</pre>

We don't have to create a class like BufferedInputSteamReader, and we just need create a class called BufferedReader which will wrap a Reader(InputSteamReader here) and provide its own ways to read off. Now we say BufferedReader decorates InputSteamReader.

<pre>
public class BufferedReader extends Reader {

    private Reader in;

    public BufferedReader(Reader in, int sz) {
       super(in);
       if (sz <= 0)
           throw new IllegalArgumentException("Buffer size <= 0");
       this.in = in;
       cb = new char[sz];
       nextChar = nChars = 0;
    }
}
</pre>

When BufferedReader visit to input directly, this.in will do the real job. In this way, BufferedReader does not have to care about how to read from input and just need assemble output from this.in and provide highly efficient reading methods.

After applying decorator design pattern, we will get 7 Readers totally.
