---
title: Marketing Funnel Analysis
author: Oz Guner
date: '2023-04-16'
slug: marketing-funnel-analysis
categories:
  - projects
tags: ["marketing"]
keywords: ["what is a good conversion rate","cohorts","marketing funnel","leads","segmentation","demographics","marketing analysis","conversion rate"]
subtitle: 'Conversion Rates and Velocity by Cohorts'
excerpt: 'Conversion rates and conversion velocities are powerful tools in the toolkit of a marketer. It is important to look at the same data from different perspectives to gain more insightful and actionable information.'
summary: 'Conversion rates and conversion velocities are powerful tools in the toolkit of a marketer. It is important to look at the same data from different perspectives to gain more insightful and actionable information.'
draft: no
series: ~
layout: single-sidebar
---

<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/plotly-binding/plotly.js"></script>
<script src="{{< blogdown/postref >}}index_files/typedarray/typedarray.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/plotly-main/plotly-latest.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/plotly-binding/plotly.js"></script>
<script src="{{< blogdown/postref >}}index_files/typedarray/typedarray.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/plotly-main/plotly-latest.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/plotly-binding/plotly.js"></script>
<script src="{{< blogdown/postref >}}index_files/typedarray/typedarray.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/plotly-main/plotly-latest.min.js"></script>

### Goal

The goal of this project is to study conversion rates and conversion rate velocities by cohorts. While you can use different tools to achieve the same results, I will be including the R code step by step to (hopefully) create impactful visualizations.

### Setup

We have a few simple datasets in hand that we downloaded from our system of records. Let’s look at our base dataset:

``` r
#install the readr package to read our csv, which contains basic data
library(readr)
df <- read_csv("C:/Users/ozeng/Documents/R Repository/portfolio/portfolio/content/project/2023-04-16-marketing-funnel-analysis/base.csv")
```

    ## Rows: 4 Columns: 3
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): month
    ## dbl (2): created, converted
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
#view data
df
```

    ## # A tibble: 4 × 3
    ##   month         created converted
    ##   <chr>           <dbl>     <dbl>
    ## 1 January 2023     3235        60
    ## 2 February 2023    2899        57
    ## 3 March 2023       2888        30
    ## 4 April 2023        744        18

Looks like this data is aggregated by month. Let’s find the conversion rate for each month.

``` r
# create a new column for the conversion rate
df$conversion_rate <- df$converted / df$created
# print the updated data frame
df
```

    ## # A tibble: 4 × 4
    ##   month         created converted conversion_rate
    ##   <chr>           <dbl>     <dbl>           <dbl>
    ## 1 January 2023     3235        60          0.0185
    ## 2 February 2023    2899        57          0.0197
    ## 3 March 2023       2888        30          0.0104
    ## 4 April 2023        744        18          0.0242

Let’s create a visualization of the conversion rate by month so we have a more insightful look into our marketing funnel:

``` r
library(plotly)
```

    ## Loading required package: ggplot2

    ## 
    ## Attaching package: 'plotly'

    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     last_plot

    ## The following object is masked from 'package:stats':
    ## 
    ##     filter

    ## The following object is masked from 'package:graphics':
    ## 
    ##     layout

``` r
# sort the data by month
df$month <- factor(df$month, levels = c("January 2023", "February 2023", "March 2023", "April 2023"))

# create the plot
plot_ly(df, x = ~month) %>%
  add_trace(y = ~created, name = "Created", type = "bar", marker = list(color = "#4aa564"),
            text = ~paste0(created)) %>%
  add_trace(y = ~converted, name = "Converted", type = "bar", marker = list(color = "#fdb81e"),
            text = ~paste0(converted)) %>%
  add_trace(y = ~conversion_rate, name = "Conversion Rate", type = "scatter", mode = "lines", yaxis = "y2",
            line = list(color = "#046b99"), marker = list(color = "#046b99"),
            text = ~paste0(scales::percent(conversion_rate, accuracy = 0.01))) %>%
  layout(title = "Conversion Rate by Month",
         xaxis = list(title = "Month"),
         yaxis = list(title = "Created/Converted Count", side = "right",
                      tickfont = list(size = 12),
                      tickformat = ",.0f",
                      showticklabels = TRUE,
                      showgrid = FALSE),
         yaxis2 = list(title = "Conversion Rate (%)", side = "left", overlaying = "y",
                       tickfont = list(size = 12),
                       tickformat = ".2%",
                       tickvals = seq(0, 1, 0.1),
                       tickmode = "linear",
                       textfont = list(size = 12),
                       showticklabels = TRUE,
                       showgrid = TRUE,
                       zeroline = TRUE),
         legend = list(x = 0.5, y = -0.2, orientation = "h",
                       font = list(size = 12),
                       xanchor = "center",
                       yanchor = "top"))
