
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
Now, we can create a plot:
```
x = np.arange(number_of_groups)
bar_width = 0.2
```
To make a bar plot it's necessary to use function [matplotlib.pyplot.bar](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.bar.html) from Matplotlib package. This function possesses several interesting parameters as:
* height
* width
* bottom
* align
* color
* edgecolor
* linewidth
* etc.

We will use some of them:
```
plt.bar(x, y, bar_width,
align='center',
color='orange',
label='Susceptible')

plt.bar(x +bar_width, y1, bar_width,
color='steelblue',
label='Resistant')
```

Function [matplotlib.pyplot.ylim](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.ylim.html?highlight=ylim#matplotlib.pyplot.ylim) is good for getting or setting the y-limits of the current axes:
```
plt.ylim([0, 250])
```
By using [matplotlib.pyplot.xlabel](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.xlabel.html?highlight=xlabel#matplotlib.pyplot.xlabel) and [matplotlib.pyplot.xticks](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.xticks.html?highlight=xticks#matplotlib.pyplot.xticks) we can set the x axis label of the current axis and set the x-limits of the current tick locations / labels, respectively. For example:
```
plt.xlabel('Years of release')
plt.ylabel('Number of varieties')
plt.xticks(x+bar_width/2, ('2000', '2005', '2009', '2010', '2013', '2015', '2016'))
```
Legend is an unconditionally important part of our graph. We will use [matplotlib.legend](https://matplotlib.org/api/legend_api.html?highlight=legend#module-matplotlib.legend) function for putting legend at the right place of the image:
```
plt.legend(title='Cultivars:', loc=(0.19, 0.77), frameon=False)
```

To make the graph more beautiful [matplotlib.axes.Axes.tick_params](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.tick_params.html?highlight=tick_params#matplotlib.axes.Axes.tick_params) function shoould be used:
```
plt.tick_params(axis='y', direction='in', labelbottom='on')
plt.tick_params(axis='x', bottom='off', top='off', left='off', right='off', labelbottom='on')
```
Finally, it's important to save the graph properly:

```
plt.savefig("/Users/natalaklimenko/Documents/python/homework grafs/plot2.png",dpi=200)
```

So, enjoy your pretty graph! :fire:  :smile:  :+1:

![plot](https://github.com/ns-klimenko/rep_for_Python/blob/master/Documents/MYDIR/plot2.png)




















