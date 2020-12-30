---
layout: post
title: Publishing Corvid to GitHub Pages
---

My sister just went out on her own as a therapist in Eugene, Oregon and so I had to get a website set up for her - [JenBeckLMFT.com](http://www.JenBeckLMFT.com). I was pleased to find out about [Corvid](https://github.com/di/corvid), a static-site generator written in Python that was really stripped down and perfect for being able to turn a few markdown files into a basic 'brochure' website. Getting it to publish to GitHub Pages smoothly was a bit of a hurdle so hopefully this documentation will help someone else with getting a site set up with a bit more ease.

Corvid publishes its HTML files to an `output` folder by default and allows you to specify a folder at build time by running `corvid -o <foldername>` (replace `<foldername>` with the actual folder name you want to use). Incidentally, GitHub Pages will only deploy from a folder named `docs` so that's what it would've had to have been (alternatively, it'll also work with files in the default directory or in the base of a `gh-pages` branch). I was being super lazy and didn't want to have to look up/ remember that command option each time I infrequently published so I thought it might be a time to learn GitHub Actions to automate renaming the default `output` folder to `docs`.

It took a while to find a good resource but [peaceiris](https://twitter.com/piris314) has an excellent write-up on writing GitHub Actions in many languages for deploying static site generated websites at [dev.to](https://dev.to/peaceiris/deploy-to-github-pages-with-github-actions-for-static-site-generator-1mo6). So no longer was I simply renaming a folder but their action automates the deployment process entirely! I no longer have to build the files locally, change the name of the deployed folder and then push that to GitHub. Now I just make whatever changes are needed to the source files locally and push my `main` branch to GitHub. The whole process starts with the following GitHub Action/ YAML code and deploying it is done by saving it to a `.yml` file in your default Git branch two folders deep in a folder structure like `.github/workflows/NameOfYourChoice.yml` (the first folder is really `.github` and I think you can name the final filename whatever you'd like - mine is `publishingCorvid.yml`)

```
name: github pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2

      - name: Setup Python
        uses: actions/setup-python@v1
        with:
          python-version: "3.9"
          architecture: "x64"

      - name: Cache dependencies
        uses: actions/cache@v1
        with:
          path: ~/.cache/pip
          key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
          restore-keys: |
            ${{ runner.os }}-pip-

      - name: Install dependencies
        run: |
          python3 -m pip install --upgrade pip
          python3 -m pip install -r ./requirements.txt
          corvid

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./output
```

From there, the GitHub action kicks in whenever I `push` my local changes to GitHub, I think spinning up a Docker container to deal with the deploy (note I did change my default branch to `main` so make sure the 6th line matches your default branch name). Then you need to make sure you have a requirements.txt file in your project's folder (from the command line run `pip freeze > requirements.txt` to create it automatically). After the default python commands to upgrade pip and install all the required packages from `requirements.txt` you need to run the actual command for building your static site generator. In this case it is `corvid`. The last part is the magic of peaceiris's separate gh-pages GitHub Action because it takes whatever is in the folder in the last line (`publish_dir`) and pushes it to a separate gh-pages branch within your Git(/Hub) repository (you don't have to set up the `gh-pages` branch in advance). Incidentally, I also updated the python version to 3.9 expecting it to break but it worked fine and I'm thinking is more future proof.

Remember earlier that I said GitHub Pages will only work with files located in your branch's home directory or a docs folder or in the base of a gh-pages branch. Well that last option is now set for us. We just have to go into our repository's page and specify the gh-pages branch as the source. Go to your project's repository on GitHub and click on `Settings`.

GitHub Repository Settings Tab:

![](/images/GitHub-Repository-Settings.png)

Scroll most of the way down the page and under `GitHub Pages` and then `Source` you want to select `Branch: gh-pages` (You can leave `/ (root)` selected).

GitHub Pages Branch (gh-pages) Setting:

![](/images/GitHub-Pages-Branch.png)

If you do select a custom domain here, GitHub will quietly add a textfile named `CNAME` to your gh-pages branch with the domain name that you entered on the first line of the file. Unfortunately, **Corvid will wipe that file out on your next deploy and disable your custom domain so you want to copy that CNAME file to your local input folder** so that it's deployed along with every future deploy. Good luck and if you have any difficulty feel free to reach out.
