Eliza 处理用户输入的句子流程如下：

- `分词`：之后的处理都是针对 “词”; 对于英文，这件事情比较简单; 而对于中文，会稍微麻烦一点。   
- `pre-substitution`： 这一步是做同义词的替换; 使得意思相近的词语，在之后的处理中被当作同一个`keyword`处理; 还有一个重要的作用，因为后面我们要选择 `decomposition pattern`,替换得到的不一定是我们要选择的 `keyword`， 而是 `keyword` 的 `decomposition pattern` 的一部分。      
- `keyword sort` : 经过了 `pre-substitution` 得到的所有“词”都叫做 `keyword`, 在 `script` 里面，会有部分 `keyword` 和它们对应的 `weights`, 根据 `weights` 从大到小，我们对句子里的 `keywords` 进行排序。  
- `Decomposition Pattern Selection`: 从 `weight` 最大的 `keyword` 开始，考察这个 `keyword` 的所有 `decomposition Pattern`， 是否有和句子匹配的，如果有，那么这是我们要选择的 `decomposition pattern`, 否则，继续从 `weight` 次之的 `keyword`依次考察，直到找到一个 `decomposition pattern` 为止。  
- `Reassembly Pattern Selection`: 在找到的 `Decomposition Pattern` 下面，选择一条 `Reassembly Pattern`. 如果有多条，那么每一次匹配到同样的`Decomposition Pattern` 的时候，就选取和上一次不一样的那条 `Reassembly Pattern`.  
- `Post substitution`: 这里主要是把原本输入句子中的 “我” 和 “你” 互换。我看到在有的实现里面，会把这一步叫做 `Conjugate substitution`.

Special Rule:

> If a $ appears first in a decomposition rule, then the output is formed as
normal, but is saved and Eliza goes on to the next keyword.  If no keywords
match, and there are saved sentences, one of them is picked at random and
used as the output, then it is discarded.
If there are no saved sentences, and no keywords match, then it uses the
keyword "xnone".

Structure：

- 每一个 `keyword` 对应一个 `weight`  
- 每一个 `keyword` 对应多个 `Decomposition Pattern`  
- 每一个 `Decomposition Pattern` 对应多个 `Reassembly Pattern`

Synon：

- 让一条 `Decomposition Pattern` 可以被当作是多条  

----
Backup of the [instruction](http://chayden.net/eliza/instructions.txt) is [here](instructions.txt)
