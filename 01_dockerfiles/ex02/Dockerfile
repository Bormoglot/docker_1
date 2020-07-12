FROM  ruby:alpine3.11

# create non-root user and group to run the app
RUN   addgroup railsapp && adduser --system --home /opt/app --ingroup railsapp railsapp

RUN   apk add --no-cache build-base \
                         libxml2-dev \
                         libxslt-dev \
                         yarn \
                         file \
                         imagemagick \
                         sqlite-dev \
                         tzdata

#  app by Erik Dahlstrand (https://github.com/erikdahlstrand/shrine-rails-example)
ONBUILD COPY  app/ /opt/app

#  set storage to the local filesystem
ONBUILD ENV   UPLOAD_SERVER=app

ONBUILD RUN   chown railsapp:railsapp /opt/app -R && chmod -R u=rwx /opt/app
ONBUILD USER  railsapp
ONBUILD WORKDIR  /opt/app

ONBUILD RUN   bundle config build.nokogiri --use-system-libraries && \
                bundle check || bundle install

ONBUILD RUN   yarn install
ONBUILD RUN   rails db:migrate
