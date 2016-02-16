I use [Harp](http://harpjs.com) to build this site. To write a new post, I'd go to `/blog` and create a new markdown file, and add the file metadata to `_data.json`. When I'm done, I'd then run `harp compile --output ../_site` which compiles all assets to HTML, CSS, JavaScript and so on to `_site` folder.

In the `_site` folder I create a CNAME and then run `surge` to upload the new changes to [surge.sh](https://surge.sh). More than once I've forgotten to add the CNAME and quite frankly I wish it was easier to go from markdown file to publish but it is what it is. There's room for Grunt or Gulp to help with this process however I'm a fan of using less tools, so what can we do? NPM scripts!

I wrote a thing to compile the site and copy the CNAME file to `_site`. So now all I do is `npm  run compile` and then run `surge`. No errors, less steps, happy.