```

    ## A marker object has been specified, but markers is not in the mode
    ## Adding markers to the mode...

<div class="plotly html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-1" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"visdat":{"3c382eca3ee8":["function () ","plotlyVisDat"]},"cur_data":"3c382eca3ee8","attrs":{"3c382eca3ee8":{"x":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"y":{},"name":"Created","type":"bar","marker":{"color":"#4aa564"},"text":{},"inherit":true},"3c382eca3ee8.1":{"x":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"y":{},"name":"Converted","type":"bar","marker":{"color":"#fdb81e"},"text":{},"inherit":true},"3c382eca3ee8.2":{"x":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"y":{},"name":"Conversion Rate","type":"scatter","mode":"lines","yaxis":"y2","line":{"color":"#046b99"},"marker":{"color":"#046b99"},"text":{},"inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":"Conversion Rate by Month","xaxis":{"domain":[0,1],"automargin":true,"title":"Month","type":"category","categoryorder":"array","categoryarray":["January 2023","February 2023","March 2023","April 2023"]},"yaxis":{"domain":[0,1],"automargin":true,"title":"Created/Converted Count","side":"right","tickfont":{"size":12},"tickformat":",.0f","showticklabels":true,"showgrid":false},"yaxis2":{"title":"Conversion Rate (%)","side":"left","overlaying":"y","tickfont":{"size":12},"tickformat":".2%","tickvals":[0,0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,1],"tickmode":"linear","textfont":{"size":12},"showticklabels":true,"showgrid":true,"zeroline":true},"legend":{"x":0.5,"y":-0.2,"orientation":"h","font":{"size":12},"xanchor":"center","yanchor":"top"},"hovermode":"closest","showlegend":true},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"x":["January 2023","February 2023","March 2023","April 2023"],"y":[3235,2899,2888,744],"name":"Created","type":"bar","marker":{"color":"#4aa564","line":{"color":"rgba(31,119,180,1)"}},"text":["3235","2899","2888","744"],"error_y":{"color":"rgba(31,119,180,1)"},"error_x":{"color":"rgba(31,119,180,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":["January 2023","February 2023","March 2023","April 2023"],"y":[60,57,30,18],"name":"Converted","type":"bar","marker":{"color":"#fdb81e","line":{"color":"rgba(255,127,14,1)"}},"text":["60","57","30","18"],"error_y":{"color":"rgba(255,127,14,1)"},"error_x":{"color":"rgba(255,127,14,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":["January 2023","February 2023","March 2023","April 2023"],"y":[0.0185471406491499,0.0196619523973784,0.010387811634349,0.0241935483870968],"name":"Conversion Rate","type":"scatter","mode":"lines+markers","yaxis":"y2","line":{"color":"#046b99"},"marker":{"color":"#046b99","line":{"color":"rgba(44,160,44,1)"}},"text":["1.85%","1.97%","1.04%","2.42%"],"error_y":{"color":"rgba(44,160,44,1)"},"error_x":{"color":"rgba(44,160,44,1)"},"xaxis":"x","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

This chart communicates the leads created in a month and converted in the same month. February seems to have a higher conversion rate than January. April is going really well and March might need a little help.

There’s one caveat in looking at conversion rates in a simple way. The 57 units converted in February might not all be created in February. There’s another way to look at this problem: The cohort velocity method. Let’s create a spaghetti chart that showcases how fast leads from a cohort convert to a paid client:

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(plotly)
library
```

    ## function (package, help, pos = 2, lib.loc = NULL, character.only = FALSE, 
    ##     logical.return = FALSE, warn.conflicts, quietly = FALSE, 
    ##     verbose = getOption("verbose"), mask.ok, exclude, include.only, 
    ##     attach.required = missing(include.only)) 
    ## {
    ##     conf.ctrl <- getOption("conflicts.policy")
    ##     if (is.character(conf.ctrl)) 
    ##         conf.ctrl <- switch(conf.ctrl, strict = list(error = TRUE, 
    ##             warn = FALSE), depends.ok = list(error = TRUE, generics.ok = TRUE, 
    ##             can.mask = c("base", "methods", "utils", "grDevices", 
    ##                 "graphics", "stats"), depends.ok = TRUE), warning(gettextf("unknown conflict policy: %s", 
    ##             sQuote(conf.ctrl)), call. = FALSE, domain = NA))
    ##     if (!is.list(conf.ctrl)) 
    ##         conf.ctrl <- NULL
    ##     stopOnConflict <- isTRUE(conf.ctrl$error)
    ##     if (missing(warn.conflicts)) 
    ##         warn.conflicts <- !isFALSE(conf.ctrl$warn)
    ##     if (!missing(include.only) && !missing(exclude)) 
    ##         stop("only one of 'include.only' and 'exclude' can be used", 
    ##             call. = FALSE)
    ##     testRversion <- function(pkgInfo, pkgname, pkgpath) {
    ##         if (is.null(built <- pkgInfo$Built)) 
    ##             stop(gettextf("package %s has not been installed properly\n", 
    ##                 sQuote(pkgname)), call. = FALSE, domain = NA)
    ##         R_version_built_under <- as.numeric_version(built$R)
    ##         if (R_version_built_under < "3.0.0") 
    ##             stop(gettextf("package %s was built before R 3.0.0: please re-install it", 
    ##                 sQuote(pkgname)), call. = FALSE, domain = NA)
    ##         current <- getRversion()
    ##         if (length(Rdeps <- pkgInfo$Rdepends2)) {
    ##             for (dep in Rdeps) if (length(dep) > 1L) {
    ##                 target <- dep$version
    ##                 res <- do.call(dep$op, if (is.character(target)) 
    ##                   list(as.numeric(R.version[["svn rev"]]), as.numeric(sub("^r", 
    ##                     "", target)))
    ##                 else list(current, as.numeric_version(target)))
    ##                 if (!res) 
    ##                   stop(gettextf("This is R %s, package %s needs %s %s", 
    ##                     current, sQuote(pkgname), dep$op, target), 
    ##                     call. = FALSE, domain = NA)
    ##             }
    ##         }
    ##         if (R_version_built_under > current) 
    ##             warning(gettextf("package %s was built under R version %s", 
    ##                 sQuote(pkgname), as.character(built$R)), call. = FALSE, 
    ##                 domain = NA)
    ##         platform <- built$Platform
    ##         r_arch <- .Platform$r_arch
    ##         if (.Platform$OS.type == "unix") {
    ##         }
    ##         else {
    ##             if (nzchar(platform) && !grepl("mingw", platform)) 
    ##                 stop(gettextf("package %s was built for %s", 
    ##                   sQuote(pkgname), platform), call. = FALSE, 
    ##                   domain = NA)
    ##         }
    ##         if (nzchar(r_arch) && file.exists(file.path(pkgpath, 
    ##             "libs")) && !file.exists(file.path(pkgpath, "libs", 
    ##             r_arch))) 
    ##             stop(gettextf("package %s is not installed for 'arch = %s'", 
    ##                 sQuote(pkgname), r_arch), call. = FALSE, domain = NA)
    ##     }
    ##     checkNoGenerics <- function(env, pkg) {
    ##         nenv <- env
    ##         ns <- .getNamespace(as.name(pkg))
    ##         if (!is.null(ns)) 
    ##             nenv <- asNamespace(ns)
    ##         if (exists(".noGenerics", envir = nenv, inherits = FALSE)) 
    ##             TRUE
    ##         else {
    ##             !any(startsWith(names(env), ".__T"))
    ##         }
    ##     }
    ##     checkConflicts <- function(package, pkgname, pkgpath, nogenerics, 
    ##         env) {
    ##         dont.mind <- c("last.dump", "last.warning", ".Last.value", 
    ##             ".Random.seed", ".Last.lib", ".onDetach", ".packageName", 
    ##             ".noGenerics", ".required", ".no_S3_generics", ".Depends", 
    ##             ".requireCachedGenerics")
    ##         sp <- search()
    ##         lib.pos <- which(sp == pkgname)
    ##         ob <- names(as.environment(lib.pos))
    ##         if (!nogenerics) {
    ##             these <- ob[startsWith(ob, ".__T__")]
    ##             gen <- gsub(".__T__(.*):([^:]+)", "\\1", these)
    ##             from <- gsub(".__T__(.*):([^:]+)", "\\2", these)
    ##             gen <- gen[from != package]
    ##             ob <- ob[!(ob %in% gen)]
    ##         }
    ##         ipos <- seq_along(sp)[-c(lib.pos, match(c("Autoloads", 
    ##             "CheckExEnv"), sp, 0L))]
    ##         cpos <- NULL
    ##         conflicts <- vector("list", 0)
    ##         for (i in ipos) {
    ##             obj.same <- match(names(as.environment(i)), ob, nomatch = 0L)
    ##             if (any(obj.same > 0L)) {
    ##                 same <- ob[obj.same]
    ##                 same <- same[!(same %in% dont.mind)]
    ##                 Classobjs <- which(startsWith(same, ".__"))
    ##                 if (length(Classobjs)) 
    ##                   same <- same[-Classobjs]
    ##                 same.isFn <- function(where) vapply(same, exists, 
    ##                   NA, where = where, mode = "function", inherits = FALSE)
    ##                 same <- same[same.isFn(i) == same.isFn(lib.pos)]
    ##                 not.Ident <- function(ch, TRAFO = identity, ...) vapply(ch, 
    ##                   function(.) !identical(TRAFO(get(., i)), TRAFO(get(., 
    ##                     lib.pos)), ...), NA)
    ##                 if (length(same)) 
    ##                   same <- same[not.Ident(same)]
    ##                 if (length(same) && identical(sp[i], "package:base")) 
    ##                   same <- same[not.Ident(same, ignore.environment = TRUE)]
    ##                 if (length(same)) {
    ##                   conflicts[[sp[i]]] <- same
    ##                   cpos[sp[i]] <- i
    ##                 }
    ##             }
    ##         }
    ##         if (length(conflicts)) {
    ##             if (stopOnConflict) {
    ##                 emsg <- ""
    ##                 pkg <- names(conflicts)
    ##                 notOK <- vector("list", 0)
    ##                 for (i in seq_along(conflicts)) {
    ##                   pkgname <- sub("^package:", "", pkg[i])
    ##                   if (pkgname %in% canMaskEnv$canMask) 
    ##                     next
    ##                   same <- conflicts[[i]]
    ##                   if (is.list(mask.ok)) 
    ##                     myMaskOK <- mask.ok[[pkgname]]
    ##                   else myMaskOK <- mask.ok
    ##                   if (isTRUE(myMaskOK)) 
    ##                     same <- NULL
    ##                   else if (is.character(myMaskOK)) 
    ##                     same <- setdiff(same, myMaskOK)
    ##                   if (length(same)) {
    ##                     notOK[[pkg[i]]] <- same
    ##                     msg <- .maskedMsg(sort(same), pkg = sQuote(pkg[i]), 
    ##                       by = cpos[i] < lib.pos)
    ##                     emsg <- paste(emsg, msg, sep = "\n")
    ##                   }
    ##                 }
    ##                 if (length(notOK)) {
    ##                   msg <- gettextf("Conflicts attaching package %s:\n%s", 
    ##                     sQuote(package), emsg)
    ##                   stop(errorCondition(msg, package = package, 
    ##                     conflicts = conflicts, class = "packageConflictError"))
    ##                 }
    ##             }
    ##             if (warn.conflicts) {
    ##                 packageStartupMessage(gettextf("\nAttaching package: %s\n", 
    ##                   sQuote(package)), domain = NA)
    ##                 pkg <- names(conflicts)
    ##                 for (i in seq_along(conflicts)) {
    ##                   msg <- .maskedMsg(sort(conflicts[[i]]), pkg = sQuote(pkg[i]), 
    ##                     by = cpos[i] < lib.pos)
    ##                   packageStartupMessage(msg, domain = NA)
    ##                 }
    ##             }
    ##         }
    ##     }
    ##     if (verbose && quietly) 
    ##         message("'verbose' and 'quietly' are both true; being verbose then ..")
    ##     if (!missing(package)) {
    ##         if (is.null(lib.loc)) 
    ##             lib.loc <- .libPaths()
    ##         lib.loc <- lib.loc[dir.exists(lib.loc)]
    ##         if (!character.only) 
    ##             package <- as.character(substitute(package))
    ##         if (length(package) != 1L) 
    ##             stop("'package' must be of length 1")
    ##         if (is.na(package) || (package == "")) 
    ##             stop("invalid package name")
    ##         pkgname <- paste0("package:", package)
    ##         newpackage <- is.na(match(pkgname, search()))
    ##         if (newpackage) {
    ##             pkgpath <- find.package(package, lib.loc, quiet = TRUE, 
    ##                 verbose = verbose)
    ##             if (length(pkgpath) == 0L) {
    ##                 if (length(lib.loc) && !logical.return) 
    ##                   stop(packageNotFoundError(package, lib.loc, 
    ##                     sys.call()))
    ##                 txt <- if (length(lib.loc)) 
    ##                   gettextf("there is no package called %s", sQuote(package))
    ##                 else gettext("no library trees found in 'lib.loc'")
    ##                 if (logical.return) {
    ##                   if (!quietly) 
    ##                     warning(txt, domain = NA)
    ##                   return(FALSE)
    ##                 }
    ##                 else stop(txt, domain = NA)
    ##             }
    ##             which.lib.loc <- normalizePath(dirname(pkgpath), 
    ##                 "/", TRUE)
    ##             pfile <- system.file("Meta", "package.rds", package = package, 
    ##                 lib.loc = which.lib.loc)
    ##             if (!nzchar(pfile)) 
    ##                 stop(gettextf("%s is not a valid installed package", 
    ##                   sQuote(package)), domain = NA)
    ##             pkgInfo <- readRDS(pfile)
    ##             testRversion(pkgInfo, package, pkgpath)
    ##             if (is.character(pos)) {
    ##                 npos <- match(pos, search())
    ##                 if (is.na(npos)) {
    ##                   warning(gettextf("%s not found on search path, using pos = 2", 
    ##                     sQuote(pos)), domain = NA)
    ##                   pos <- 2
    ##                 }
    ##                 else pos <- npos
    ##             }
    ##             deps <- unique(names(pkgInfo$Depends))
    ##             depsOK <- isTRUE(conf.ctrl$depends.ok)
    ##             if (depsOK) {
    ##                 canMaskEnv <- dynGet("__library_can_mask__", 
    ##                   NULL)
    ##                 if (is.null(canMaskEnv)) {
    ##                   canMaskEnv <- new.env()
    ##                   canMaskEnv$canMask <- union("base", conf.ctrl$can.mask)
    ##                   "__library_can_mask__" <- canMaskEnv
    ##                 }
    ##                 canMaskEnv$canMask <- unique(c(package, deps, 
    ##                   canMaskEnv$canMask))
    ##             }
    ##             else canMaskEnv <- NULL
    ##             if (attach.required) 
    ##                 .getRequiredPackages2(pkgInfo, quietly = quietly)
    ##             cr <- conflictRules(package)
    ##             if (missing(mask.ok)) 
    ##                 mask.ok <- cr$mask.ok
    ##             if (missing(exclude)) 
    ##                 exclude <- cr$exclude
    ##             if (packageHasNamespace(package, which.lib.loc)) {
    ##                 if (isNamespaceLoaded(package)) {
    ##                   newversion <- as.numeric_version(pkgInfo$DESCRIPTION["Version"])
    ##                   oldversion <- as.numeric_version(getNamespaceVersion(package))
    ##                   if (newversion != oldversion) {
    ##                     tryCatch(unloadNamespace(package), error = function(e) {
    ##                       P <- if (!is.null(cc <- conditionCall(e))) 
    ##                         paste("Error in", deparse(cc)[1L], ": ")
    ##                       else "Error : "
    ##                       stop(gettextf("Package %s version %s cannot be unloaded:\n %s", 
    ##                         sQuote(package), oldversion, paste0(P, 
    ##                           conditionMessage(e), "\n")), domain = NA)
    ##                     })
    ##                   }
    ##                 }
    ##                 tt <- tryCatch({
    ##                   attr(package, "LibPath") <- which.lib.loc
    ##                   ns <- loadNamespace(package, lib.loc)
    ##                   env <- attachNamespace(ns, pos = pos, deps, 
    ##                     exclude, include.only)
    ##                 }, error = function(e) {
    ##                   P <- if (!is.null(cc <- conditionCall(e))) 
    ##                     paste(" in", deparse(cc)[1L])
    ##                   else ""
    ##                   msg <- gettextf("package or namespace load failed for %s%s:\n %s", 
    ##                     sQuote(package), P, conditionMessage(e))
    ##                   if (logical.return && !quietly) 
    ##                     message(paste("Error:", msg), domain = NA)
    ##                   else stop(msg, call. = FALSE, domain = NA)
    ##                 })
    ##                 if (logical.return && is.null(tt)) 
    ##                   return(FALSE)
    ##                 attr(package, "LibPath") <- NULL
    ##                 {
    ##                   on.exit(detach(pos = pos))
    ##                   nogenerics <- !.isMethodsDispatchOn() || checkNoGenerics(env, 
    ##                     package)
    ##                   if (isFALSE(conf.ctrl$generics.ok) || (stopOnConflict && 
    ##                     !isTRUE(conf.ctrl$generics.ok))) 
    ##                     nogenerics <- TRUE
    ##                   if (stopOnConflict || (warn.conflicts && !exists(".conflicts.OK", 
    ##                     envir = env, inherits = FALSE))) 
    ##                     checkConflicts(package, pkgname, pkgpath, 
    ##                       nogenerics, ns)
    ##                   on.exit()
    ##                   if (logical.return) 
    ##                     return(TRUE)
    ##                   else return(invisible(.packages()))
    ##                 }
    ##             }
    ##             else stop(gettextf("package %s does not have a namespace and should be re-installed", 
    ##                 sQuote(package)), domain = NA)
    ##         }
    ##         if (verbose && !newpackage) 
    ##             warning(gettextf("package %s already present in search()", 
    ##                 sQuote(package)), domain = NA)
    ##     }
    ##     else if (!missing(help)) {
    ##         if (!character.only) 
    ##             help <- as.character(substitute(help))
    ##         pkgName <- help[1L]
    ##         pkgPath <- find.package(pkgName, lib.loc, verbose = verbose)
    ##         docFiles <- c(file.path(pkgPath, "Meta", "package.rds"), 
    ##             file.path(pkgPath, "INDEX"))
    ##         if (file.exists(vignetteIndexRDS <- file.path(pkgPath, 
    ##             "Meta", "vignette.rds"))) 
    ##             docFiles <- c(docFiles, vignetteIndexRDS)
    ##         pkgInfo <- vector("list", 3L)
    ##         readDocFile <- function(f) {
    ##             if (basename(f) %in% "package.rds") {
    ##                 txt <- readRDS(f)$DESCRIPTION
    ##                 if ("Encoding" %in% names(txt)) {
    ##                   to <- if (Sys.getlocale("LC_CTYPE") == "C") 
    ##                     "ASCII//TRANSLIT"
    ##                   else ""
    ##                   tmp <- try(iconv(txt, from = txt["Encoding"], 
    ##                     to = to))
    ##                   if (!inherits(tmp, "try-error")) 
    ##                     txt <- tmp
    ##                   else warning("'DESCRIPTION' has an 'Encoding' field and re-encoding is not possible", 
    ##                     call. = FALSE)
    ##                 }
    ##                 nm <- paste0(names(txt), ":")
    ##                 formatDL(nm, txt, indent = max(nchar(nm, "w")) + 
    ##                   3L)
    ##             }
    ##             else if (basename(f) %in% "vignette.rds") {
    ##                 txt <- readRDS(f)
    ##                 if (is.data.frame(txt) && nrow(txt)) 
    ##                   cbind(basename(gsub("\\.[[:alpha:]]+$", "", 
    ##                     txt$File)), paste(txt$Title, paste0(rep.int("(source", 
    ##                     NROW(txt)), ifelse(nzchar(txt$PDF), ", pdf", 
    ##                     ""), ")")))
    ##                 else NULL
    ##             }
    ##             else readLines(f)
    ##         }
    ##         for (i in which(file.exists(docFiles))) pkgInfo[[i]] <- readDocFile(docFiles[i])
    ##         y <- list(name = pkgName, path = pkgPath, info = pkgInfo)
    ##         class(y) <- "packageInfo"
    ##         return(y)
    ##     }
    ##     else {
    ##         if (is.null(lib.loc)) 
    ##             lib.loc <- .libPaths()
    ##         db <- matrix(character(), nrow = 0L, ncol = 3L)
    ##         nopkgs <- character()
    ##         for (lib in lib.loc) {
    ##             a <- .packages(all.available = TRUE, lib.loc = lib)
    ##             for (i in sort(a)) {
    ##                 file <- system.file("Meta", "package.rds", package = i, 
    ##                   lib.loc = lib)
    ##                 title <- if (nzchar(file)) {
    ##                   txt <- readRDS(file)
    ##                   if (is.list(txt)) 
    ##                     txt <- txt$DESCRIPTION
    ##                   if ("Encoding" %in% names(txt)) {
    ##                     to <- if (Sys.getlocale("LC_CTYPE") == "C") 
    ##                       "ASCII//TRANSLIT"
    ##                     else ""
    ##                     tmp <- try(iconv(txt, txt["Encoding"], to, 
    ##                       "?"))
    ##                     if (!inherits(tmp, "try-error")) 
    ##                       txt <- tmp
    ##                     else warning("'DESCRIPTION' has an 'Encoding' field and re-encoding is not possible", 
    ##                       call. = FALSE)
    ##                   }
    ##                   txt["Title"]
    ##                 }
    ##                 else NA
    ##                 if (is.na(title)) 
    ##                   title <- " ** No title available ** "
    ##                 db <- rbind(db, cbind(i, lib, title))
    ##             }
    ##             if (length(a) == 0L) 
    ##                 nopkgs <- c(nopkgs, lib)
    ##         }
    ##         dimnames(db) <- list(NULL, c("Package", "LibPath", "Title"))
    ##         if (length(nopkgs) && !missing(lib.loc)) {
    ##             pkglist <- paste(sQuote(nopkgs), collapse = ", ")
    ##             msg <- sprintf(ngettext(length(nopkgs), "library %s contains no packages", 
    ##                 "libraries %s contain no packages"), pkglist)
    ##             warning(msg, domain = NA)
    ##         }
    ##         y <- list(header = NULL, results = db, footer = NULL)
    ##         class(y) <- "libraryIQR"
    ##         return(y)
    ##     }
    ##     if (logical.return) 
    ##         TRUE
    ##     else invisible(.packages())
    ## }
    ## <bytecode: 0x000001d921651630>
    ## <environment: namespace:base>

