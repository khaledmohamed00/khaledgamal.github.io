FROM ruby:3.2-alpine

# Install required packages
RUN apk add --no-cache build-base libffi-dev yaml-dev nodejs git bash

# Install gems into a global path (not inside /site)
RUN gem install bundler && \
    bundle config set --local path '/gems' && \
    bundle config set --local bin '/gems/bin'

# Set working directory
WORKDIR /site

# Copy Gem-related files only to install dependencies
COPY Gemfile Gemfile.lock ./

# Install dependencies globally
RUN bundle install

# Make sure the Jekyll binary is in PATH
ENV PATH="/gems/bin:$PATH"

# Copy site contents last (preserves Docker caching)
COPY . .

CMD ["bundle", "exec", "jekyll", "serve", "--host", "0.0.0.0", "--watch"]

# docker build -t jekyll-github .
# docker run -p 4000:4000 -v $(pwd):/site jekyll-github