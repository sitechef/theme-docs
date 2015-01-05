# Introduction

This is a guide to creating and editing themes using the SiteChef CLI tool

The SiteChef CLI tool and the base themes supplied with SiteChef have been designed
to be easy-to-modify, simple to setup and, as far as possible use common open standards
and open source tooling.

Our goal is to support developers to help them deliver top quality, responsive
websites for their clients *as quickly as possible*.

If you have any problems with any of the aspects of theme generation, don't hesitate
to get in touch at [dev@sitechef.co.uk](MAILTO:dev@sitechef.co.uk).
This [documentation](https://github.com/sitechef/theme-docs) and the
[SiteChef CLI](https://github.com/sitechef/sitechef-cli) are open source and we
welcome any contributions.


#Quickstart

1. Install [Node.js](nodejs.org/download)
2. Install the SiteChef command line utility `npm install sitechef -g`
3. Clone your theme to a local directory
  `sitechef init [your-api-key] [optional directory name]`
  eg: `sitechef init 999999999888888`
4. Move to your directory (`cd [your-directory]`) and run the local server `sitechef serve`
5. View your theme hosted locally at [http://localhost:3999/](http:/)
6. When you are happy with your changes, publish your theme back to SiteChef with `sitechef publish`
