
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Coding Workshop: Tables in RMarkdown 2021-11-18

-   {gt}
    -   Pro: Looks really good by default (best looking html in my
        opinion!)
    -   Pro: Footnotes fully featured
    -   Pro: Can use tidyselect to select data rows/cols. Generally
        adheres to tidyverses style guide
    -   Pro: Easy quick saving of tables `gt::gtsave()`
    -   Pro: Great documentation
    -   Con: Word not yet supported, PDF/RTF under development BUT
        gtsummary objects will automatically default to other print
        engines so you can knit to other outputs. Non-gtsummary objects
        will just not print in final document.
    -   Con: Can’t have more than 2 spanning headers - although gt will
        support this soon.
-   {Huxtable}
    -   Pro: Works well with html, pdf, rtf and word outputs
    -   Pro: Can quick save tables as well
    -   Con: I find the documentation confusing
    -   Con: Default settings are not as nice looking as flextable and
        gt (although once you add compact theme they look better)
    -   Con: For gtsummary tables, you may lose the footnote numbering.
        Footnote still appears but without numbers
    -   Con: Hux table doesn’t let you see it in the viewer like gt.
        Prints as markdown, making it harder to preview
    -   Con: Footnotes have limited support
    -   Con: While gtsummary does a lot of the leg work customizing
        tables for gtsummary objects, non-gtsummary tables can be
        cumbesome to try to customize
-   {flextable}
    -   Pro: Footnotes fully featured
    -   Pro: Works well with html and pdf. Best word output in my
        opinion
    -   Pro: Great documentation
    -   Con: Can’t use tidyselect to index rows/cols
    -   Con: A little cumbersome to quick save tables. it uses webshot
        to take a screen shot
-   {kable} + {kableExtra}
    -   Formatting options more limited, but this can be useful for
        dashboards (it sizes tables better than gt and offers some
        limited reactivate like scroll over)

Summary:

-   gt is best for HTML, and is currently under construction for PDF and
    RTF (aka Word). gt is already pretty great for PDF and RTF, but not
    all formatting is available for the outputs. I think they are nearly
    ready to release it, however.

-   flextable is great for Word and PowerPoint. While PDF is technically
    supported, flextable just makes an image and slaps it into a PDF
    document.

-   huxtable is great for the LaTeX output (which includes PDF of
    course). I have used this to make reports all in Latex because you
    can save an individual table’s latex code out as a text file, and
    simple import it into the latex document