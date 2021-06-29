# Transformer

[ViT](Transformer%20437254063d424c49892ba2befbf0f2ae/ViT%2047b25d0e25174739bf2b7ed606548454.md)

主要参考

[详解Transformer中Self-Attention以及Multi-Head Attention_霹雳吧啦Wz-CSDN博客](https://blog.csdn.net/qq_37541097/article/details/117691873)

针对RNN&LSTM 无法并行化等问题

优点：记忆长度长、可以并行化

战术贴图

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled.png)

其实贴了也没有什么用，也看不懂

下面理解下

## Self-Attention模块

主要实现对给定输入的一个attention的输出

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%201.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%201.png)

细节方面

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%202.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%202.png)

首先 $x_1$ 经过Embedding（映射），变成 $a_1$，然后后面都是对 $a_1$操作，从 $a_1$可以生成三个向量 $q,k,v$，

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%203.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%203.png)

$q,k$相互match，然后在经过softmax，得到两个数

两个数，这两个数和 $v$相乘后在相加，就得到一个attention

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%204.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%204.png)

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%205.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%205.png)

再贴下self attention的作用

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%206.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%206.png)

## Multi-head Self-Attention

作用和上面的Self Attention一样

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%207.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%207.png)

具体细节

首先看下前面一个head

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%208.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%208.png)

再是两个head，其实源码中就是将 $q,k,v$向量按head数量均分

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%209.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%209.png)

然后按照下标分别结合成head1，head2...

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2010.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2010.png)

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2011.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2011.png)

每个head就是一个小型Self-attention，

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2012.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2012.png)

最后将其拼接

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2013.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2013.png)

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2014.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2014.png)

还有一个

为了解决输入顺序改变后输出一样改变的问题

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2015.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2015.png)

提出了Positional Encoding

![Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2016.png](Transformer%20437254063d424c49892ba2befbf0f2ae/Untitled%2016.png)

就是在输入的 $a_i$上在加一个同样dim的位置编码