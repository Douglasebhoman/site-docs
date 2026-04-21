
## styles.css

style.css is used to separate presentation from content. Instead of putting design rules inside every HTML page, all styling is centralized in one file.

> **Note:**

> style.css --> Is linked from every page in the site — homepage, blog index, and all post pages.

Main responsibilities include: Branded colour themes and responsive behaviors. This separation of concerns improves maintainability.

## CNAME

It is used to connect the custom domain, "douglasebhoman.com" to the hosting provider. This tells GitHub which custom domain to use, while the DNS CNAME record tells the internet where that domain should point.

This improves branding, simplifies domain management, and allows documentation platforms to remain flexible if hosting infrastructure changes. 

## Blog post structure

Each blog post is stored in its own folder with an index.html file to enable clean URLs, support organization, and simplify hosting across web servers. 

### Future plan

The present structure is temporary; the long-term strategy is to migrate content to a static site generator (Eleventy). This would provide a more structured architecture, simple maintenance, improved content organization, and make future updates more efficient.

## assets/images

Images are kept in a flat structure because the site currently has no image processing pipeline. All images are referenced directly by filename, so subdirectories would require path updates across multiple HTML files with no tooling to manage them.