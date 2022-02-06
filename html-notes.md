# HTML Notes
## Intro
- HTML is composed of elements.  These elements almost always have the element tags and content
  ```
  <elementName> Content! </elementName>
  ```
- One of the main HTML elements used in webpage design is the `body`.  The body is used to house the main content of the page
- Whenever an element is contained inside of another element, it is known as the child of that parent element.
- Multiple children contained by a parent are known as siblings to each other

### Headings
- Headings in HTML are used to describe content like titles and new sections of the text
- In total there are 6 headings of decreasing size starting from `h1` down to `h6`

### Divs
- Divs are divisions/containers that split the page into sections.  These sections are used for grouping elements of HTML together
- They don't have a visual representation but are useful for applying custom styles to the elements

### Attributes
- Attributes are content added to the opening tag of an element to provide information and change styling
- Attributes have the name of the attribute and the value of an attribute
- One of the more commonly used attributes is the `id` attribute.  It is used to specify different elements from one another
  ```
  <div id="example">
    content
  </div>
  ```

### Displaying Text
- The two main elements used for displaying text are `paragraph` and `span` tags denoted with `p` and `span` respectively
- It is best to use a `span` element when you are targeting a specific piece of content that is inline with other content or on the same line as other text.  If you are dividing content into blocks it is best to use a `div`

### Styling Text
- It is possible to style text using raw HTML tags.  You can emphasize text using `em` tags and highlight important text using `strong` tags
- `em` tags will generally render in italics
- `strong` tags will generally render in bold

### Line Breaks
- Spacing in HTML code will **NOT** affect the spacing of the rendered screen in browser.  If you need to change the spacing of certain things, you will need to use a `br` line break
- `br` tags are only composed of the starting tag with no end tag

### Unordered Lists
- You can use the `ul` tag to create a list of items that appear in no particular order
- `ul` will list items with a bullet point (which you can remove with CSS)
- Each item within a `ul` is a list item `li`
  ```
  <ul>
    <li>One</li>
    <li>Two</li>
    <li>Three</li>
  </ul>
  ```

### Ordered Lists
- You can use the `ol` tag to create a list of items that appear in order
- The lists created with the `ol` tag will render with numbers rather than bullet points
- You still use the `li` element for list items

### Images
- You can add non text content like images by using the `img` element
- The `img` tag is different from other elements in that it is a *self-closing* tag
  ```
  <img src="somelocation" />
  ```
- The `img` tag has a **REQUIRED** attribute known as `src` which is the source of the image in the form of a URL 
- To make images more accessible to users and more inclusive, you can use the `alt` attribute which is used to provide an alternate description of the image
- The `alt` is also used to provide a description of the image if it fails to load, have the browser read the description of the image to the visually impaired, and help with SEO 

### Videos
- You can use the `video` tag to imbed a video into the content of your site
- The `video` tag has an opening and closing tag
- Like the `img` tag, the `video` tag **REQUIRES** a `src` attribute
- The `video` tag also has `width` and `height` attributes to change the size of what is displayed in browser
- There is also a `controls` attribute which allows the user to perform actions like pause, play, mute, etc.
- Between the opening and closing tags you can put content that should be shown if the video isn't supported or can't load

## HTML Standards
- HTML documents always start with `<!DOCTYPE html>` which declares that the document is HTML
- To create html content you must make an `html` element after the doctype declaration.  This is where we will put all of out content

### The Head
- The head of an html document contains the `metadata` of the webpage.  It is information about the page that won't be directly displayed on the page.  The head also has opening and closing tags
- Using the `title` element in the head, you can change and display the name of the current page in the tab of the browser

### Linking to Other Pages
- Linking between pages is how you can allow for users to move throughout your website or move to a different website entirely
- You add links to web pages by adding an anchor `a` tag.  The link is included as a `href` attribute
- Set the content of the anchor to be what you want to be displayed on the screen for the link
- If you want the link to open in a new window or tab you can add the `target` attribute with the `"_blank"` value.  Older browsers will open a window while newer browsers will open a new tab
  ```
  <a href="example.com" target="_blank">Click Me!</a>
  ```

### Linking to a Relative Page
- If you would like to link to a page within your own site you can set the `href` of the anchor tag to the filepath of the desired page

### Creating Non-Text Links
- You can create non-text links in HTML by having the anchor tag as the parent of a child element.  By wrapping the child in the `a` tag it will become the link

### Linking to the Same Page
- In order to link to elements on the same page you must give your elements `id` attributes
- Once you have set `id` attributes on the elements, you can use an anchor tag and reference the desired `id` in the `href` by using a `#`
  ```
  <a href="#idName">Click Me!</a>
  ```

### Whitespace and Indentation
- As mentioned previously, whitespace is ignored while rendering an html document
- To improve readabilitiy, do not be afraid to use whitespace and indentation
- Using indentation at each level will help make reading at a glance much easier
  ```
  <body>
    <p>Paragraph 1</p>
    <div>
      <p>Paragraph 2</p>
    </div>
  </body>
  ```

### Comments
- You can leave comments in html documents using `<!--` to start the comment and `-->` to end the comment
  ```
  <!-- This is a comment -->
  ```

## Tables
- Tables are useful for organizing and displaying content on the screen
- You create the table by using the `table` element
- You add row elements to the table by using the `tr` elements
- To actually add data to the rows of tables, you must use the `td` (table data) element
  ```
  <table>
    <tr>
      <td>73</td>
      <td>81</td>
    </tr>
  </table>
  ```
- To add headings to the rows and columns of tables, you  use the `th` element
  - `th` elements have an attribute known as `scope`.  The scope is used to define if the heading is a `row` or `col` heading
- To give your tables a border to make it easier to read, you must use CSS
  ```
  table, td {
    border: 1px solid black;
  }
  ```
- You can span across multiple columns in a table by using the `colspan` attribute of a `td`.  You set this attribute to an integer wrapped in quotations specifying how many columns you want it to display across
- Similar to `colspan` you can have a `td` span across multiple rows by using the `rowspan` attribute
- Sometimes tables will be so long that you will want to section them off.  You can use the `tbody` element to section the table off to make it more easily readable.  You should enclose the data in the `element` but leave the `column headings` outside of the body
- The `column headings` should be placed within the `thead` element of a table.  This will apply the column headings to each `tbody` element
- You can add a footer to a table using the `tfoot` element