# Notes on 01_dockerfiles

## ex00

Using *apk add --no-cache* so there will be no local cache and the image will be smaller (as suggested [here](https://github.com/gliderlabs/docker-alpine/pull/503#discussion_r383887905) and [here](https://stackoverflow.com/questions/49118579/alpine-dockerfile-advantages-of-no-cache-vs-rm-var-cache-apk)).

## ex01

Creating non-root user for security reasons.

Tar's *--strip components some-number* to extract without top directory.

## ex02

`ONBUILD` instruction is useful to automate the build on a particular software stack.

[Nokogiri](https://nokogiri.org/) is an HTML and XML parser able to search documents via XPath or CSS3 selectors (installing [instructions](https://nokogiri.org/tutorials/installing_nokogiri.html)).

Using a photo storage [app](https://github.com/erikdahlstrand/shrine-rails-example) by Erik Dahlstrand as a test.