``` r
# read the data from the csv file
data <- read.csv("C:/Users/ozeng/Documents/R Repository/portfolio/portfolio/content/blog/2023/04/14/the-great-conversion-rate-debate/cr_by_cohort.csv")
#let's look at the data
data%>% top_n(10)
```

    ## Selecting by converted_to_paid

    ##    created_cohort leads_signups days_to_convert converted_to_paid
    ## 1          23-Jan          3235              53                 5
    ## 2          23-Feb          2899              15                 4
    ## 3          23-Jan          3235              19                 4
    ## 4          23-Apr           744               2                 4
    ## 5          23-Apr           744               0                 4
    ## 6          23-Feb          2899               9                 5
    ## 7          23-Jan          3235               1                 4
    ## 8          23-Jan          3235               0                 7
    ## 9          23-Feb          2899               2                 5
    ## 10         23-Mar          2888               1                 4
    ## 11         23-Feb          2899               0                 6
    ## 12         23-Mar          2888               0                 4

Notice how the data is structured. Each record indicates a month cohort, the total leads/signups in that month, and the total leads/signups converted at specific days each month. Whenever there’s at least one unit converted at a specific day interval, one record will be created. Now let’s calculate the conversion rate for each record:

``` r
# calculate the conversion rate
conversion_rate <- data %>%
  filter(days_to_convert > 0) %>%
  group_by(days_to_convert, created_cohort) %>%
  summarize(conversion_rate = sum(converted_to_paid) / sum(leads_signups))
```

    ## `summarise()` has grouped output by 'days_to_convert'. You can override using
    ## the `.groups` argument.

