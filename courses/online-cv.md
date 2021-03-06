---
layout: default
title: Create a free online CV with GitHub Pages
description: Get set up with GitHub and create a free, customized online CV to host your accomplishments and show off your technical skills (1-2 hours).
image: /assets/images/online-cv-image.png
parent: Courses
nav_order: 1
permalink: /courses/3kdf8dlz93l3jf9zla9fjds03jf2a
---

# Create a free online CV with GitHub Pages
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Getting started

![Online CV image](/assets/images/online-cv-image.png)

In this course, you will learn the following:
- How to create a GitHub account, and why it is useful
- How to host free websites with GitHub Pages
- How to make a copy of a CV website template and customize it

See a [live demo](https://jrlegrand.github.io/online-cv/) of the finished product.

We won't get into the basics of GitHub (clone, push, pull, etc), but there are definitely [guides for that](https://guides.github.com/activities/hello-world/).

At the end of the course, you will have a professional, clean, responsive (looks good on mobile devices) online CV like the one above which you can show off and even keep tinkering with if you want.

## Create a GitHub account

A GitHub account is the starting point of learning to code, and is a great way to showcase the work you are doing on any projects.  It is also one of the best ways to collaborate with others on coding projects and keep track of changes to your own code. In this case, the reason we are creating a GitHub account is to use an amazing service called [GitHub Pages](https://pages.github.com/), which allows you to create and host websites for free.

1. Go to [github.com](https://github.com/) and click **Sign up** in the top right corner.
    - Enter a username, email, and password
    - Fill out the survey about what you're interested in
    - Verify your email
    - When it asks what you want to do first, click **Skip this for now**
1. When you're done, your screen should look like this:
![GitHub welcome screen](/assets/images/github-welcome.png)

## Set up GitHub Pages

We are going to start with a free basic website template that is designed for the purpose of creating an online CV, and then we will make customizations in the next few sections. As I mentioned before, [GitHub Pages](https://pages.github.com/) is the service provided by GitHub to host websites for free. It uses another service called [Jekyll](https://jekyllrb.com/) to generate static websites from plain text files. You don't need to know the details of either of these services to complete this project, but thought you might like to know.

The free basic website template we are going to use currently has all of its code hosted in a GitHub [repository](https://docs.github.com/en/github/getting-started-with-github/github-glossary#repository), which is basically just like a file folder stored on GitHub.  The first thing we are going to do with the repository is to [fork](https://docs.github.com/en/github/getting-started-with-github/github-glossary#fork) it, or create a personal copy of the code that you can use to make changes without affecting the original repository.

1. Go to this [GitHub repository](https://github.com/sharu725/online-cv).
1. In the top right, click on the **Fork** button.  It may take a few seconds to complete the process.
![GitHub fork button](/assets/images/fork.png)
1. Now you have a copy of the original repository on your own GitHub profile.  It should look similar to the screenshot below, but instead of `coderx-test`, you should see your username.
![GitHub fork success](/assets/images/fork-success.png)
1. Click the **Settings** button, outlined in red above.
1. In the Settings page, scroll down to the **GitHub Pages** section and change the source from `None` to `master`.  Click **Save**.  This means GitHub will start using your `master` branch as the place to look for the content of your website.  We will get into the details of this soon.
![GitHub Pages source](/assets/images/github-pages-source.png)
1. It will take a minute or two before your website is live.  Immediately, if you scroll down to the GitHub Pages section again, you will see "Your site is ready to be published at...".  When it is ready, you will see "Your site is published at...".
![GitHub Pages success](/assets/images/github-pages-success.png)
1. **Bonus points:** If you prefer your CV to be hosted at `<your-username>.github.io` as opposed to `<your-username>.github.io/online-cv`, you can change your repository name to `<your-username>.github.io`.  So for my example, I would set my repository name to `coderx-test.github.io`.  Or if you wanted this to be called a `resume` instead of an `online-cv`, you can change the repository name to `resume` and then it will be hosted at `<your-username>.github.io/resume`.  For the purposes of this course, I am going to leave mine as `online-cv`.
1. 🎉 Congrats! You have hosted your first GitHub Pages website for free!  Now it's time to customize it and make it your own.

## Personalize your website

### First steps

1. To get back to your main repository page, click the **Code** button near the top left of the screen.
1. Almost all of the work we need to do is in the `_data/data.yml` file, so first click on the `_data` folder, and then click on the `data.yml` file.
    - Make sure you are still in the `master` branch of your repository
![data.yml](/assets/images/data-yml.png)
1. If you look through this file, you should see a lot of the same information about "Alan Doe" that is currently showing up on your website.
1. To edit this file, click the **pencil icon** outlined in red above.
1. Every time you make changes to this file and are ready to see them in action, scroll down to the bottom and click **Commit changes**.
    - It will take GitHub Pages and Jekyll a minute or so to re-build your website
    - After that, you will immediately see your changes by refreshing your website
![Commit changes](/assets/images/commit-changes.png)

### Edit the sidebar

1. The first part of `data.yml` is all about the sidebar.
    - I recommend setting `about` and `education` to `False` because I don't want to see the "how to use?" section and I want education to show in the main section
    - I personally removed both `languages` and `interests` sections because they took up too much space and weren't important to me
    - Change all of the other fields to your personal information
    - We will update your avatar later
1. After you're done updating, scroll down and click **Commit changes** as described above.
1. Wait a minute or so and refresh your website to see the changes!

```yaml
sidebar:
    about: True # set to False or comment line if you want to remove the "how to use?" in the sidebar
    education: True # set to False if you want education in main section instead of in sidebar

    # Profile information
    name: Alan Doe
    tagline: Full Stack Developer
    avatar: profile.png  #place a 100x100 picture inside /assets/images/ folder and provide the name of the file below

    # Sidebar links
    email: hello@webjeda.com
    phone: 012 345 6789
    website: blog.webjeda.com #do not add http://
    linkedin: alandoe
    github: sharu725
    telegram: # add your nickname without '@' sign
    gitlab:
    bitbucket:
    twitter: '@webjeda'
    stack-overflow: # Number/Username, e.g. 123456/alandoe
    codewars:
    goodreads: # Number-Username, e.g. 123456-alandoe

    languages:
      - idiom: English
        level: Native 

      - idiom: French
        level: Professional

      - idiom: Spanish
        level: Professional

    interests:
      - item: Climbing
        link:

      - item: Snowboarding
        link:

      - item: Cooking
        link:
```

### Edit career profile

1. Replace the existing text under the `summary` item with a short description of your career profile.
    - You can use line breaks if you want to make it more readable as shown in the example below
    - If you want to call this section something different (like "Objective" or something), just edit the `title` field
1. If you don't want this section at all, just delete it entirely.
1. Remember to **Commit changes** when you are done.

```yaml
career-profile:
    title: Career Profile
    summary: |
      Summarise your career here lorem ipsum dolor sit amet, consectetuer
      adipiscing elit. You can [download this free resume/CV template here]().
      Aenean commodo ligula eget dolor aenean massa. Cum sociis natoque
      penatibus et magnis dis parturient montes, nascetur ridiculus mus.
      Donec quam felis, ultricies nec, pellentesque eu.
      Second paragraph if required.
```

### Edit education, experience, projects, publications, and skills

We will use the education section as an example that you can apply to the other sections.  This file is written in [YAML](https://yaml.org/) (hence the `.yml` file extension), but you don't need to know anything about that to complete this course.

1. It is important to format everything exactly as the example is formatted (including the number of spaces each line is indented and the specific placement of `-`, `|`, and `>` characters).
1. Replace the listed fields with your own content.
    - In the details section, you can add bullet points by using the dash (`-`) character as shown in the example below
    - If you only want to show bullet points with no additional introduction paragraph, just delete the introduction text under the details section
1. If you want to add an additional education subsection, just copy an existing subsection (including `degree`, `university`, `time`, and `details`) and paste it below an existing subsection within the `education` section.
1. If you want to remove an education subsection entirely, just delete one of the education subsections.
1. Do the same for the other sections - they have different fields, but the same principles apply.
1. Remember to **Commit changes** when you are done.

```yaml
education:
    - degree: MSc in Computer Science
      university: University of London
      time: 2011 - 2012
      details: |
        Describe your study here lorem ipsum dolor sit amet, consectetuer
        adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum
        sociis natoque penatibus et magnis dis parturient montes, nascetur
        ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu,
        pretium quis, sem.
          - Bullet point
          - Bullet point
    - degree: BSc in Applied Mathematics
      university: Bristol University
      time: 2007 - 2011
      details: |
        Describe your study here lorem ipsum dolor sit amet, consectetuer
        adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum
        sociis natoque penatibus et magnis dis parturient montes, nascetur
        ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu,
        pretium quis, sem.
          - Bullet point
          - Bullet point
```
### Edit photo and favicon

1. Find a square photo of yourself at least 100x100 pixels in size.
  - *Hint: You can right-click your LinkedIn photo and "Save image as..."*
1. If you want to change your favicon (the little image that shows up in your tabs), [generate your own](https://favicon.io/) or find one you like somewhere else.
  - *Hint: You can typically find other websites' favicons by adding "/favicon.ico" to the end of their url.  Here's the favicon for [GitHub](https://github.com/favicon.ico)*
1. Go back to your main repository page (click the **Code** link in the top left).
1. If you are changing your favicon: from the main repository page, click **Add file** -> **Upload files** and find the favicon to upload.  Click **Commit changes**.
![Add file button](/assets/images/add-file.png)
1. To change your image, navigate from the main repository page to `/assets/images`.  Repeat the steps above with your image.
  - Take note of your image name
1. If your image name is different from `profile.png`, go back to the `/_data/data.yml` file and change the line below to match the file name of your image:

```yaml
    avatar: profile.png  #place a 100x100 picture inside /assets/images/ folder and provide the name of the file below
```

## Other customizations

### Theme color, title, and description

1. In your main repository page, edit `_config.yml`
1. I would recommend changing `title`, `url`, `baseurl` (if you changed from `online-cv`), `description`, and `theme_skin`.
1. Remember to **Commit changes** when you are done.

```yaml
# Site Settings
title: My Resume
url: 'http://webjeda.com'
baseurl: '/online-cv' #change it according to your repository name
description: A beautiful Jekyll theme for creating resume
# Style will be applied only after restarting the build or serve. Just choose one of the options.
theme_skin: blue # blue turquoise green berry orange ceramic
chrome_mobile_color: #use hex colors (ex:#1976d2) or leave empty if you don't want a color for chrome mobile searchbar
```

### Experience vs experiences

1. It bugged me that the heading for job experience was plural.  Because we have total control over how things work in our CV, we can change it (if it bothers you)!
1. From your main repository page, navigate to `/includes/experiences.html` and edit this file.
1. Towards the end of the first block of code (pasted below), change "Experiences" to "Experience" or whatever you want to call it.
1. Remember to **Commit changes** when you are done.

```yaml
<section class="section experiences-section">
  <h2 class="section-title">
    <span class="fa-stack fa-xs">
      <i class="fas fa-circle fa-stack-2x"></i>
      <i class="fas fa-briefcase fa-stack-1x fa-inverse"></i>
    </span>
    Experiences
  </h2>
```

### Fix header height on mobile

1. I noticed the header of the sidebar was too tall on mobile devices.  If you notice this, follow the steps below.
1. From your main repository page, navigate to `/_sass/_base.scss` and edit this file.
1. Around line 39, you should see a `.sidebar-wrapper` section.  To fix the issue, delete the line in this section that says `min-height: 800px;`
1. Remember to **Commit changes** when you are done.

```yaml
.sidebar-wrapper {
    background: $theme-color;
    position: absolute;
    right: 0;
    width: 280px;
    height: 100%;
    min-height: 800px;
    color: #fff;
```

## Conclusion

Congrats!!!  You've made it through your first CodeRx course and have a GitHub profile and a free online CV to show for it.  Please follow us on [LinkedIn](https://www.linkedin.com/company/coderx), [Twitter](https://twitter.com/coderx_io), [Instagram](https://www.instagram.com/coderx_io/), and [GitHub](https://github.com/coderxio).  Also please [share the signup link](https://mailchi.mp/ac1988c7d7f4/trujlqmy5g) to this course with anyone you think might find this useful!  Thank you for taking the time to work on this, and enjoy your new online CV!
