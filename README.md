## About

An experimental NGINX builder that allows you to build a custom NGINX image with selected modules using Docker BuildKit and Docker Bake.

## Usage

Here an example of how to use this builder with Docker Bake for building NINX with Brotli and GeoIP2 modules enabled using the Alpine base image.

```hcl
target "default" {
  contexts = {
    "nginx" = "target:nginx-builder"
  }
  tags = [ "your-image-tag-goes-here" ]
}

target "nginx-builder" {
  args = {
    "ENABLED_MODULES" = "brotli geoip2"
  }
  context = "https://github.com/chocolatefrappe/nginx-builder.git#alpine" # <- Supported, alpine and debian
}
```