``` r
conversion_rate
```

    ## # A tibble: 107 × 3
    ## # Groups:   days_to_convert [60]
    ##    days_to_convert created_cohort conversion_rate
    ##              <int> <chr>                    <dbl>
    ##  1               1 23-Jan                0.00124 
    ##  2               1 23-Mar                0.00139 
    ##  3               2 23-Apr                0.00538 
    ##  4               2 23-Feb                0.00172 
    ##  5               2 23-Jan                0.000927
    ##  6               2 23-Mar                0.00104 
    ##  7               3 23-Apr                0.00269 
    ##  8               3 23-Feb                0.000690
    ##  9               3 23-Mar                0.000693
    ## 10               4 23-Jan                0.000618
    ## # ℹ 97 more rows

In this case, a conversion rate is assigned for each record. If we are going to take a holistic view to look at the total leads converted at day X, we’d need to create a running conversion rate calculation, as follows:

``` r
# create a new dataframe with the running total
conversion_rate_running <- conversion_rate %>%
  group_by(created_cohort) %>%
  arrange(created_cohort, days_to_convert) %>%
  mutate(rt_conv = cumsum(conversion_rate)) %>%
  filter(days_to_convert > 0)  # remove the first value label
```

Notice that using the `cumsum()` method and grouping by cohort, you can create a running conversion rate in that specific cohort, which literally sums up the cumulative values.

