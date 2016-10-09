

### Docker uses union filesystem
Docker uses union filesystems to store images. This means that each image is made of a base image plus a collection of diffs that adds the required changes. Each diff represents an additional layer of an image. This has a
direct impact on how your write your Dockerfile and use the various directives.



