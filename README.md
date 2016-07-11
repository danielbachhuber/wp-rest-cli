wp-rest-cli
===========

Unlock the potential of the WP REST API at the command line. Project backed by [Pressed](https://www.pressed.net/), [Chris Lema](https://chrislema.com/), [Human Made](https://hmn.md/), [Pagely](https://pagely.com/), [Pantheon](https://pantheon.io/) and many others. [Learn more →](http://wp-cli.org/restful/)

**Warning:** This project is at a very early stage. Treat it as an experiment, and understand that breaking changes will be made without warning. The sky may also fall on your head. Using wp-rest-cli requires the latest nightly build of [WP-CLI](http://wp-cli.org/), which you can install with `wp cli update --nightly`.

[![Build Status](https://travis-ci.org/wp-cli/restful.svg?branch=master)](https://travis-ci.org/wp-cli/restful)

Quick links: [Overview](#overview) | [Installing](#installing) | [Contributing](#Contributing)

## Overview

wp-rest-cli makes [WP REST API](http://v2.wp-api.org/) endpoints available as [WP-CLI](http://wp-cli.org/) commands. It does so by:

* Auto-discovering WP REST API endpoints from any WordPress site running WordPress 4.4 or higher.
* Registering WP-CLI commands for the endpoints it understands.

For example:

    $ wp rest
    usage: wp rest attachment <command>
       or: wp rest category <command>
       or: wp rest comment <command>
       or: wp rest meta <command>
       or: wp rest page <command>
       or: wp rest pages-revision <command>
       or: wp rest post <command>
       or: wp rest posts-revision <command>
       or: wp rest status <command>
       or: wp rest tag <command>
       or: wp rest taxonomy <command>
       or: wp rest type <command>
       or: wp rest user <command>

    $ wp --http=demo.wp-api.org rest tag get 65 --format=json
    {
      "id": 65,
      "link": "http://demo.wp-api.org/tag/dolor-in-sunt-placeat-molestiae-ipsam/",
      "name": "Dolor in sunt placeat molestiae ipsam",
      "slug": "dolor-in-sunt-placeat-molestiae-ipsam",
      "taxonomy": "post_tag"
    }

Notice how you can use `--http=<domain>` to interact with a remote WordPress site. `--http=<domain>` must be supplied as the second argument to be used. Without it, wp-rest-cli will look for endpoints of a WordPress site in a directory specified by `--path=<path>` (or the current directory, if `--path=<path` isn't supplied).

There are many things wp-rest-cli can't yet do. Please [review the issue backlog](https://github.com/wp-cli/restful/issues), and open a new issue if you can't find an exising issue for your topic.

### Profiling REST responses

You can also add `--debug=rest` to any of the `rest` commands to see full details on REST responses. This can be useful for measuring and profiling API requests.

For example:

    $ wp rest --http=demo.wp-api.org tag get 65 --debug=rest
    Debug: REST command executed 1 queries in 0.000311 seconds. Ordered by slowness, the queries are:
    1:
      - 0.000311 seconds
      - call_user_func, WP_REST_Terms_Controller->get_item, get_term, WP_Term::get_instance
      - SELECT t.*, tt.* FROM wp_terms AS t INNER JOIN wp_term_taxonomy AS tt ON t.term_id = tt.term_id WHERE t.term_id = 65
      (1.56s)

## Installing

wp-rest-cli requires the latest nightly version of WP-CLI. Update with `wp cli update --nightly`.

Once you've done so, you can install wp-rest-cli with `wp package install wp-cli/restful`.

wp-rest-cli also requires the [latest WP REST API beta](https://wordpress.org/plugins/rest-api/) installed and activated on whichever WordPress you'd like to interact with. Older betas are unsupported — please keep up to date.

## Contributing

Code and ideas are more than welcome. Please [open an issue](https://github.com/wp-cli/restful/issues) with questions, feedback, and violent dissent. Pull requests are expected to include test coverage.