Next, we’ll create a plotly chart:

``` r
# create the plotly chart
p <- # create the plotly chart with custom hover text
  plot_ly(data = conversion_rate_running, x = ~days_to_convert, y = ~rt_conv, color = ~created_cohort, type = "scatter", mode = "lines", showlegend = TRUE,
          hovertemplate = "On day %{x} of creation, the average conversion rate was %{y:.2%}.") %>%
  layout(title = "Conversion Rate by Days to Convert and Created Cohort",
         xaxis = list(title = "Days to Convert", showgrid = FALSE),
         yaxis = list(title = "Running Total Conversion Rate", tickformat = ".2%", showgrid = FALSE),
         legend = list(x = 0.05, y = 1, tracegroupgap = 0, traceorder = "grouped"),
         margin = list(l = 50, r = 50, b = 50, t = 50),
         hovermode = "x",
         colorway = c("#E7298A", "#66A61E", "#E6AB02", "#713122"))

# add data labels to the very last values
last_values <- conversion_rate_running %>%
  group_by(created_cohort) %>%
  slice_tail(n = 1)

for(i in 1:nrow(last_values)){
  p <- p %>% add_annotations(x = last_values$days_to_convert[i],
                             y = last_values$rt_conv[i],
                             text = paste0(round(last_values$rt_conv[i]*100, 2), "%"),
                             showarrow = FALSE, xshift = 10, yshift = 10)
}
p
```

