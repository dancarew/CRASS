# CRASS

**CRASS** is a simple [responsive CSS](http://www.alistapart.com/articles/responsive-web-design/) grid library for mobile devices, tablets, and monitors.

## Features

- Mobile:   1 column
- Tablet:   6 columns
- Monitor: 12 columns

The grid is 93.75% wide (at 1024px), which is 960px/1024px. :)

For tablet, six even columns, each at ~16.666% wide. For monitors, 12 even columns, each at ~8.333% wide. On monitors, that's 80px each. "Gutters" are created using padding (24px/1.5em on each side) on the *inside* of the column, leaving 32px of content inside. When the gutters are paired up (on the inside columns), that's 48px of gutters. Mobile gets one column.

I like *wide* gutters because vertical rules look very elegant inside. Yes, I know the gutters are wider than the columns.

Visually (for "pixel thinkers"):

Outer | Column | Gutter...

24px | 32px | 48px | 32px | 48px | 32px | 48px | 32px | 48px | 32px | 48px | 32px | 48px | 32px | 48px | 32px | 48px | 32px | 24px

The reality:

8.333% | 8.333% | 8.333% | ...

Huge thanks to Joni Korpi for faking gutters on the inside with non-responsive ems. Brilliant thinking. His grid is the [Golden Grid System](http://goldengridsystem.com/).

## Basics

- `page` is the basic box
- `section` divides big areas of the page
- `monitor-row` is one row of content for screens >= 1024px
- `tablet-row` is one row of content for screens >= 768px <= 1024px
- `monitor-col_n` is the columnar division of a `monitor_row`; 12 columns max
- `tablet-col_n` is the columnar division of a `tablet-row`; 6 columns max

Other classes:

- `push_n` pushes your columns if you want white space on the left
  
  (`pull_n` is unnecessary because the column is limited in width and `*-col_n` classes are wrapped in `*-row` s)
  
- `left_n` places your column so many columns from the left to the right
- `right_n` places your column so many columns from the right to the left

`left_n` and `right_n` (CSS `position`, instead of `margin-left`) break the "normal flow" of the document, allowing you to rearrange the source order of HTML, while still staying true to the original design.

Some designers have [expressed concern](http://trentwalton.com/2011/07/14/content-choreography/) on how to reconcile document flow with design, but [960.gs](http://960.gs/) has some solutions:

> By utilizing the (`left`) and (`right`) classes, elements can be rearranged, independent of the order in which they appear in the markup. This allows you to keep more pertinent info higher in the HTML, without sacrificing precision in your page layout. For instance, view the source code of this page to see how the `H1` tag has been re-positioned.

When you want to break items out of the `monitor-row`/`tablet-row` grid, it's time to go custom, my friends.

## Example

    page
        section
            monitor-row
                tablet-row
                    monitor-col_2 tablet-col_6
                tablet-row
                    monitor-col_10 tablet-col_6
            monitor-row
                tablet-row
                    monitor-col_6 tablet-col_1
                    monitor-col_6 tablet-col_5

This example says I want:

- One `page`
- With one `section`
- With two rows for monitors
- (Scan ahead...) In that first `monitor-row`, I want a 2-column wide division and a 10-column wide division
- In the next `monitor-row`, I want two 6-column wide divisions, so it's all nice and even
- (Backtracking...) For tablets, I want three rows
- In the first tablet row, I want a 6-column wide division
- In the second tablet row, I want a 6-column wide division
- In the third tablet row, I want one 1-column wide division and one 5-column wide division

## Borders (or as graphic designers call them "Rules" in between sipping mochas in their black turtlenecks)

Comes with some classes for adding bottom/left/right borders. These aren't bulletproof. CSS sucks ass in extending boxes to the same height of its siblings, which means the vertical borders could only extend on the shortest column. JavaScript might have fixed this in the past on non-responsive designs, but not today. I don't know what to tell you. Apply it when you can kind of guess about the content's height.

## Your grid sucks

That's cool. Don't use it.

Or better, use it when it helps you and then break out when you need to. Here's a weakness where you might want go your own way:

From a 12-column grid for monitors (divisible by 1, 2, 3, 4, 6, 12), the grid collapses to a 6-column grid for tablets (divisible by 1, 2, 3, 6). That means on tablets you can't have 25%:75% ratio columns anymore. Lay on a thin layer of custom overwrite with the usual grid classes:

HTML:

    page
        section
            monitor-row
                tablet-row
                    monitor-col_2 tablet-col_6 tablet-sidebar
                tablet-row
                    monitor-col_10 tablet-col_6 tablet-main

CSS:

    @media only screen and (min-width: 48em) and (max-width: 63.999em) {
        /* Ha, screw you, tablet-col_6! */
        /* ...but still give me your padding goodness */
        tablet-sidebar { width: 25%; }
        tablet-main { width: 75%; }
    }

## Feedback

Fork it. Download it. Demo it. Study it. Rip it apart. Put it back together again. Let me know if this is cool or stupid.

[rich@richardcornish.com](mailto:rich@richardcornish.com)