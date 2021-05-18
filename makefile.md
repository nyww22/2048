# Makefile



{% embed url="https://qiita.com/petitviolet/items/a1da23221968ee86193b" %}

{% embed url="http://objectclub.jp/community/memorial/homepage3.nifty.com/masarl/article/gnu-make/rule.html" %}



### 疑似ターゲット：.Phoney

{% embed url="https://qiita.com/kasei-san/items/ad25df63260e86c5cc71" %}



### 暗黙ルール

{% embed url="https://www.ecoop.net/coop/translated/GNUMake3.77/make\_10.jp.html" %}

{% embed url="http://www.jsk.t.u-tokyo.ac.jp/~k-okada/makefile/" %}

{% embed url="http://exlight.net/devel/make/basics.html" %}

{% embed url="http://quruli.ivory.ne.jp/document/make\_3.79.1/make-jp\_9.html" %}



### サフィックスルール（ダブルサフィックス、シングルサフィックス）

{% embed url="http://nenya.cis.ibaraki.ac.jp/TIPS/makefile2.html" %}

{% embed url="https://zenn.dev/kusaremkn/articles/84005016fca5df121b8e" %}

```text
.SUFFIXES:
.SUFFIXES: .c .sh

.sh:
	cat $< >$@
	chmod a+x $@
.c:
	$(CC) $(CFLAGS) $(LDFLAGS) $^ $(LDLIBS) -o $@

```



