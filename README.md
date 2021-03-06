
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Coding Workshop: Tables in RMarkdown 2021-11-18

## Pros and Cons of Table Packages

### {gt}

    - Pro: Looks really good by default (best looking html in my opinion!)
    - Pro: Footnotes fully featured
    - Pro: Can use tidyselect to select data rows/cols. Generally adheres to tidyverse style guide 
    - Pro: Great documentation 
    - Con: Word not yet supported, PDF/RTF under development BUT gtsummary objects will automatically default to other print engines so you can knit to other outputs. Non-gtsummary objects will just not print in final document. 
    - Con: Can't have more than 2 spanning headers - although gt will support this soon

### {huxtable}

    - Pro: Works well with html, pdf, rtf and word outputs
    - Pro: You can save the latex code with the `as_latex()` directly- helpful when you have to write docs with latex
    - Con: I find the documentation confusing
    - Con: Default settings are not as nice looking as flextable and gt (although once you add compact theme they look better)
    - Con: For gtsummary tables, you may lose the footnote numbering. Footnote still appears but without numbers
    - Con: Hux table doesn’t let you see it in the viewer like gt. Prints as markdown, making it harder to preview
    - Con: Footnotes have limited support
    - Con: While gtsummary does a lot of the leg work customizing tables for gtsummary objects, non-gtsummary tables can be cumbesome to try to customize 

### {flextable}

    - Pro: Footnotes fully featured
    - Pro: Works well with html and pdf. Best word output in my opinion
    - Pro: Great documentation 
    - Con: Can't use tidyselect to index rows/cols

### {kable} + {kableExtra}

    - Formatting options more limited, but this can be useful for dashboards (it sizes tables better than gt and offers some limited reactivate like scroll over)

# Summary:

-   gt is best for HTML, and is currently under construction for PDF and
    RTF (aka Word). gt is already pretty great for PDF and RTF, but not
    all formatting is available for the outputs. They will release it
    soon however

-   flextable works well for Word and PowerPoint. While PDF is
    technically supported, flextable just makes an image and puts it
    into a PDF document.

-   huxtable is best for the LaTeX output (which includes PDF). Has a
    lot of output options but doesn’t look as good right out of the box.

# Resources

-   gt documention: <https://gt.rstudio.com/>

-   flextable documentation:
    <https://ardata-fr.github.io/flextable-book/>

-   huxtable documentation:
    <https://hughjonesd.github.io/huxtable/reference/index.html>

-   gtsummary + RMarkdown:
    <https://www.danieldsjoberg.com/gtsummary/articles/rmarkdown.html>

-   flextable complex table:
    <https://stackoverflow.com/questions/70059022/reproduce-a-complex-table-with-double-headesrs/70072503#70072503>

-   `bstfun::style_tbl_compact()`

## Some Formatting Functions for Word/PDF Outputs

-   huxtable: `width(table)` &lt;- 0.8
-   flextable: set table properties to autofit! This helps automatically
    pick a width

``` r
trial %>%
  tbl_summary() %>%
  as_flex_table() %>%
  flextable::set_table_properties(layout = "autofit")
```

## Other tips

-   Load biostatR instead of gtsummary- then you won’t have trouble with
    renv
-   Code to manipulate gtsummary tables and omit estimates above/below a
    certain threshold (e.g. unstable OR estimates):

``` r
x <- trial %>% 
  gtsummary::tbl_uvregression(y = age, 
                   method = lm)

x
```

Adjust `x$table_body` internals:

``` r
x$table_body <- x$table_body %>%
  mutate(estimate = dplyr::case_when(
             estimate < 0 ~ NA_real_, 
                     TRUE ~ estimate))

x
```
