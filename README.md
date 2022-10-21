# INF4000 Week 5: 
# Trouble shooting with Google: where the programming starts
![a](https://github.com/casszhao/INF4000.github.io/raw/main/debugging.jpg)


Noted this week is 
* **NOT** about advanced techniques and skills for R studio
* **NOT** about following each step and reproducing each result or graphs
* about practice solving problems **on your own**
* **Dont rush** doing this worksheet. 
* Better way to use this worksheet: stop and think how you will do to find the soluation, how you want to approach the issue, and then move on.




Learning objective:

* To use right sources and platform to search and debug
* To locate problem
* To formulate a "good" question





When see errors, do not panic.

Coders/data scientists, fix errors and mistakes, all the time. Today, let s talk about how to troubleshoot yourself.

After a while of coding, you will know how and where to start to fix the problem. Before that, you can try following general strategies to debug an error:



1. **Google**
 * Read the ERROR MESSAGE! Most error message does tell you what the problem is. Google it.
 * Many times it is a common error with a known solution. Sometime, even just copy paste your error message, you will find many people had the exactly issue like yours before.
 * Change a way to describe your problem if you cannot find the solution. 
 * Sometime, results from Google costs a lot of time to filter (particularly, when you ask in a not so good way), try other professional platforms, such as: stackoverflow, w3schools.com, codeproject.com


2. **Go back to your dataset**

Just check your data, even it is readable and loadable.
        
       
2. **Repeate it with simpler/smaller data**
 * Create a minimal, reproducible example using simple data
 * Note which inputs don’t trigger the error
 * If not already done, write simple tests to reduce chances of creating a new bug


3. **Figure out where the error is** 
 * Use the “scientific method”, e.g. repeate it a little bit differently (modify your code/arguments just a tiny bit. When modify, try to only change a single variable. In such an way, it is easy to compare and then locate the problem.)
 * Hypothesize, test with experiments, and record results
 * If needed, ask someone else for a second pair of eyes to review

4. **Dont be afraid of testing around**
* Just try it







These steps should be followed each time you encounter an unexpected error. Many times, you may not even know what line of code the error is coming from. How can you determine where the code is not behaving? You can follow these general steps to answer this question:

 * Begin running the code.
 * Stop the code where you suspect the bug/problem is arising.
 * If necessary, try removing the suspected line to see the changes in the result.
 * Look and/or walk through the code, step-by-step at that point.
 * [**Rubber duck debugging**](https://en.wikipedia.org/wiki/Rubber_duck_debugging). Explain your code to a rubber duck line by line. It will suprise you sometime that you figure out the problem during the process when you talk to your duck. So time to amazon yourself a rubber duck.

![a](rubbder_duck.jpg)


 This can be done ad-hoc in a separate R script containing the function code, or using several built-in tools in RStudio. 


## Case study: Trouble shooting with via playing around

When debugging, do not afraid trying or playing around. Sometime you solve the problem unintentionally when you play around.

One question a student asked from last week: 

> why the coordinate does not show "2020"?

![a](coordinator.png)


Let s check the code 

```r
ggplot(country_data,aes(year, NY.GDP.PCAP.KD.ZG) ) +
  geom_point(aes(colour =country)) +
  facet_grid(region ~ income) +
  labs(x="Year", y="GDP Per Capita Growth (annual %)",
       title='Faceting test', subtitle = 'Facet on both axes',
       colour="Country",
       caption='World Development Indicators, World Bank') +
       scale_x_continuous(breaks=seq(2000,2020,10))
```

So the problem is about the coordinate. Let s investigate line by line. Obviously, the first few lines should be fine, as they just indicate the data or set up textual titles. E.g., ```aes(year, NY.GDP.PCAP.KD.ZG)```, ``` x= ``` and ``` y= ``` just indicate data, should be fine. Similar for ```title=```, ```colour=``` and ```caption=```.

So we initially focus on 
Within the code, lines regarding coordinate are

```r
scale_x_continuous(breaks=seq(2000,2020,10))
```

We go back to [WEEK 4 material](https://vle.shef.ac.uk/webapps/blackboard/content/listContentEditable.jsp?content_id=_6272367_1&course_id=_103961_1#) to see what it says about ```scale_x_continuous``` (```control+F``` to locate it in the file):
> You can modify which values are shown on the axis of a continuous variable using the **scale_x_continuous** for X axis and scale_y_continuous for Y axis. That function expects a list of numerical values on which to draw axis numbers, and this can easily be created with the seq function. You can use these functions in any plot, not just those with faceting enabled. The example below reduces the number of values shown on the X axis to create a cleaner plot.

After read this, we probably further confirm that ```scale_x_continuous``` is where we should look at. 
Let s further dig into this line/argument by just googling it --> ["scale_x_continuous"]([https://www.google.com/search?q=scale_x_continuous(breaks%3Dseq(2000%2C2020%2C10))&oq=scale_x_continuous(breaks%3Dseq(2000%2C2020%2C10))&aqs=chrome.0.69i59.425j0j7&sourceid=chrome&ie=UTF-8](https://www.google.com/search?q=scale_x_continuous&sxsrf=ALiCzsZ0siBuC0xWiandh7D2MpLGYriRyA%3A1666300368588&ei=0LlRY7W1I_iE9u8Py8uA-A0&ved=0ahUKEwi13bvM3O_6AhV4gv0HHcslAN8Q4dUDCA8&uact=5&oq=scale_x_continuous&gs_lp=Egdnd3Mtd2l6uAED-AEC-AEBMgQQIxgnMgQQABhDMgQQABhDMgQQABhDMgQQABhDMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABDIFEAAYgARI1wVQAFgAcAB4AcgBAJABAJgBXqABXqoBATHiAwQgTRgB4gMEIEEYAOIDBCBGGACIBgE&sclient=gws-wiz))

We go for the first result retrieved (It is possible that you have got something else as your first returned result. It does not matter, what we want is to know more about scale_x_continuous). This leads us to the ggplot2 documentation. PERFECT. Conventionally, **a documentation is the most official introduction for a function/package. And it is usually one of the most comprehensive one.**

Now, maybe we can try scaling up the range of the coordinate to see if 2020 will show up.
Let s try ```scale_x_continuous(breaks=seq(2000,2022,10))``` instead of ```scale_x_continuous(breaks=seq(2000,2020,10))```
Then you will find nothing change. Let s try ```scale_x_continuous(breaks=seq(1998,2022,10))``` Now something changes.
![a](screenshot_years1.png)



Let's check the "year" in the original dataset. We sort the 



## Case study: Fuction
Next, let’s look at an example function.






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
*[Hands-On Programming with R(]https://rstudio-education.github.io/hopr/debug.html)
*[A case study in debugging R](https://github.com/karawoo/2019-01-17-rstudioconf/blob/master/woo_rstudioconf_2019.pdf)
*[Debugging R Code](https://rstats.wtf/debugging-r-code.html)
*[Advanced R debugging](https://adv-r.hadley.nz/debugging.html)
*[Debugging with the RStudio IDE](https://support.rstudio.com/hc/en-us/articles/205612627-Debugging-with-the-RStudio-IDE)

[github 1](https://github.com/annloh/fixURcode/tree/master/docs)
[github 2](https://github.com/hhy37/webinars-57-debugging-in-rstudio-)
[github 1](https://github.com/theavanrossum/debuggerRMarkdownLesson)
[github 1](https://github.com/RodrigRicardo/debuggingRStudio)
[git](https://github.com/ColinFay/debugin)


