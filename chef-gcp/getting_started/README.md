# Managing Google Cloud Platform resources

Here is the notes for google's resource cookbooks to drive GCP.

We are going to just focus on Google compute, but there is a huge selection
of cookbooks to drive building up GCP. Check out
[this link](https://supermarket.chef.io/users/googlecloudplatform).

The Google Compute Engine cookbook is located on
[Chef Supermarket](https://supermarket.chef.io/cookbooks/google-gcompute).


## Step 1: Install Google Compute Engine cookbook

First thing first, you need to pull down the cookbooks:

    mkdir cookbooks
    cd cookbooks
    git init
    git add .
    git commit -m "inital commit"
    knife supermarket install google-cloud


## Step 2: Create and download a service account key

Next you need to create a service account `.json`. Make it administrator of the
services you will manage. For simplicity in this tutorial make it `Owner` or
`Editor`.

I would save it to your `~/` location, i.e. `gcp_creds.json`.

Tip: Protect this file as it contains the key to all your services:

    chmod 600 ~/gcp_creds.json


## Step 3: Create a cookbook to hold your recipes

You should have a cookbook to hold the recipes appropriate for your deployment.
In this tutorial we'll call ours `chef-gcp-workshop` but it can be anything you'd
like.

    chef generate cookbook ~/cookbooks/chef-gcp-workshop


## Step 4: Create (or modify an existing) recipe for your deployment

Ok, go ahead and edit the `one_machine.rb` and `one_machine_delete.rb` with your
settings and move them to your cookbook (created in the previous step):

    vi one_machine.rb
    vi one_machine_delete.rb
    mv one_machine.rb ~/cookbooks/chef-gcp-workshop/recipes
    mv one_machine_delete.rb ~/cookbooks/chef-gcp-workshop/recipes


## Step 5: Apply the recipe and spin up your machine

Run the command to spin up a machine:

    chef-client -z -r "recipe[chef-gcp-workshop::one_machine]"

When it succeeds run the command to delete the machine:

    chef-client -z -r "recipe[chef-gcp-workshop::one_machine_delete]"


## What's next?

Now you can programaticlly declare what you want with GCP with these cookbooks.
Go ahead and use the `one_machine` recipe and extend it to two machines of 4
gigs.
