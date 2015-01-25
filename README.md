Embeding help into Shiny App
========================================================

Presendation covers:
- Possible Embedding HTML and MD to the Shiny application
- Layouting
- Actual example

Ways to embed HTML and MD 1
========================================================

Methods:
- Shiny [tags](http://shiny.rstudio.com/articles/html-tags.html) for html fragments e.g.

```
tags$div(class="header", checked=NA,
         tags$p("Ready to take the Shiny tutorial? If so"),
         tags$a(href="shiny.rstudio.com/tutorial", "Click Here!")
)
```

- [Embeding](http://shiny.rstudio.com/articles/interactive-docs.html) Shiny into .Rmd 

It is good for inserting small intrractive Shiny fragments inside larger markdown document.


Ways to embed HTML and MD 2
========================================================
- [Including .html or .md in ui.R](http://shiny.rstudio.com/gallery/including-html-text-and-markdown-files.html) e.g.
```
includeMarkdown("include.md")
```

```
includeHTML("include.html")
```

It is way I selected to include documentation of my Shiny application as part of application itself:
 1. Write help in .md. Note: including of md is not compatible [shiny.io](shiny.io).
 2. Generage .html.
 3. include .html content into ui.R.
 4. Publish into [shiny.io](shiny.io).

Layout in Shiny application
========================================================
Adding html document to existing Shiny applications requires some layouting decisions:
 * Adding as header;
 * Adding below output;
 * Adding as separate tab. It was selected for final implementation:
 
```
mainPanel(
    tabsetPanel(
      tabPanel("Plot", plotOutput('plot')),
      tabPanel("Documentation", includeHTML("README.html"))
    )
  )
```

Demonstration
========================================================
For outcome of the presentation see [Simple Car Explorer Application](http://pranasblk.shinyapps.io/CarsExplorer/).

The application analyses `mtcars` data set:

```r
head(mtcars, 3)
```

```
               mpg cyl disp  hp drat    wt  qsec vs am gear carb
Mazda RX4     21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
Mazda RX4 Wag 21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
Datsun 710    22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
```
