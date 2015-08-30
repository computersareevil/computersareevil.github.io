# Creating a GitHub Pages Blog

## Assumptions

* You have a [GitHub](https://github.com/) account
* You have access to (and know how to use) a terminal
* You are at least vaguely familiar with [Git](https://git-scm.com/) and
  [Ruby](https://www.ruby-lang.org/) and have access to them

## Steps

Generally speaking, you're going to follow the
[installation steps on GitHub](https://pages.github.com/). I've tweaked things
to suit the needs of this blog, feel free to do the same. Don't be afraid to
experiment. If things go horribly wrong, you can always start over.

> **Note:** Don't write a blog post while setting up your blog—it really slows
  the process ;)

### Prepare a GitHub Repository for Your Blog

1. Create a new organization on Github
  * This will allow you to keep example projects separate from your mainline
    repositories
  * Name your organization with lowercase letters only—it'll save you some
    headaches later
  * From here on I'll simply reference your organization name as
    `<organization>`
2. Create a new repository under your organization called
  `<organization>.github.io`
3. Initial commit:
  * If you created your repository with a `README.md` file then your first
  commit is already done and you can just check out the new repository:
    * Open a terminal to the directory where you want to store your blog and
    clone the repository:
    ```sh
    $ git clone https://github.com/<organization>/<organization>.github.io
    ```
  * I prefer to create a blank repository and initialize it myself:
    ```sh
    $ mkdir <organization>.github.io
    $ cd <organization>.github.io
    $ git init
    $ git remote add origin git@github.com:<organization>/<organization>.github.io.git
    $ echo '<organization>: the blog' >README.md
    $ git add --all
    $ git commit -m 'initial commit'
    $ git push -u origin master
    ```
4. Add an `index.html` file:
  ```sh
  $ echo '<organization>: the blog' >index.html
  $ git add index.html
  $ git commit -m 'add index.html'
  $ git push origin master
  ```
5. Open a browser to `http://<organization>.github.io/` and bask in the glory of
  your new blog!
  * If the page isn't found, you may need to wait up to 10 minutes for your
    new repository to propagate to the web server.

### Prepare Your Development Environment

Every GitHub Page is run through the Ruby-based [Jekyll](http://jekyllrb.com/)
static site generator. Since you'll likely want to preview changes to your blog
before pushing them live, you'll want a copy of Jekyll running locally.

> **Note:** "Local" is a relative term. If you prefer to keep your dev machine
> clean, spin up a new dev box at [Cloud9](https://c9.io/) or
> [Nitrous](https://www.nitrous.io/) and have at it!

The following assumes you have Ruby installed. Depending on your personal setup,
it may or may not already be installed (run `ruby --version` in a terminal to
find out). In either case, if you're developing on your local machine I *highly*
recommend using [RVM](https://rvm.io/) to manage your Ruby instances.

> **Note:** The installation and use of Ruby and RVM are outside the scope of
> this aricle, so I won't be covering that here, but if you use RVM, create a
> `@github-pages` gemset for easy maintenance down the road.

1. Install [Bundler](http://bundler.io/), a package manager for your Ruby gems:
  ```sh
  gem install bundler
  ```
2. Install the `github-pages` gem (via Bundler), which will also install Jekyll
  and other gems used by GitHub Pages:
  * Create a new file in your project directory named `Gemfile` with the
    following contents:
    ```ruby
    source 'https://rubygems.org'
    gem 'github-pages'
    ```
  * Install the required gems (this may take a few minutes...):
    ```sh
    $ bundle install
    ```
    * *Note:* This also creates a new file called `Gemfile.lock`—you will want
      this file to get committed later along with your `Gemfile`
3. Test your blog locally:
    * Run Jekyll to start a local server:
    ```sh
    $ bundle exec jekyll serve
    ```
    * Open a web browser to http://localhost:4000
    * Assuming everything looks good, you can stop Jekyll by pressing *ctrl+c*
      in the terminal
    * *Note:* Running Jekyll creates a `_site` directory to store rendered
      files—you will **not** want to commit this directory
4. Create a `.gitignore` file to ignore the `_site` directory:
  ```sh
  $ echo '/_site/' >>.gitignore
  ```
4. Commit and push your changes:
  ```sh
  $ git add Gemfile Gemfile.lock .gitignore
  $ git commit -m 'add Gemfile with github-pages gem'
  $ git push origin master
  ```
