# INF4000 Week 5: 
# Trouble shooting with Google: where the programming starts

Learning objective:
* Note this week is NOT about advanced techniques or skills for R studio
* To read error messages
* available source to start search for your bug
* examples

![a](https://github.com/casszhao/INF4000.github.io/blob/main/debugging.jpg)

When see errors, do not panic.

Coders/data scientists, fix errors and mistakes, so-called "debug", all the time. Today, let s look at debugging.


There are two ways you can make your life easier. The first is knowing the tools at your disposal in RStudio to debug errors. RStudio provides a variety of tools to help you diagnose the problem at its source and come up with a solution as quick as possible. The second is knowing how to write functions that return clear yet detailed errors using condition handling. This post will walk through both of these topics so that you can become better at handling errors when writing your own code as well as working with errors in someone else’s code.

After a while of coding, you will know how and where to start to fix the problem. Before that, you can try following general strategies to debug an error:


1. **Google**
 * Read the ERROR MESSAGE! Most error message does tell you what the problem is. Google it.
 * Many times it is a common error with a known solution. Sometime, even just copy paste your error message, you will find many people had the exactly issue like yours before.
 * Change a way to describe your problem if you cannot find the solution. 
 * Sometime, results from Google costs a lot of time to filter (particularly, when you ask in a not so good way), try other professional platforms, such as: 
 ** w3schools.com, codeproject.com
        
2. **Make it repeatable**
 * Create a minimal, reproducible example (e.g. reprex) using simple data
 * Note which inputs don’t trigger the error
 * If not already done, write simple tests to reduce chances of creating a new bug

3. **Figure out where the error is** 
 * Use the “scientific method”
 * Hypothesize, test with experiments, and record results
 * If needed, ask someone else for a second pair of eyes to review

4. **Fix it and test it**
 These four steps should be followed each time you encounter an unexpected error in a function. Many times, you may not even know what line of code the error is coming from. How can you determine where the code is not behaving? You can follow these general steps to answer this question:

 * Begin running the code.
 * Stop the code where you suspect the bug/problem is arising.
 * Look and/or walk through the code, step-by-step at that point.

 This can be done ad-hoc in a separate R script containing the function code, or using several built-in tools in RStudio.



## Case study: Boxplot
Let’s look at an example boxplot to demonstrate the use of these tools. Mary trys to produce boxplots where the colour represents the category, these appear overlapping if varwidth is set to TRUE

![a](https://github.com/casszhao/INF4000.github.io/blob/main/boxplot1.png)

Let s see her code
```
require(ggplot2)
#> Loading required package: ggplot2
ggplot(data = iris, aes(Species, Sepal.Length)) + geom_boxplot(aes(colour = Sepal.Width < 3.2), varwidth = TRUE)
#> Warning: position_dodge requires non-overlapping x intervals
```

## Case study: Fuction
Next, let’s look at an example function.


## Case study: Trouble shooting with via play arounding
Tips: when debugging, do not afraid try
One question from last week: how to show a full range of coordinates.



## Case study: Trouble shooting with Google




Let s say you want to present the time distribution of your data via a nice visualisation. And you find a good reference that you want to do something similar with your data. 

<img src="https://github.com/casszhao/INF4000.github.io/blob/main/yelp_vio.png" width="300" />
<img src="https://github.com/casszhao/INF4000.github.io/blob/main/xfact_vio.png" width="300" />
<img src="https://github.com/casszhao/INF4000.github.io/blob/main/AmazDigiMu_vio.png" width="300" />
<img src="https://github.com/casszhao/INF4000.github.io/blob/main/AmazPantry_vio.png" width="300" />
<img src="https://github.com/casszhao/INF4000.github.io/blob/main/AmazInstr_vio.png" width="400" align="left" alt="My Image"/>
<img src="https://github.com/casszhao/INF4000.github.io/blob/main/agnews_vio.png" width="400" align="left" alt="My Image"/>


If you are interested in our new [paper](https://arxiv.org/pdf/2210.09197.pdf), welcome to check out.
## Topic one

```example code```

example code 2
```
example code
```

cheatsheet for [github pages](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

## my fav error message

Techniques not only for R

Do a fancy code with bug and find 


小组活动
Now, let s practice.

Let s demonstrate the topic of a article. 

--> search
--> world cloud
--> how to do world cloud

做这个
https://r4ds.had.co.nz/data-visualisation.html


运用“高科技”

other tips:
- explain to yourself
- stackoverflow
- 

## Other useful links
[Hands-On Programming with R(]https://rstudio-education.github.io/hopr/debug.html)
[A case study in debugging R](https://github.com/karawoo/2019-01-17-rstudioconf/blob/master/woo_rstudioconf_2019.pdf)
[Debugging R Code](https://rstats.wtf/debugging-r-code.html)
[Advanced R debugging](https://adv-r.hadley.nz/debugging.html)
[Debugging with the RStudio IDE](https://support.rstudio.com/hc/en-us/articles/205612627-Debugging-with-the-RStudio-IDE)

[github 1](https://github.com/annloh/fixURcode/tree/master/docs)
[github 2](https://github.com/hhy37/webinars-57-debugging-in-rstudio-)
[github 1](https://github.com/theavanrossum/debuggerRMarkdownLesson)
[github 1](https://github.com/RodrigRicardo/debuggingRStudio)
[git](https://github.com/ColinFay/debugin)


