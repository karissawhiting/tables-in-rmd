
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Coding Workshop: Tables in RMarkdown -11-18

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

<div id="whhlnmjecw" style="overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>html {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Helvetica Neue', 'Fira Sans', 'Droid Sans', Arial, sans-serif;
}

#whhlnmjecw .gt_table {
  display: table;
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#whhlnmjecw .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#whhlnmjecw .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#whhlnmjecw .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 0;
  padding-bottom: 6px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#whhlnmjecw .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#whhlnmjecw .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#whhlnmjecw .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#whhlnmjecw .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#whhlnmjecw .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#whhlnmjecw .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#whhlnmjecw .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#whhlnmjecw .gt_group_heading {
  padding: 8px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
}

#whhlnmjecw .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#whhlnmjecw .gt_from_md > :first-child {
  margin-top: 0;
}

#whhlnmjecw .gt_from_md > :last-child {
  margin-bottom: 0;
}

#whhlnmjecw .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#whhlnmjecw .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 12px;
}

#whhlnmjecw .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#whhlnmjecw .gt_first_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
}

#whhlnmjecw .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#whhlnmjecw .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#whhlnmjecw .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#whhlnmjecw .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#whhlnmjecw .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#whhlnmjecw .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding: 4px;
}

#whhlnmjecw .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#whhlnmjecw .gt_sourcenote {
  font-size: 90%;
  padding: 4px;
}

#whhlnmjecw .gt_left {
  text-align: left;
}

#whhlnmjecw .gt_center {
  text-align: center;
}

#whhlnmjecw .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#whhlnmjecw .gt_font_normal {
  font-weight: normal;
}

#whhlnmjecw .gt_font_bold {
  font-weight: bold;
}

#whhlnmjecw .gt_font_italic {
  font-style: italic;
}

#whhlnmjecw .gt_super {
  font-size: 65%;
}

#whhlnmjecw .gt_footnote_marks {
  font-style: italic;
  font-weight: normal;
  font-size: 65%;
}
</style>
<table class="gt_table">
  
  <thead class="gt_col_headings">
    <tr>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1"><strong>Characteristic</strong></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1"><strong>N</strong></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1"><strong>Beta</strong></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1"><strong>95% CI</strong><sup class="gt_footnote_marks">1</sup></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1"><strong>p-value</strong></th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td class="gt_row gt_left">Chemotherapy Treatment</td>
<td class="gt_row gt_center">189</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">Drug A</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">Drug B</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">0.44</td>
<td class="gt_row gt_center">-3.7, 4.6</td>
<td class="gt_row gt_center">0.8</td></tr>
    <tr><td class="gt_row gt_left">Marker Level (ng/mL)</td>
<td class="gt_row gt_center">179</td>
<td class="gt_row gt_center">-0.05</td>
<td class="gt_row gt_center">-2.5, 2.4</td>
<td class="gt_row gt_center">>0.9</td></tr>
    <tr><td class="gt_row gt_left">T Stage</td>
<td class="gt_row gt_center">189</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">T1</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">T2</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">1.3</td>
<td class="gt_row gt_center">-4.2, 6.9</td>
<td class="gt_row gt_center">0.6</td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">T3</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">2.6</td>
<td class="gt_row gt_center">-3.3, 8.6</td>
<td class="gt_row gt_center">0.4</td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">T4</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">-2.0</td>
<td class="gt_row gt_center">-7.8, 3.8</td>
<td class="gt_row gt_center">0.5</td></tr>
    <tr><td class="gt_row gt_left">Grade</td>
<td class="gt_row gt_center">189</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">I</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">II</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">1.4</td>
<td class="gt_row gt_center">-3.6, 6.4</td>
<td class="gt_row gt_center">0.6</td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">III</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">2.0</td>
<td class="gt_row gt_center">-3.1, 7.0</td>
<td class="gt_row gt_center">0.4</td></tr>
    <tr><td class="gt_row gt_left">Tumor Response</td>
<td class="gt_row gt_center">183</td>
<td class="gt_row gt_center">3.8</td>
<td class="gt_row gt_center">-0.66, 8.3</td>
<td class="gt_row gt_center">0.094</td></tr>
    <tr><td class="gt_row gt_left">Patient Died</td>
<td class="gt_row gt_center">189</td>
<td class="gt_row gt_center">2.2</td>
<td class="gt_row gt_center">-2.0, 6.3</td>
<td class="gt_row gt_center">0.3</td></tr>
    <tr><td class="gt_row gt_left">Months to Death/Censor</td>
<td class="gt_row gt_center">189</td>
<td class="gt_row gt_center">-0.14</td>
<td class="gt_row gt_center">-0.54, 0.26</td>
<td class="gt_row gt_center">0.5</td></tr>
  </tbody>
  
  <tfoot>
    <tr class="gt_footnotes">
      <td colspan="5">
        <p class="gt_footnote">
          <sup class="gt_footnote_marks">
            <em>1</em>
          </sup>
           
          CI = Confidence Interval
          <br />
        </p>
      </td>
    </tr>
  </tfoot>
</table>
</div>


