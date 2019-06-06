# Circular

## A Pseudo-Dynamic Web Framework, powered by App Engine

Circular is an attempt to take the performance of static pages, and seamlessly merge it with the flexibility of dynamic pages, by leveraging a cloud native microservices architecture, tightly integrated automated CI/CD pipeline, and a few clever architecture tricks.

### Basic Principle

The deployment consists of two seperate repositories - one for content, and one for dynamic code. The static repo is built using Hugo and AMP-HTML, and is intended to be rendered to a cloud storage bucket for direct serving, or to a CDN system if you prefer.

The second repo is for your dynamic code - all dynamic content in Circular is handled with embedded elements within the static AMP-HTML page. Requests for the dynamic content are sent to an App Engine Standard application as JSON or gRPC, and responses are rendered into the static template page client side.

This allows for massive performance benefits over traditional fully dynamic serving, but would be prohibitively difficult to manage and work with on an ongoing basis, as every update to the static content would require re-rendering the page, uploading it to the bucket, etc.

Those problems are solved by a bidirectional automated build and deploy chain implemented with Google Cloud Build. Anytime that either repostitory is updated with new content or code, it rebuilds itself and, if neccessary, the other part of the page, then smoothly deploys it for immediate serving. No user input is required.

### Progress/Release notes

Currently this is being migrated over from Google Cloud Source repositories, and it does not include the deployment manager files to reproduce the cloud build chain, which I will be adding.

### Planned features

* In-page WYSIWYG editor for markdown content and uploading new media

* Security (current has none, **please** do not even think of using this in a production environment)

* Theme editor

* Integrations for mirroring content from existing Wordpress deployments

