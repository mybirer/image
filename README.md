image
=========
Processes images and finds thumbnails for Feedbin

### Requirements

* libvips 8.6+
* Ruby 2.7
* An AWS S3 bucket
* Redis shared with the main Feedbin instance

### Environment variables

* `AWS_ACCESS_KEY_ID` - Your AWS access key ID
* `AWS_SECRET_ACCESS_KEY` - You AWS secret access key
* `AWS_S3_BUCKET_IMAGES` (or `AWS_S3_BUCKET` if not set) - The bucket to upload the thumbnails to
* `REDIS_URL` - The URL to the Redis instance used by the main Feedbin instance
* `FACEBOOK_ACCESS_TOKEN` - Needed to access Instagram images

Optional variables, you might need these for non-AWS providers:

* `AWS_S3_REGION` - The AWS region of your bucket
* `AWS_S3_HOST` - domain of your endpoint
* `AWS_S3_ENDPOINT` - Same but with the scheme and port
* `AWS_S3_PATH_STYLE` - Need to be set to `true` for Minio


You can technically also use Minio or another S3 alternative by editing the parameters in [lib/storage.rb](lib/storage.rb). The Minio cookbook has [an example](https://github.com/minio/cookbook/blob/master/docs/fog-aws-for-ruby-with-minio.md) with the necessary parameters.

### Setup
Clone the repo and install dependencies:
```
git clone https://github.com/feedbin/image.git
cd image
bundle
```

Start the server with `bundle exec foreman start`

You may need to adjust the `ENTRY_IMAGE_HOST` environment variable of the main Feedbin instance if you want to use a reverse proxy to S3 or if you're using an alternative file server. The variable can be used to replace the hostname clients use to get the images, but the path can't be changed.