<div class="plotly html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-2" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-2">{"x":{"visdat":{"3c3816c5216c":["function () ","plotlyVisDat"]},"cur_data":"3c3816c5216c","attrs":{"3c3816c5216c":{"x":{},"y":{},"mode":"lines","showlegend":true,"hovertemplate":"On day %{x} of creation, the average conversion rate was %{y:.2%}.","color":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scatter"}},"layout":{"margin":{"b":50,"l":50,"t":50,"r":50},"title":"Conversion Rate by Days to Convert and Created Cohort","xaxis":{"domain":[0,1],"automargin":true,"title":"Days to Convert","showgrid":false},"yaxis":{"domain":[0,1],"automargin":true,"title":"Running Total Conversion Rate","tickformat":".2%","showgrid":false},"legend":{"x":0.05,"y":1,"tracegroupgap":0,"traceorder":"grouped"},"hovermode":"x","colorway":["#E7298A","#66A61E","#E6AB02","#713122"],"annotations":[{"text":"1.88%","x":14,"y":0.0188172043010753,"showarrow":false,"xshift":10,"yshift":10},{"text":"2.1%","x":75,"y":0.0210417385305278,"showarrow":false,"xshift":10,"yshift":10},{"text":"2.41%","x":106,"y":0.0241112828438949,"showarrow":false,"xshift":10,"yshift":10},{"text":"0.83%","x":25,"y":0.00831024930747922,"showarrow":false,"xshift":10,"yshift":10}],"showlegend":true},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"x":[2,3,5,6,10,11,12,14],"y":[0.00537634408602151,0.00806451612903226,0.00940860215053763,0.010752688172043,0.0134408602150538,0.0147849462365591,0.0174731182795699,0.0188172043010753],"mode":"lines","showlegend":true,"hovertemplate":["On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}."],"type":"scatter","name":"23-Apr","marker":{"color":"rgba(102,194,165,1)","line":{"color":"rgba(102,194,165,1)"}},"textfont":{"color":"rgba(102,194,165,1)"},"error_y":{"color":"rgba(102,194,165,1)"},"error_x":{"color":"rgba(102,194,165,1)"},"line":{"color":"rgba(102,194,165,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[2,3,6,7,9,10,11,12,13,15,16,17,19,21,22,23,24,25,26,27,28,29,31,32,33,34,35,36,38,41,45,60,75],"y":[0.0017247326664367,0.00241462573301138,0.00310451879958606,0.00413935839944809,0.00586409106588479,0.00689893066574681,0.00758882373232149,0.00827871679889617,0.00896860986547085,0.0103483959986202,0.0106933425319076,0.0110382890651949,0.0113832355984822,0.0120731286650569,0.0127630217316316,0.0134529147982063,0.0137978613314936,0.0144877543980683,0.0148327009313556,0.015177647464643,0.016212487064505,0.0169023801310797,0.0175922731976544,0.0179372197309417,0.018282166264229,0.0186271127975164,0.0189720593308037,0.0193170058640911,0.0196619523973784,0.0200068989306657,0.0203518454639531,0.0206967919972404,0.0210417385305278],"mode":"lines","showlegend":true,"hovertemplate":["On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}."],"type":"scatter","name":"23-Feb","marker":{"color":"rgba(252,141,98,1)","line":{"color":"rgba(252,141,98,1)"}},"textfont":{"color":"rgba(252,141,98,1)"},"error_y":{"color":"rgba(252,141,98,1)"},"error_x":{"color":"rgba(252,141,98,1)"},"line":{"color":"rgba(252,141,98,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[1,2,4,5,7,8,9,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,41,42,47,48,49,52,53,54,57,60,61,63,69,70,71,73,75,77,88,97,103,106],"y":[0.00123647604327666,0.00216383307573416,0.00278207109737249,0.00340030911901082,0.00401854714064915,0.00432766615146832,0.00494590417310665,0.00587326120556414,0.00649149922720247,0.0071097372488408,0.00772797527047913,0.00834621329211747,0.0089644513137558,0.00989180834621329,0.0105100463678516,0.0112828438948995,0.0115919629057187,0.0119010819165379,0.0125193199381762,0.0128284389489954,0.0131375579598145,0.0134466769706337,0.0137557959814529,0.014064914992272,0.0146831530139104,0.0149922720247295,0.0153013910355487,0.0156105100463679,0.015919629057187,0.0162287480680062,0.0165378670788253,0.0168469860896445,0.0171561051004637,0.0174652241112828,0.017774343122102,0.0180834621329212,0.0183925811437403,0.0194744976816074,0.0197836166924266,0.0200927357032458,0.0204018547140649,0.0207109737248841,0.0210200927357032,0.0213292117465224,0.0216383307573416,0.0219474497681607,0.0222565687789799,0.0225656877897991,0.0228748068006182,0.0231839258114374,0.0234930448222566,0.0238021638330757,0.0241112828438949],"mode":"lines","showlegend":true,"hovertemplate":["On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}."],"type":"scatter","name":"23-Jan","marker":{"color":"rgba(141,160,203,1)","line":{"color":"rgba(141,160,203,1)"}},"textfont":{"color":"rgba(141,160,203,1)"},"error_y":{"color":"rgba(141,160,203,1)"},"error_x":{"color":"rgba(141,160,203,1)"},"line":{"color":"rgba(141,160,203,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[1,2,3,7,12,13,15,16,17,22,23,24,25],"y":[0.00138504155124654,0.00242382271468144,0.00311634349030471,0.00346260387811634,0.00415512465373961,0.00450138504155125,0.00519390581717452,0.00554016620498615,0.00623268698060942,0.00657894736842105,0.00727146814404432,0.00796398891966759,0.00831024930747922],"mode":"lines","showlegend":true,"hovertemplate":["On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}."],"type":"scatter","name":"23-Mar","marker":{"color":"rgba(231,138,195,1)","line":{"color":"rgba(231,138,195,1)"}},"textfont":{"color":"rgba(231,138,195,1)"},"error_y":{"color":"rgba(231,138,195,1)"},"error_x":{"color":"rgba(231,138,195,1)"},"line":{"color":"rgba(231,138,195,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

Remember that, in the single conversion rate method, our conversion rate for January was 1.85% and February was 1.97%. However, the cohort-based conversion rate paints a clearer picture by eliminating the time bias. January actually has a higher conversion rate with 2.41% versus February’s 2.1%. Moreover, January was converting at higher levels at on average on Day 75, where February is today: 2.26% vs 2.1%.

### Other ways to look at conversion velocity.

Another way to look at conversion velocity is by custom segmentation. Examples can include intent levels, demographics, and product actions. Let’s look at the same data from another perspective:

    ## Selecting by converted_to_paid

    ##      channel leads_signups days_to_convert converted_to_paid
    ## 1  Channel 2           835               8                 3
    ## 2  Channel 2           835               7                 5
    ## 3  Channel 2           835               6                 4
    ## 4  Channel 2           835               4                 5
    ## 5  Channel 2           835               3                 6
    ## 6  Channel 2           835               2                 5
    ## 7  Channel 2           835               1                 5
    ## 8  Channel 2           835               0                 7
    ## 9  Channel 3           333              19                 4
    ## 10 Channel 3           333               4                 3
    ## 11 Channel 1          1949              53                 5
    ## 12 Channel 1          1949              22                 3
    ## 13 Channel 1          1949              15                 3
    ## 14 Channel 1          1949               0                 3

Similar to the other dataset, this dataset communicates the speed to convert broken down by channels instead of time. Regardless of when they were created we can look at how leads from different channels convert.

``` r
# calculate the conversion rate
conversion_rate <- data %>%
  filter(days_to_convert > 0) %>%
  group_by(days_to_convert, channel) %>%
  summarize(conversion_rate = sum(converted_to_paid) / sum(leads_signups))
```

    ## `summarise()` has grouped output by 'days_to_convert'. You can override using
    ## the `.groups` argument.

``` r
# create a new dataframe with the running total
conversion_rate_running <- conversion_rate %>%
  group_by(channel) %>%
  arrange(channel, days_to_convert) %>%
  mutate(rt_conv = cumsum(conversion_rate)) %>%
  filter(days_to_convert > 0)  # remove the first value label

# create the plotly chart
p <- # create the plotly chart with custom hover text
  plot_ly(data = conversion_rate_running, x = ~days_to_convert, y = ~rt_conv, color = ~channel, type = "scatter", mode = "lines", showlegend = TRUE,
          hovertemplate = "On day %{x} of creation, the average conversion rate was %{y:.2%}.") %>%
  layout(title = "Conversion Rate by Days to Convert and Channel",
         xaxis = list(title = "Days to Convert", showgrid = FALSE),
         yaxis = list(title = "Running Total Conversion Rate", tickformat = ".2%", showgrid = FALSE),
         legend = list(x = 0.05, y = 1, tracegroupgap = 0, traceorder = "grouped"),
         margin = list(l = 50, r = 50, b = 50, t = 50),
         hovermode = "x",
         colorway = c("#E7298A", "#66A61E", "#E6AB02", "#713122"))

# add data labels to the very last values
last_values <- conversion_rate_running %>%
  group_by(channel) %>%
  slice_tail(n = 1)

for(i in 1:nrow(last_values)){
  p <- p %>% add_annotations(x = last_values$days_to_convert[i],
                             y = last_values$rt_conv[i],
                             text = paste0(round(last_values$rt_conv[i]*100, 2), "%"),
                             showarrow = FALSE, xshift = 10, yshift = 10)
}
p
```

<div class="plotly html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-3" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-3">{"x":{"visdat":{"3c3870d7259d":["function () ","plotlyVisDat"]},"cur_data":"3c3870d7259d","attrs":{"3c3870d7259d":{"x":{},"y":{},"mode":"lines","showlegend":true,"hovertemplate":"On day %{x} of creation, the average conversion rate was %{y:.2%}.","color":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"scatter"}},"layout":{"margin":{"b":50,"l":50,"t":50,"r":50},"title":"Conversion Rate by Days to Convert and Channel","xaxis":{"domain":[0,1],"automargin":true,"title":"Days to Convert","showgrid":false},"yaxis":{"domain":[0,1],"automargin":true,"title":"Running Total Conversion Rate","tickformat":".2%","showgrid":false},"legend":{"x":0.05,"y":1,"tracegroupgap":0,"traceorder":"grouped"},"hovermode":"x","colorway":["#E7298A","#66A61E","#E6AB02","#713122"],"annotations":[{"text":"1.77%","x":77,"y":0.0177013853258081,"showarrow":false,"xshift":10,"yshift":10},{"text":"7.54%","x":73,"y":0.0754491017964072,"showarrow":false,"xshift":10,"yshift":10},{"text":"16.82%","x":73,"y":0.168168168168168,"showarrow":false,"xshift":10,"yshift":10}],"showlegend":true},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"x":[3,6,9,11,15,22,23,24,27,30,31,34,47,52,53,57,60,63,69,71,77],"y":[0.00102616726526424,0.00205233453052848,0.00307850179579271,0.00410466906105695,0.00564391995895331,0.00667008722421755,0.00769625448948179,0.00846587993842996,0.0094920472036942,0.0100051308363263,0.0105182144689584,0.0110312981015906,0.0115443817342227,0.0120574653668548,0.0146228835300154,0.0151359671626475,0.0156490507952796,0.0161621344279117,0.0166752180605439,0.017188301693176,0.0177013853258081],"mode":"lines","showlegend":true,"hovertemplate":["On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}."],"type":"scatter","name":"Channel 1","marker":{"color":"rgba(102,194,165,1)","line":{"color":"rgba(102,194,165,1)"}},"textfont":{"color":"rgba(102,194,165,1)"},"error_y":{"color":"rgba(102,194,165,1)"},"error_x":{"color":"rgba(102,194,165,1)"},"line":{"color":"rgba(102,194,165,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[1,2,3,4,6,7,8,9,10,11,13,14,15,16,17,19,20,22,24,25,27,28,29,30,32,34,36,41,48,69,70,73],"y":[0.00598802395209581,0.0119760479041916,0.0191616766467066,0.0251497005988024,0.029940119760479,0.0359281437125748,0.0395209580838323,0.0407185628742515,0.0431137724550898,0.0455089820359281,0.0467065868263473,0.0491017964071856,0.0502994011976048,0.051497005988024,0.0538922155688623,0.0550898203592814,0.0574850299401198,0.0586826347305389,0.0598802395209581,0.0610778443113772,0.0622754491017964,0.0634730538922156,0.0646706586826347,0.0658682634730539,0.067065868263473,0.0682634730538922,0.0694610778443114,0.0706586826347305,0.0718562874251497,0.0730538922155689,0.074251497005988,0.0754491017964072],"mode":"lines","showlegend":true,"hovertemplate":["On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}."],"type":"scatter","name":"Channel 2","marker":{"color":"rgba(252,141,98,1)","line":{"color":"rgba(252,141,98,1)"}},"textfont":{"color":"rgba(252,141,98,1)"},"error_y":{"color":"rgba(252,141,98,1)"},"error_x":{"color":"rgba(252,141,98,1)"},"line":{"color":"rgba(252,141,98,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":[2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,34,37,39,41,42,44,47,49,50,53,54,57,61,73],"y":[0.003003003003003,0.00600600600600601,0.015015015015015,0.018018018018018,0.024024024024024,0.027027027027027,0.03003003003003,0.036036036036036,0.039039039039039,0.042042042042042,0.045045045045045,0.048048048048048,0.0510510510510511,0.0540540540540541,0.0570570570570571,0.0600600600600601,0.0660660660660661,0.0780780780780781,0.0810810810810811,0.0840840840840841,0.0870870870870871,0.0900900900900901,0.0930930930930931,0.0990990990990991,0.102102102102102,0.108108108108108,0.111111111111111,0.114114114114114,0.117117117117117,0.12012012012012,0.126126126126126,0.129129129129129,0.132132132132132,0.135135135135135,0.138138138138138,0.141141141141141,0.144144144144144,0.147147147147147,0.15015015015015,0.156156156156156,0.159159159159159,0.162162162162162,0.165165165165165,0.168168168168168],"mode":"lines","showlegend":true,"hovertemplate":["On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}.","On day %{x} of creation, the average conversion rate was %{y:.2%}."],"type":"scatter","name":"Channel 3","marker":{"color":"rgba(141,160,203,1)","line":{"color":"rgba(141,160,203,1)"}},"textfont":{"color":"rgba(141,160,203,1)"},"error_y":{"color":"rgba(141,160,203,1)"},"error_x":{"color":"rgba(141,160,203,1)"},"line":{"color":"rgba(141,160,203,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

In this case, Channel 3 converts the best, followed by Channel 2 and Channel 1. Looking at this data with time controls could introduce even more insights as different channels might convert at different circumstances.

### Conclusion

Conversion rates and conversion velocities are powerful tools in a marketer’s toolkit. It’s important to look at the same data from different perspectives to gain more insightful and actionable information.
