Automated Deployment From GitHub on Gandi Simple Hosting
========================================================

This tutorial will be useful if you:

* have a website with static content
* want to host the source code for your website on GitHub or BitBucket
* want the site to be hosted on a Gandi Simple Hosting instance, and 
* you want your site to be updated automatically any time changed are pushed to the repo.

## Requirements

* A Gandi Simple Hosting (PHP/MySQL) (or create one below)
* A GitHub or BitBucket account
* A public git repo with static web content

We're using the [Gandi CLI](http://cli.gandi.net) for this tutorial, but you can also perform these steps within your Gandi account.

### Create a PHP/MySQL Simple Hosting Instance

    $ gandi paas create --name squirrels --type phpmysql --vhosts squirrels.gandi.xyz

### Connect to the instance via SSH

The following command will activate the console and automatically open a connection to it.

    $ gandi paas console squirrels

### Clone the repo to the instance

Clone the repo into the `htdocs/` directory:

    $ cd /srv/data/web/vhosts/www.squirrel.li/htdocs
    $ rm index.html                                               # Because the directory has to be empty first
    $ git clone https://github.com/soulshake/squirrels.git .      # Note the dot at the end

Create a PHP file (we'll call ours `pull.php`) with the following contents:

```
<?php
`git pull`;                         // This will execute the `git pull` command on your instance
header("Cache-Control: max-age=1"); // Lower the cache while we're here so the changes take effect faster
echo "hello!";                      // So you can confirm the file is in the right place by browsing to the URL
?>
```

Check that everything is working correctly by browsing to the URL corresponding to `pull.php`. In our case, it looks like this:

    http://www.squirrels.gandi.xyz/pull.php

![screenshot](http://ss.squirrel.li/image/3N0v3n1I2S1o "pull.php")

Next, go to the settings page of your GitHub repo, then choose "Webhooks & Services" from the menu on the left.

Click "Add webhook" and paste the path to your .php file in the "Payload URL" field:

![screenshot](http://ss.squirrel.li/image/1U1G3l133O3O)

Now, every time your repo is updated, your website will be, too!

Note that changes will still take about a minute to be visible unless you purge the cache manually.