# V0 of the surf website

This is a fork of the minimal mistakes themes working with jekyll and github pages.

Full documentation of the theme: https://mmistakes.github.io/minimal-mistakes/

Run the local server with the following command in the root folder
```bash
$ bundle exec jekyll serve --incremental
```

# Update linux mint (Jan 14, 2025)
Now runs in an apptainer container. First, you need to exclude ruby paths from you site config `_config.yaml`:
```yml
exclude:
   - Gemfile
   - Gemfile.lock
   - node_modules
   - vendor/bundle/ # the vendor lines are suggested by the documentation but not useful here.
   - vendor/cache/
   - vendor/gems/
   - vendor/ruby/
   - ruby
   - jekyll_sandbox
```


```bash
$ # download a working jekyll image
$ apptainer build jekyll_serve.sif docker://bretfisher/jekyll-serve
# create a sandbox for running the image
$ apptainer build --sandbox jekyll_sandbox jekyll_serve.sif
# You can run the image in interractive mod
$ apptainer shell jekyll_sandbox
# In there, you will likely want to run bundle install 
Apptainer> bundle install
# Then you can simply serve your site
$ apptainer exec jekyll_sandbox   bundle exec jekyll serve --incremental --host 0.0.0.0 --port 4000
```

Make sure you only have one server running on a given port 😉