x$table_body <- x$table_body %>%
  mutate(estimate = dplyr::case_when(
             estimate < 0 ~ NA_real_, 
                     TRUE ~ estimate))

x
<div id="fxlfvqutdq" style="overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>html {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Helvetica Neue', 'Fira Sans', 'Droid Sans', Arial, sans-serif;
}

#fxlfvqutdq .gt_table {
  display: table;
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#fxlfvqutdq .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#fxlfvqutdq .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#fxlfvqutdq .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 0;
  padding-bottom: 6px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#fxlfvqutdq .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#fxlfvqutdq .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#fxlfvqutdq .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#fxlfvqutdq .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#fxlfvqutdq .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#fxlfvqutdq .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#fxlfvqutdq .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#fxlfvqutdq .gt_group_heading {
  padding: 8px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
}

#fxlfvqutdq .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#fxlfvqutdq .gt_from_md > :first-child {
  margin-top: 0;
}

#fxlfvqutdq .gt_from_md > :last-child {
  margin-bottom: 0;
}

#fxlfvqutdq .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#fxlfvqutdq .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 12px;
}

#fxlfvqutdq .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#fxlfvqutdq .gt_first_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
}

#fxlfvqutdq .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#fxlfvqutdq .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#fxlfvqutdq .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#fxlfvqutdq .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#fxlfvqutdq .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#fxlfvqutdq .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding: 4px;
}

#fxlfvqutdq .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#fxlfvqutdq .gt_sourcenote {
  font-size: 90%;
  padding: 4px;
}

#fxlfvqutdq .gt_left {
  text-align: left;
}

#fxlfvqutdq .gt_center {
  text-align: center;
}

#fxlfvqutdq .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#fxlfvqutdq .gt_font_normal {
  font-weight: normal;
}

#fxlfvqutdq .gt_font_bold {
  font-weight: bold;
}

#fxlfvqutdq .gt_font_italic {
  font-style: italic;
}

#fxlfvqutdq .gt_super {
  font-size: 65%;
}

#fxlfvqutdq .gt_footnote_marks {
  font-style: italic;
  font-weight: normal;
  font-size: 65%;
}
</style>
<table class="gt_table">
  
  <thead class="gt_col_headings">
    <tr>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1"><strong>Characteristic</strong></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1"><strong>N</strong></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1"><strong>Beta</strong></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1"><strong>95% CI</strong><sup class="gt_footnote_marks">1</sup></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1"><strong>p-value</strong></th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td class="gt_row gt_left">Chemotherapy Treatment</td>
<td class="gt_row gt_center">189</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">Drug A</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">Drug B</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">0.44</td>
<td class="gt_row gt_center">-3.7, 4.6</td>
<td class="gt_row gt_center">0.8</td></tr>
    <tr><td class="gt_row gt_left">Marker Level (ng/mL)</td>
<td class="gt_row gt_center">179</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">-2.5, 2.4</td>
<td class="gt_row gt_center">>0.9</td></tr>
    <tr><td class="gt_row gt_left">T Stage</td>
<td class="gt_row gt_center">189</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">T1</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">T2</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">1.3</td>
<td class="gt_row gt_center">-4.2, 6.9</td>
<td class="gt_row gt_center">0.6</td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">T3</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">2.6</td>
<td class="gt_row gt_center">-3.3, 8.6</td>
<td class="gt_row gt_center">0.4</td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">T4</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">-7.8, 3.8</td>
<td class="gt_row gt_center">0.5</td></tr>
    <tr><td class="gt_row gt_left">Grade</td>
<td class="gt_row gt_center">189</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">I</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center">—</td>
<td class="gt_row gt_center"></td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">II</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">1.4</td>
<td class="gt_row gt_center">-3.6, 6.4</td>
<td class="gt_row gt_center">0.6</td></tr>
    <tr><td class="gt_row gt_left" style="text-align: left; text-indent: 10px;">III</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">2.0</td>
<td class="gt_row gt_center">-3.1, 7.0</td>
<td class="gt_row gt_center">0.4</td></tr>
    <tr><td class="gt_row gt_left">Tumor Response</td>
<td class="gt_row gt_center">183</td>
<td class="gt_row gt_center">3.8</td>
<td class="gt_row gt_center">-0.66, 8.3</td>
<td class="gt_row gt_center">0.094</td></tr>
    <tr><td class="gt_row gt_left">Patient Died</td>
<td class="gt_row gt_center">189</td>
<td class="gt_row gt_center">2.2</td>
<td class="gt_row gt_center">-2.0, 6.3</td>
<td class="gt_row gt_center">0.3</td></tr>
    <tr><td class="gt_row gt_left">Months to Death/Censor</td>
<td class="gt_row gt_center">189</td>
<td class="gt_row gt_center"></td>
<td class="gt_row gt_center">-0.54, 0.26</td>
<td class="gt_row gt_center">0.5</td></tr>
  </tbody>
  
  <tfoot>
    <tr class="gt_footnotes">
      <td colspan="5">
        <p class="gt_footnote">
          <sup class="gt_footnote_marks">
            <em>1</em>
          </sup>
           
          CI = Confidence Interval
          <br />
        </p>
      </td>
    </tr>
  </tfoot>
</table>
</div>
