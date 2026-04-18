# Chirpy Starter

[![Gem Version](https://img.shields.io/gem/v/jekyll-theme-chirpy)][gem]&nbsp;
[![GitHub license](https://img.shields.io/github/license/cotes2020/chirpy-starter.svg?color=blue)][mit]

This project uses the [**Chirpy**][chirpy] Jekyll theme from [RubyGems.org][gem].

## Prerequisites

### Install Ruby 3.1

Download and install `rubyinstaller-devkit-3.1.4-1-x64.exe` from the Ruby installer.

### Verify Ruby installation

```shell
ruby -v
```

### Locate theme files

After installing the Chirpy theme gem, locate theme files with:

```shell
bundle info --path jekyll-theme-chirpy
```

## Setup

### 1. Navigate to project directory

```shell
cd E:\mlotfic.github.io
```

### 2. Clean the bundle environment (if upgrading Ruby)

```shell
del Gemfile.lock
```

### 3. Install dependencies

```shell
bundle install
```

## Running the Site

### Start the development server

```shell
bundle exec jekyll serve
```

### Open in browser

Navigate to `http://localhost:4000`

## Build for Production

```shell
bundle exec jekyll build
```

## Additional Commands

### Clean build (remove generated site)

```shell
bundle exec jekyll clean
```

### Incremental build (faster updates)

```shell
bundle exec jekyll build --incremental
```

### Build with drafts included

```shell
bundle exec jekyll build --drafts
```

### Serve with drafts and future posts

```shell
bundle exec jekyll serve --drafts --future
```

### Update dependencies

```shell
bundle update
```

### Check gem version

```shell
bundle show jekyll-theme-chirpy
```

### List all installed gems

```shell
gem list
```

### Update all gems

```shell
gem update
```

### Check for syntax errors

```shell
bundle exec jekyll doctor
```

### Bundle Commands

#### List all gems in the bundle

```shell
bundle list
```

#### Show where a specific gem is installed

```shell
bundle show [gem-name]
```

#### Check for outdated gems

```shell
bundle outdated
```

#### Check for security vulnerabilities

```shell
bundle audit
```

#### Cache all gems locally

```shell
bundle cache
```

#### Display bundler version

```shell
bundle version
```

#### Show why a gem is included

```shell
bundle why [gem-name]
```

#### Open a gem in your editor

```shell
bundle open [gem-name]
```

#### Validate Gemfile

```shell
bundle validate
```

#### Show bundler configuration

```shell
bundle config
```

#### Lock the bundle (update Gemfile.lock)

```shell
bundle lock
```

## Git Commands

### Check status

```shell
git status
```

### Add changes

```shell
git add .
```

### Commit changes

```shell
git commit -m "Your message here"
```

### Push to repository

```shell
git push origin main
```

## Important Notes

**Theme File Locations**

Jekyll only reads theme files from these specific folders:
- `_data`
- `_layouts`
- `_includes`
- `_sass`
- `assets`

Configuration options are limited to the `_config.yml` file.

**Troubleshooting**

1. **Bundler version mismatch** - If you encounter bundler issues, reinstall:
   ```shell
   gem install bundler
   ```

2. **Gemfile.lock conflicts** - Delete `Gemfile.lock` when switching Ruby versions. Bundler caches dependency resolution there.

3. **Gem installation** - To manually install dependencies:
   ```shell
   gem install jekyll bundler jekyll-theme-chirpy
   ```

```shell
$ bundle exec htmlproofer _site

```

The Jekyll team claims that this is to leave the ball in the user’s court, but this also results in users not being
able to enjoy the out-of-the-box experience when using feature-rich themes.

To fully use all the features of **Chirpy**, you need to copy the other critical files from the theme's gem to your
Jekyll site. The following is a list of targets:

```shell
.
├── _config.yml
├── _plugins
├── _tabs
└── index.html
```

To save you time, and also in case you lose some files while copying, we extract those files/configurations of the
latest version of the **Chirpy** theme and the [CD][CD] workflow to here, so that you can start writing in minutes.

## Usage

Check out the [theme's docs](https://github.com/cotes2020/jekyll-theme-chirpy/wiki).

## Contributing

This repository is automatically updated with new releases from the theme repository. If you encounter any issues or want to contribute to its improvement, please visit the [theme repository][chirpy] to provide feedback.

## License

This work is published under [MIT][mit] License.

[gem]: https://rubygems.org/gems/jekyll-theme-chirpy
[chirpy]: https://github.com/cotes2020/jekyll-theme-chirpy/
[CD]: https://en.wikipedia.org/wiki/Continuous_deployment
[mit]: https://github.com/cotes2020/chirpy-starter/blob/master/LICENSE
