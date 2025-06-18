FROM ruby:3.2-alpine

# Install required packages
RUN apk add --no-cache build-base libffi-dev yaml-dev nodejs git bash

WORKDIR /site

# Copy Gem-related files first
COPY Gemfile Gemfile.lock ./

# Install gems and expose binstubs
RUN gem install bundler && \
    bundle config set --local path 'vendor/bundle' && \
    bundle config set --local bin 'vendor/bundle/bin' && \
    bundle install

# Add the gem bin path to ENV so 'jekyll' is found
ENV PATH="/site/vendor/bundle/bin:$PATH"

# Now copy site content
COPY . .

CMD ["bundle", "exec", "jekyll", "serve", "--host", "0.0.0.0", "--watch"]
