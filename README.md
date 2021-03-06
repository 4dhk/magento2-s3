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
* Run following command
    `````````````````````
    composer config repositories.magento2-s3 vcs https://github.com/4dhk/magento2-s3
    composer require arkade/magento2-s3:dev-master
    php bin/magento module:enable Arkade_S3
    php bin/magento setup:upgrade
    `````````````````````
* Create an bucket and IAM user in aws s3. 

* Go to Stores -> Configuration -> ARKADE EXTENSIONS, enter s3 information.

* Go to Stores -> Configuration -> Advanced -> System -> Media Storage, change to Amazon S3 and press Synchronize. P.S. synchronization may take longer than expected. Instead you can add/modify a record(system/media_storage_configuration/media_storage) in core_config_data and set it to 2.

* Go to Stores -> Configuration -> General -> Web. Change the Base URL for User Media Files and Secure Base URL for User Media Files to s3 url or cloud front url.

* Enable the Static website hosting in S3.

* Add Following fall back rules to S3 Static website hosting
`````````````````````
<RoutingRules>
  <RoutingRule>
    <Condition>
      <HttpErrorCodeReturnedEquals>404</HttpErrorCodeReturnedEquals>
    </Condition>
    <Redirect>
      <Protocol>https</Protocol>
      <HostName>your.host.name</HostName>
      <ReplaceKeyPrefixWith>pub/media/</ReplaceKeyPrefixWith>
      <HttpRedirectCode>302</HttpRedirectCode>
    </Redirect>
  </RoutingRule>
  <RoutingRule>
    <Condition>
      <HttpErrorCodeReturnedEquals>403</HttpErrorCodeReturnedEquals>
    </Condition>
    <Redirect>
      <Protocol>https</Protocol>
      <HostName>your.host.name</HostName>
      <ReplaceKeyPrefixWith>pub/media/</ReplaceKeyPrefixWith>
      <HttpRedirectCode>302</HttpRedirectCode>
    </Redirect>
  </RoutingRule>
</RoutingRules>

`````````````````````

* For avoid accident delete file or got ransomware needed to recover files. See below for details.
https://superuser.com/questions/55688/amazon-s3-recover-deleted-file

* If your site is using https, will need to setup Clound Front with ssl cert. Otherwise the site will show unsecured. Origin of cloud front should point to Static website hosting endpoint.

-------

We have a [Troubleshooting](https://github.com/arkadedigital/magento2-s3/wiki/Troubleshooting) page on our wiki that we'll keep up to date with any issues that the community might have with the extension.

If you can't find the answer you're looking for, however, feel free to [create a GitHub issue](https://github.com/arkadedigital/magento2-s3/issues/new) or [send us an email](mailto:support@arkade.com.au) for support regarding this extension.

### Does this extension upload my log files?

No, the S3 extension only syncs across the media folder. You will need to find an alternative solution to store your log files.

### We did something wrong and all our images are gone! Can you restore it?

We always recommend taking a backup of your media files when switching file storage systems. Unfortunately, we won’t be able to restore images if you somehow accidentally delete them.
