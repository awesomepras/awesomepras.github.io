# awesomepras.github.io
Creating github.io site instead of using wordpress.  
Posts or thoughts before the dementia kicks in.

## Site: 
[https://awesomepras.github.io](https://awesomepras.github.io)

### how to jekyll
1. Install jekyll
    ```
    sudo apt install ruby-full build-essential
    sudo gem install jekyll
    jekyll --version
    echo '
    # Ruby exports
    export GEM_HOME=$HOME/gems
    export PATH=$HOME/gems/bin:$PATH
    ' >> ~/.bashrc  
    
    source ~/.bashrc  
    gem install jekyll bundler
    jekyll -v
    
    ```
2. Jekyll CLI Commands

    ```jekyll build```: Generates the static site in the _site directory.  
    ```jekyll serve```: Builds the site and starts a web server on your local and preview site in http://localhost:4000 
    ```jekyll new [site name]```: Creates a new Jekyll site in a new directory with the specified site name. 
    ```jekyll doctor```: Outputs any configuration or dependency issues that may be present.  
    ```jekyll clean```: Deletes the _site directory, which is where the generated site files are stored.  
    ```jekyll help```: Outputs the help documentation for Jekyll.  
    ```jekyll serve --draft```: Generates and serves your Jekyll site, including any posts that are in the _drafts directory.  

3. Update Jekyll configuration file 
The Jekyll configuration file is a YAML file named _config.yml 

4. Build a new site 
```jekyll new [site name]```

    > _config.yml: The Jekyll configuration file containing your site’s settings and options.  
    > _posts: A directory that contains your site’s content (can be blog posts). These can be Markdown or HTML files with a specific file naming convention: YEAR-MONTH-DAY-title.MARKUP. 
    > Gemfile and Gemfile.lock: Bundler uses these files to manage the Ruby gems on which your site relies.  
    > index.md: The default homepage for your site, generated from a Markdown or HTML file.  
    > But there are more files/folders that can be used to customize your Jekyll website.   
    > These folders include:
    > _includes: A directory that contains reusable HTML snippets that can be included in your layouts and pages. Such as navbar, footer, e.t.c.  
    > _layouts: A directory that contains HTML layout templates that define the structure of your pages.  
    > assets: A directory that contains any files that are used by your site, such as images and CSS files.  
    > _sass: A directory that contains Sass files that can be used to generate CSS for your site.  


#### Ref:
https://kinsta.com/blog/jekyll-static-site/#how-do-you-create-a-static-website-on-jekyll  
https://jekyllrb.com/docs/themes/#overriding-theme-defaults  

