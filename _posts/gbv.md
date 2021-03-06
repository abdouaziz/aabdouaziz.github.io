---
layout: post
title:  "Gender Based Violence"
date:   20121-10-17 14:22:01 
author_profile: true
excerpt_separator: "<!--more-->"
header:
  overlay_image: /images/waterfront.jpg
  overlay_filter: 0.4 # same as adding an opacity of 0.5 to a black background
---



Small project I realized when I was learning python and thought I could hack trading easily. I implemented really simplistic methods with a simple simulator in order to back test my strategy, which worked effectively. (back testing, not the strategy itself)

<!--more-->

Github repo: [here](github.com/RafaelCartenet/BOTAI/)

When I was learning python I gave myself some little challenges in order to get familiar with the language. One of them was competing in a lot of programming little contests, to get the basic syntax and reflexes of the language, the other one being tackling "real life" use cases with what I learned.

I am retro engineering this little project as I didn't take the time to make a complete explanation at that time. The key at that time was to get familiar with OOP with Python, that is creating a little project around a set of classes and implement methods.


Backtesting output example:

```
---------------------------------------------------------------------------------------
|#	|Date				                |StackP  |action|amount	|result	|balance
---------------------------------------------------------------------------------------
|1	|2017-03-04 00:00:00+00:00	|1.06593 |Call	|1.00		|True	  |1000.00
|2	|2017-03-04 00:05:00+00:00	|1.06628 |Call	|1.00		|False	|1000.88
|3	|2017-03-04 00:10:00+00:00	|1.06613 |Put	  |2.14		|False	|999.88
|4	|2017-03-04 00:15:00+00:00	|1.06622 |Call	|4.56		|False	|997.74
|5	|2017-03-04 00:20:00+00:00	|1.06619 |Put	  |9.75		|True	  |993.18
|6	|2017-03-04 00:25:00+00:00	|1.06615 |Call	|1.00		|False	|1001.76
|7	|2017-03-04 00:30:00+00:00	|1.06603 |Put	  |2.14		|True	  |1000.76
|8	|2017-03-04 00:35:00+00:00	|1.06602 |Call	|1.00		|True	  |1002.64
|9	|2017-03-04 00:40:00+00:00	|1.06619 |Call	|1.00		|False	|1003.52
|10	|2017-03-04 00:45:00+00:00	|1.06613 |Put	  |2.14		|False	|1002.52
|11	|2017-03-04 00:50:00+00:00	|1.06645 |Call	|4.56		|False	|1000.38
|12	|2017-03-04 00:55:00+00:00	|1.06625 |Put	  |9.75		|True	  |995.82
|13	|2017-03-04 01:00:00+00:00	|1.06605 |Call	|1.00		|True	  |1004.40
|14	|2017-03-04 01:05:00+00:00	|1.06632 |Call	|1.00		|True	  |1005.28
|15	|2017-03-04 01:10:00+00:00	|1.06634 |Call	|1.00		|False	|1006.16
|16	|2017-03-04 01:15:00+00:00	|1.06611 |Put	  |2.14		|False  |1005.16
...

Datas information
--------------------------------------
  Period Start		: 03/04/17 00:00
  Period End		: 03/04/17 23:58
  Timestep used		: M5
  Ups			: 139 | 48.43%
  Downs			: 137 | 47.74%
  Equals		: 11 | 3.83%

Results
--------------------------------------
  Initial Balance	: 1000.00$
  Final Balance		: 1117.04$
  Profit		: 117.04$
  Relative profit	: 11.70%
  Nb actions taken	: 287
  Max Balance		: 1117.04$
  Min Balance		: 879.35$

Consecutive actions results
--------------------------------------
  MaxConsRight		: 6
  MaxConsWrong		: 7
  Details :
  consecutive right actions
   	|uni	|cumul
   	-------------
    2:	|16	|39
    3:	|12	|23
    4:	|8	|11
    5:	|2	|3
    6:	|1	|1
  consecutive wrong actions
   	|uni	|cumul
   	-------------
    2:	|14	|34
    3:	|10	|20
    4:	|3	|10
    5:	|2	|7
    6:	|4	|5
    7:	|1	|1
```

Below you'll find an explanation of the output for every section
- **Detailed transactions**: Detailed transactions during the whole period. Pretty useful for debugging a strategy, highliting the main errors the model did during simulation.
- **Datas Information**: This gave me a quick idea about the data that has been used as well as some simple simple statistics to give me hints regarding the following results such as the distribution of each label.
- **Results**: The results regarding profits. Although final profit is important, min and max balance also are. If you get to have a minimum balance, of course, that means something went wrong, you spent money that you didn't have. And on the other side if you had during the back testing period a way higher number than the final amount you get, that means you did some critical mistakes at some point that you may have avoided. It also gives the number of taken actions, that gives indication about how confident the model is to take a prediction, whatever the prediction is.
- **Consecutive action results**: This little additional summary was mostly used for debugging my MartinGale strategy as too many consecutive mistakes can lean to bankrupt quite fast. It gives an idea about the streaks the model had, regardless whether it's a winning streak or a losing streak, although losing streaks matter more ...


## EXAMPLES

```
Consecutive actions results
--------------------------------------
  MaxConsRight		: 10
  MaxConsWrong		: 12
  Details :
  consecutive right actions
   	|uni	|cumul
   	-------------
    2:	|858	|1656
    3:	|403	|798
    4:	|215	|395
    5:	|95	|180
    6:	|41	|85
    7:	|18	|44
    8:	|15	|26
    9:	|9	|11
    10:	|2	|2
  consecutive wrong actions
   	|uni	|cumul
   	-------------
    2:	|808	|1591
    3:	|390	|783
    4:	|211	|393
    5:	|93	|182
    6:	|43	|89
    7:	|29	|46
    8:	|5	|17
    9:	|6	|12
    10:	|3	|6
    11:	|1	|3
    12:	|2	|2
```
