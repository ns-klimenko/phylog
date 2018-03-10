
# **Bio::Phylo**


Читаем [дерево](https://www.jasondavies.com/tree-of-life/life.txt)

```
import urllib3 as URL
tree_url=URL.PoolManager().request('get', 'https://www.jasondavies.com/tree-of-life/life.txt').data.decode('utf-8')
```
Импортируем нужные библиотеки:

```
from Bio import Phylo
import pylab
from io import StringIO
import matplotlib
import matplotlib.pyplot as plt
```
Рисуем это дерево псевдографикой (draw_ascii):

```
t=StringIO(tree_url)
tt = Phylo.read(t, 'newick')
Phylo.draw_ascii(tt)
```
Рисуем дерево с помощью draw:

```
matplotlib.rc('font', size=6)
from pylab import rcParams
rcParams['figure.figsize'] = 10, 30
tt.ladderize()
Phylo.draw(tt, do_show=False)
```
Сохраняет изображение дерева в растровый формат (png) и векторный (pdf):


```
plt.savefig('/Users/natalaklimenko/Documents/phylo-dot.png', format="png", dpi=2000)
plt.savefig('/Users/natalaklimenko/Documents/phylo-dot.pdf', format="pdf", dpi=2000)
```
![plot](https://github.com/ns-klimenko/phylog/blob/master/phylo-dot.pdf)
![plot](https://github.com/ns-klimenko/phylog/blob/master/phylo-dot.png)

Изменяем формат на phyloxml и записываем [файл](https://github.com/ns-klimenko/phylog/blob/master/rest-trees.xml):
```
Phylo.write(tt, 'rest-trees.xml', 'phyloxml')
```
# **ETE (ETE3)::Tree**

Читаем [дерево](https://www.jasondavies.com/tree-of-life/life.txt)
```
import urllib3 as URL
tree_url=URL.PoolManager().request('get', 'https://www.jasondavies.com/tree-of-life/life.txt').data.decode('utf-8')
```
Можем посмотреть на само дерево:
```
from io import StringIO
from ete3 import Tree
t = Tree(tree_url, format=1)
t.show()
```
Вырезаем из дерева набор из 42  листьев. Рисуем:

```
leaf=t.get_leaf_names()
select=leaf[0:41]
t.prune(select)
print(t)
```
Рисуем  первое из этих деревьев с дополнительной обработкой символов на узлах:

```
from ete3 import Tree, NodeStyle, TreeStyle

ts = TreeStyle()
ts.show_leaf_name = True
# Draws nodes as small red spheres of diameter equal to 10 pixels
s = NodeStyle()
s["shape"] = "sphere"
s["size"] = 10
s["fgcolor"] = "darkred"

# Gray dashed branch lines
s["hz_line_type"] = 1
s["hz_line_color"] = "#cccccc"

for n in t.traverse():
n.set_style(s)
t.show(tree_style=ts)
```

 :smile:  :+1:
