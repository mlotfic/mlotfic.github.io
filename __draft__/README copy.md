# Chirpy Starter

[![Gem Version](https://img.shields.io/gem/v/jekyll-theme-chirpy)][gem]&nbsp;
[![GitHub license](https://img.shields.io/github/license/cotes2020/chirpy-starter.svg?color=blue)][mit]

When installing the [**Chirpy**][chirpy] theme through [RubyGems.org][gem].

## Jekyll can only read files in the folders
```md
`_data`, 
`_layouts`, 
`_includes`, 
`_sass` and 
`assets`,
```

and small part of options of the
```md
`_config.yml` file
```

## to locate these files after installing theme gem
```shell
bundle info --path jekyll-theme-chirpy
```

## Install Ruby 3.1

```md
`rubyinstaller-devkit-3.1.4-1-x64.exe`
```

## Check current Ruby

```shell
ruby -v
```

---

## Go back to your project

```
cd E:\mlotfic.github.io
```

## Clean the old bundle environment.

```shell
del Gemfile.lock
```

# Install gems again

```shell
bundle install
```

---

## Run the site

```shell
bundle exec jekyll serve
```

## Open browser:

```shell
http://localhost:4000
```



# Implementation Watchouts + Dev Wisdom

**1️⃣ Delete `Gemfile.lock` after Ruby change**

Bundler caches dependency resolution there.

```
Gemfile.lock
```

---

**3️⃣ Bundler version mismatch**

If needed:

```shell
gem install bundler
```

---

## install dependencies

```shell
$ gem install jekyll bundler jekyll-theme-chirpy
```

## build

```shell

$ bundle exec jekyll build

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
