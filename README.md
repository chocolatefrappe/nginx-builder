## About

An experimental NGINX builder that allows you to build a custom NGINX image with selected modules using Docker BuildKit and Docker Bake.

## Usage

Here an example of how to use this builder with Docker Bake for building NINX with Brotli and GeoIP2 modules enabled using the Alpine base image.

```hcl
# docker-bake.hcl
target "default" {
  contexts = {
    "xnginx" = "target:nginx-builder" # <- Reference the builder target defined below
  }
  tags = [ "your-image-tag-goes-here" ]
}

target "nginx-builder" {
  args = {
    NGINX_VERSION = "stable" # <- Specify the NGINX version, e.g., "stable" or "1.23.3"
    ENABLED_MODULES = "brotli geoip2" # <- Specify the modules you want to enable, e.g., "brotli geoip2"
  }
  context = "https://github.com/chocolatefrappe/nginx-builder.git#alpine" # <- Supported, alpine and debian
}
```

```Dockerfile
# Dockerfile

FROM xnginx

# Just like the official NGINX image, you can add your own configuration files
# or other customizations here.
# 
# Just remember that the modules you specified in the builder will be available
# in the image, so you can use them in your configuration.
```

## Supported Modules

All modules are pulled from the official [NGINX repository](https://github.com/nginx/pkg-oss/). Please visit the repository for the full list of available modules.
