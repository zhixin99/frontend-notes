# HTML

## Core tags
| Tag Name        | Meaning / Use                                                 | Attributes       | 
| --------------- | ------------------------------------------------------------- | ---------------- | 
| `<p>`           | Paragraph of text.                                            |
| `<div>`         | Division or container for grouping elements (block-level).    |
| `<a>`           | Hyperlink (anchor).                                           | href <br> target="_blank"

## Headings
- Only use one `h1` per page. No more, no less.  
- Heading numbers should be consecutive. No skip.   
- Headings always introduce new content sections. A heading for some content should never be a `<p>` or a `<div>`.   

| Tag Name        | Meaning / Use                                                 | Attributes       | 
| --------------- | ------------------------------------------------------------- | ---------------- | 
| `<h1>` – `<h6>` | Headings — `<h1>` is the largest, `<h6>` the smallest.        |

## Landmark regions
| Tag Name        | Meaning / Use                                                 | Attributes       | 
| --------------- | ------------------------------------------------------------- | ---------------- | 
| `<nav>`         | Navigation section (menu links).                              |
| `<header>`      | Header section of a page or article.                          |
| `<main>`        | The main content area.                                        |
| `<article>`     | a self-contained composition which is independently distributable or reusable, like blogs, news                                     |
| `<section>`     | Logical section or topic block.                               |
| `<footer>`      | Footer section.                                               |

## Embedded content
| Tag Name        | Meaning / Use                                                 | Attributes       | 
| --------------- | ------------------------------------------------------------- | ---------------- | 
| `<img>`         |                                                        | src
| `<audio>`         |                                                         | controls
| `<video>`         |                                                        | controls muted loop autoplay

```html
<!-- tells the browser to use default video controls -->
<audio controls>
    <!-- in case the browser can't open the video, they can download the video -->
    <a href="media/audio/scrimbaPodTom.mp3">download audio</a>
    <source src="media/audio/scrimbaPodTom.mp3" type="audio/map3">
    <source src="media/audio/scrimbaPodTom.wav" type="audio/wav">
</audio>
```


## Table
| Tag Name        | Meaning / Use                                                 | Attributes       | 
| --------------- | ------------------------------------------------------------- | ---------------- | 
| `<table>`          |   
| `<caption>`          |  Table heading  
| `<tr>`          |  Defines a row of cells|
| `<td>`          |  A cell of table that contains data | colspan rowspan
| `<th>`          |  Table heading | scope="col" scope="row"
| `<thead>`          |  Table head
| `<tbody>`          |  Table body
| `<tfoot>`          |  Table footer
```html
<table>
    <thead>
        <caption>My Concerts 🎸</caption>
        <tr>
            <th>Artist scope="col"</th>
            <th>Location scope="col"</th>
            <th>Cost scope="col"</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Blur</td>
            <td>Exeter</td>
            <td>£50</td>
        </tr>
        <tr>
            <td>Billie Eilish</td>
            <td>London</td>
            <td>£90</td>
        </tr>
        <tr>
            <td>Adele</td>
            <td>Bristol</td>
            <td>£65</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="2">Sum</td>
            <td>£205</td>
        </tr>
    </tfoot>
</table>
```

## Connected consecutive items
| Tag Name        | Meaning / Use                                                 | Attributes       | 
| --------------- | ------------------------------------------------------------- | ---------------- | 
| `<ul>`          | Unordered list (with bullet points).                          |
| `<ol>`          | Ordered list (with numbers).                                  |
| `<li>`          | List item (inside `<ul>` or `<ol>`).                          |



| Tag Name        | Meaning / Use                                                 | Attributes       | Usage       | 
| --------------- | ------------------------------------------------------------- | ---------------- | ----------- | 
| `<dl>`          | Description list.                                             |                  | metadata 
| `<dt>`          | Description term (inside `<dl>`).                             |                  |
| `<dd>`          | Description details (inside `<dl>`).                          |                  |


| Tag Name        | Meaning / Use                                                 | Attributes       | Usage       | 
| --------------- | ------------------------------------------------------------- | ---------------- | ----------- | 
| `<br>`          | Line break.                                                   |
| `<hr>`          | Horizontal line (divider).                                    |


## Formatting Elements

| Tag Name        | Meaning / Use                                                 | Attributes       | Usage       | 
| --------------- | ------------------------------------------------------------- | ---------------- | ----------- | 
| `<mark>`        | Highlight in yellow.                                          |                  | 
| `<strong>`          |      Used for importance, seriousness or urgency, like a warning. Bolds the text to make them visually clear                      |                  |
| `<b>`          |                           |                  |
| `<i>`          |                           |                  |
| `<em>`          |  Add semantic meaning which can be understand by screen reader. It should be emphasized / stressed when spoken                         |                  |
| `<del>`          | Deleted text.                          |                  |
| `<ins>`          | Inserted text.                        |                  |
| `<sub>`          |                        |                  |
| `<sup>`          |                         |                  |
