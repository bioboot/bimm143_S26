# Introduction to Bioinformatics  

Website repo for UC San Diego's BIMM143 undergraduate bioinformatics lab course for biology majors.  

For an example of the deployed website visit:  

- http://thegrantlab.org/bimm143/  
- http://bioboot.github.io/bimm143_W26/  


**Overview:** This is a [jekell based static site](http://jekyllrb.com/docs/home/) typically served from GitHub Pages. To view locally on your own machine (i.e. build locally before pushing or submitting a pull 
request to this [bioboot GitHub](https://github.com/bioboot/bimm143_S25) repo or your own repo) you will need to have the **jekyll** and **github-pages** gem setup on your machine (see further 
below for full instructions)


> Side Note: If you are setting up a new course website and don't want all the bloat from my existing BIMM143 course then check out the streamlined https://github.com/bioboot/course_theme repo to get you started with a nice course Jekyll website theme like mine.


## Install ruby, jekyll and github-pages 
Instructions for ruby setup via `homebrew` are [here](https://jekyllrb.com/docs/installation/macos/).

Once installed consider updating RubyGems first (may need sudo for these).

	sudo gem update --system

Then install the Jekyll Gem and the GitHub Gem

	gem install jekyll
	gem install github-pages

Optional: Pygments python based syntax highlighter

	pip install Pygments


## Basics of Jekyll websites
Jekyll websites are configured based on the contents of the various underscore prefixed files and folders. You can find out more about these here: http://jekyllrb.com/docs/structure/

However, most likely you will want to leave most of these alone and just add your content changes to the `index.md`, `schedule.md` and `_data/authors.yml` files. You will also want to add or create new files in the **class-material/** 
directory (i.e. add lecture slides, handouts, cheat-sheets etc.)

Please remember that all content is on the **gh-pages** branch! 
So you will want to be working on this branch and push back to this branch.

A typical workflow for folks that have been added as **"Collaborators"** would look something like this:

	## One time only clone
	git clone https://github.com/bioboot/bimm143_S25.git
	cd bimm143_W25

	## Edit your files (e.g. schedule.md, _data/authors.yml, _config.yml)
	vi schedule.md

	## Check changes localy
	#jekyll serve
	bundle exec jekyll serve

	## Pull recent changes
	git pull origin gh-pages

	## Stage, commit and push your changes
	git status
	git add schedule.md
	git commit -m "Your msg about changes"
	git push origin gh-pages



### Roll forward instructions...

To roll forward for a new years class follow the steps below (assuming you already have **jekyll** and **github-pages** 
setup on your local machine):

Git clone old site to a new dir

  	cd ~/Dropbox/Teaching
  	mkdir bimm143_F25
  	cd bimm143_F25
  	git clone git@github.com:bioboot/bimm143_S25.git bimm143_F25
  	cd bimm143_F25/
  
Update `_config.yml`, `_data/authors.yml` and `index.md`. IN particular, rembember to change the dates and the pre-course questionnaire and post-course evaluation forms. Go through the regular `git add`, `git commit -m` cycle. But don’t yet push to GitHub (as we will want a new repo for this years class).
  

On GitHub make a new repo (Use the “+” sign and name it `bimm143_F25` to match your local directory name. This name matching is purely for convenience).

Then on the local machine change your remotes to point to this new repo.

  	git remotes -v   
  	git remote rm origin  

Now add our new repo and push changes:  

  	git remote add origin git@github.com:bioboot/bimm143_F25.git  
  	git push -u origin gh-pages  

Then preview your new site online: For example https://bioboot.github.io/bimm143_W26/ and visit the repo itself to see if everything is ship-shape: https://github.com/bioboot/bimm143_W26  
