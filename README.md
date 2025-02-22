# Logstash Plugin

[![Travis Build Status](https://travis-ci.com/logstash-plugins/logstash-output-mongodb.svg)](https://travis-ci.com/logstash-plugins/logstash-output-mongodb)

This is a plugin for [Logstash](https://github.com/elastic/logstash).

It is fully free and fully open source. The license is Apache 2.0, meaning you are pretty much free to use it however you want in whatever way.

## Documentation

Logstash provides infrastructure to automatically generate documentation for this plugin. We use the asciidoc format to write documentation so any comments in the source code will be first converted into asciidoc and then into html. All plugin documentation are placed under one [central location](http://www.elastic.co/guide/en/logstash/current/).

- For formatting code or config example, you can use the asciidoc `[source,ruby]` directive
- For more asciidoc formatting tips, see the excellent reference here https://github.com/elastic/docs#asciidoc-guide

## Need Help?

Need help? Try #logstash on freenode IRC or the https://discuss.elastic.co/c/logstash discussion forum.

## Developing

### 1. Plugin Developement and Testing

#### Code
- To get started, you'll need JRuby with the Bundler gem installed.

- Create a new plugin or clone and existing from the GitHub [logstash-plugins](https://github.com/logstash-plugins) organization. We also provide [example plugins](https://github.com/logstash-plugins?query=example).

- Install dependencies
```sh
bundle install
```

#### Test

- Update your dependencies

```sh
bundle install
```

- Run tests

```sh
bundle exec rspec
```

### Setup instructions for Amazon Linux 2023
- Install JDK 17
```sh
sudo dnf install java-17-amazon-corretto-devel
export JAVA_HOME=/usr/lib/jvm/java-17-amazon-corretto.aarch64
```

- Clone and build logstash
```sh
git clone --depth 1 --branch v8.8.1 https://github.com/elastic/logstash
cd logstash
export OSS=true
export LOGSTASH_SOURCE=1
export LOGSTASH_PATH=~/logstash
./gradlew assemble
```

- Install JRuby 9.2.9.0
```sh
sudo dnf install gcc
cd ~
wget https://repo1.maven.org/maven2/org/jruby/jruby-dist/9.2.9.0/jruby-dist-9.2.9.0-bin.zip
unzip jruby-dist-9.2.9.0-bin.zip
rm jruby-dist-9.2.9.0-bin.zip
export PATH=$PATH:~/jruby-9.2.9.0/bin
```

- Install Ruby build tools
```sh
cd logstash-output-mongodb
gem install rake
gem install bundler -v 2.3.27
bundle install
```

### 2. Running your unpublished Plugin in Logstash

#### 2.1 Run in a local Logstash clone

- Edit Logstash `Gemfile` and add the local plugin path, for example:
```ruby
gem "logstash-filter-awesome", :path => "/your/local/logstash-filter-awesome"
```
- Install plugin
```sh
# Logstash 2.3 and higher
bin/logstash-plugin install --no-verify

# Prior to Logstash 2.3
bin/plugin install --no-verify

```
- Run Logstash with your plugin
```sh
bin/logstash -e 'filter {awesome {}}'
```
At this point any modifications to the plugin code will be applied to this local Logstash setup. After modifying the plugin, simply rerun Logstash.

#### 2.2 Run in an installed Logstash

You can use the same **2.1** method to run your plugin in an installed Logstash by editing its `Gemfile` and pointing the `:path` to your local plugin development directory or you can build the gem and install it using:

- Build your plugin gem
```sh
gem build logstash-filter-awesome.gemspec
```
- Install the plugin from the Logstash home
```sh
# Logstash 2.3 and higher
bin/logstash-plugin install --no-verify

# Prior to Logstash 2.3
bin/plugin install --no-verify

```
- Start Logstash and proceed to test the plugin

## Contributing

All contributions are welcome: ideas, patches, documentation, bug reports, complaints, and even something you drew up on a napkin.

Programming is not a required skill. Whatever you've seen about open source and maintainers or community members  saying "send patches or die" - you will not see that here.

It is more important to the community that you are able to contribute.

For more information about contributing, see the [CONTRIBUTING](https://github.com/elastic/logstash/blob/master/CONTRIBUTING.md) file.