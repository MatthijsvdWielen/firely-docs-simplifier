.. _package_feeds:

Package Feeds
=============
Package Feeds allow organizations to manage private FHIR packages using controlled dependencies and distribution boundaries.

Simplifier has always offered the option to create private projects for developing and validating data models. Now, these projects benefit from access to private package feeds. This feature is ideal whether you are still developing your FHIR project or wish to distribute packages to a select group of users. With package feeds, implementers can publish private packages directly from Simplifier projects, create Implementation Guides for these packages, and develop projects using their own private packages as dependencies.

Setting up your feed
---------------------

In your private project, configure your Package Feed by navigating to **Manage > Choose Feed**. On the subsequent screen, create a new feed. After creating and applying the feed, perform a **Restore** to update your project's dependencies.

.. image:: ../images/ChooseFeed.png

When creating a package from your *private* project without a configured feed, you will see a warning asking whether to publish publicly or create a private package feed.

.. image:: ../images/ConfigureFeed.png

After creating your private package feed:

.. image:: ../images/CreateFeed.png

The feed will appear on your project page.

.. image:: ../images/PackageFeed.png

Simplifier displays a warning if you need to restore dependencies after creating or changing your feed.

.. image:: ../images/PackageClosureError.png

Managing multiple Feeds
-----------------------

If different teams within your organization work on separate private implementations, you can add their package feeds to your upstream dependencies. This functionality is only available for feeds within the same Organization.

.. image:: ../images/UpstreamFeeds.png

Current limitations and restrictions
------------------------------------

It is not possible to create a private package from a public Simplifier project. To create a private release, you have two options:

1. **Convert your project to private**: Change the project settings from public to private and then create your release.

2. **Use semantic versioning (semver) labels**: If you do not require a private release but wish to indicate that the release is not stable, we recommend using semver labels such as ``-alpha``. After release, consider unlisting the packages to reduce visibility.


