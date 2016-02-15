Arkade S3 Extension
===================

Arkade's S3 extension for Magento 2 allows retailers to upload their catalogue and WYSIWYG images straight to Amazon S3.

Benefits
--------

### Easy to use

This extension is easy to use with little configuration! You only need to follow a few simple steps (and one of them is simply to create a copy of your images as a precaution) to get up and running!

### Sync all your media images

The following images are automatically saved to S3:

* Product images
* Generated thumbnails
* WYSIWYG images
* Category images

### Magento can now scale horizontally

Complex file syncing between multiple servers is now a thing of the past with this extension. All your servers will be able to share the one S3 bucket as the single source of media.

### Easy integration with CloudFront CDN

CloudFront CDN supports using S3 as an origin server so you can significantly reduce load on your servers.

Installation
------------

See the [Installation](https://github.com/arkadedigital/magento2-s3/wiki/Installation) page on our wiki.

Support
-------

Feel free to [create a GitHub issue](https://github.com/arkadedigital/magento2-s3/issues/new) for support regarding this extension.

### Does this extension upload my log files?

No, the S3 extension only syncs across the media folder. You will need to find an alternative solution to store your log files.

### We did something wrong and all our images are gone! Can you restore it?

We always recommend taking a backup of your media files when switching file storage systems. Unfortunately, we won’t be able to restore images if you somehow accidentally delete them.
