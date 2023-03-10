# Kha's Guide to Hosting a Resume

## Purpose

How and Why should one use these tools to host a resume, with some lessons from Andrew Etter's Book "Modern Technical Writing."

## Prerequisites

* A resume formatted in markdown.
* Visual Studio Code (VSCode)
* A GitHub Account
* Download Jekyll following the instructions [here](https://jekyllrb.com/docs/installation/).
  * Select the your operating system under "Guides".

## How-Tos

### Creating your Markdown Resume (if you haven't already)

Creating a resume is Markdown is crucial to this project. It not only makes it much quicker to edit, it also makes it easier to experiment with different styles as well. Not only that, it is extremely readable in comparison to XML/HTML. Resumes need to stay up to date. Andrew Etter agrees, saying that other formats like Microsoft Docs are mostly for one-time papers, which a resume that needs to stay up to date isn't necessarily so.

A good resource to learn some Markdown is this [Commonmark Markdown Tutorial](https://commonmark.org/help/tutorial/).
A good reference guide is [The Markdown Guide](https://www.markdownguide.org/).

### Setting up your GitHub Repo

As per Andrew Etter's recommendations, we'll be using GitHub Desktop for version control. This is because, unlike using more centralized systems, using a Distributed (non-centralized) version control system allows for offline work, and makes it easier for multiple people to work on the same file. In our case, it's also convenient, as we can package documentation alongside our project.

1. Open Github Desktop
2. Click on: File -> New Repository.
   1. For your repo name, enter "username.github.io", where username is your GitHub username.
   2. Make sure the the privacy setting is set to "public"! The site won't work otherwise.
   2. Everything else is optional, change it as you see fit.
3. Publish the repository on GitHub by pressing the "Publish Repository" button.

### Setting up your Static Site

Static sites are awesome for hosting resumes, as they're they're fast simple, and flexible. No need for  databases, and easy to host just about everywhere. Using a static site generator, in our case, Jekyll, will make it easy for us to host and customize our resume.  

As it's hosted online, it also updates much faster, and you don't have to worry about giving recruiters an old link!

1. If you haven't already, install [Jekyll](https://jekyllrb.com/docs/installation/) onto the machine you're using. This will help with debugging.
2. Open up the "username.github.io" folder on your computer in VSCode.
   * A simple way to do this is to right click on your GitHub Repo in GitHub Desktop, and click on "Open in Visual Studio Code."
3. You'll need to create these directories:
   * _layouts
   * _sass
   * assests\css
4. Copy your markdown resume into the root folder.
5. Rename it to "index.md".
6. At the top of the file, you can add a header that Jekyll can use as variables. `layout` will help us link a stylesheet to the resume, while `title` will be useful to setup the `head` block of html. This header won't be displayed on the website.

    ```yaml
    ---
    title: Kha's Resume
    layout: default
    ---
    ```

7. Create `default.html` inside the `_layouts` directory.
   * In here, you can make an HTML template for your default layout. Here's mine!

    ```html
    <!doctype html>
    <html>
    <head>
        <meta charset="utf-8">

        <!-- {{ page.title }} here references the "title" in the header in our markdown file!-->
        <title>{{ page.title }}</title>

    </head>
    <body>
        <section>
            <!--This gets all of the content (not the header) of the markdown!-->
            {{ content }}
        </section>
        <footer>
            &copy; Kha Pham 2023
        </footer>
    </body>
    </html>
    ```

That provides us with a basic site with default styling! Commit your changes, and push change to GitHub. Then, try accessing username.github.io in your browser. You should see your resume!

#### Adding some Styles

You'll probably want to change some of the styles on your resume. Here's how to do it!

1. Create a file named `styles.scss` to `assets\css`.
   * All we need in there is the following codeblock. It will reference back to the style that we'll add in the `_sass` folder in the next step.

      ```scss
        --- 
        --- 
        @import "main";
      ```

2. Create a file named `main.scss` in  `_sass`. In here, you'll be able to use [sass](https://sass-lang.com/guide) to style up your resume!
    * The [W3Schools CSS Tutorial](https://www.w3schools.com/css/) will also help as a reference.

3. In your `default.html` file in `_layouts`, add the following in your `<head>` block. This will link the stylesheet to your html.

   ```html
        <!--Make sure you have this for styles to work! This will reference the css file
            that Jekyll generates for us.-->
        <link rel="stylesheet" href="assets/css/styles.css">
   ```

### Debugging and Live Edit

To test the changes without needing to push to GitHub all the time, you can run `jekyll serve --livereload` in the terminal. This will let you open `localhost:4000` on your browser, and whenever you make an edit to the code, Jekyll will detect and regenerate the site. All you need to do, then, is press the referesh button on your browser and you should see the changes!

### Resources

Some have already been stated up above, but it's here just in case!

* [W3Schools CSS Tutorial](https://www.w3schools.com/css/).
* [Sass Guide](https://sass-lang.com/guide).
* [Modern Technical Writing: An Introduction to Software Documentation](https://www.amazon.ca/Modern-Technical-Writing-Introduction-Documentation-ebook/dp/B01A2QL9SS) by Andrew Etter.
* [Jekyll's Documentation](https://jekyllrb.com/docs/)
* [Commonmark Markdown Tutorial](https://commonmark.org/help/tutorial/).
* [The Markdown Guide](https://www.markdownguide.org/).


## Authors and Acknowledgements

I'd like to give acknoledge the following - 

* [Jekyll's Documentation](https://jekyllrb.com/docs/), which I modified the template of the layouts and styles from.
* Mahamud Hasan Asif, who helped review my resume and documentation.

## FAQs

> Why isn't my livereload working?

One of the reasons why it didn't work for me was because I was running it in WSL on Windows. Try using Powershell or the Command Line instead!

> Why isn't my resume showing up?

* Make sure that it has been renamed to `index.md`!
* Make sure that it is in the root directory, which should be `username.github.io`.
* Double check your `_layout`, and make sure that the HTML is formatted correctly.
* If it's not appearing on username.github.io, wait a few minutes! Sometimes, it takes Jekyll a little longer to generate the site online.

> Why is Markdown better than using a word processor like Microsoft Word or Google Docs?

Markdown is designed to be simple and lightweight. It's also designed to be readable, and highly compatible with HTML/CSS, as it only shows the general format of the document, rather than forcing styles on the entire thing. Word and Docs have their places as "short, attractive PDFs that can be consumed and discarded", but is much harder to maintain and keep up to date in the long run.