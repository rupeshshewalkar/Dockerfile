
## Dokcer onbuild

This directive defines a trigger that gets executed at a later time. The trigger is a regular
Dockerfile directive like RUN or ADD. An image containing ONBUILD directives is
called a parent image. When a parent image is used as a base image (i.e., using the
FROM directive), the image being built—also called the child—triggers the directives
defined by ONBUILD in the parent.

In other words, the parent image tells the child image what to do at build time.
You can still add directives in the Dockerfile of the child, but the ONBUILD directives
of the parent will be executed first.

For Node.js applications, for instance, you can use a parent image defined by this
Dockerfile:


    FROM node:0.12.6
    RUN mkdir -p /usr/src/app
    WORKDIR /usr/src/app
    ONBUILD COPY package.json /usr/src/app/
    ONBUILD RUN npm install
    ONBUILD COPY . /usr/src/app
    CMD [ "npm", "start" ]

Your child image would be defined like this (at a minimum):

    FROM node:0.12.6-onbuild

When building your child image, Docker would automatically copy the package.json
file from your local context to /usr/src/app, it would execute npm install and copy
the entire context to usr/src/app.

