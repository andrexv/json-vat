# JSON VAT

This is a Ruby client for searching the `jsonvat.com` service.

## Installation

```ruby
gem 'json_vat', '~> 1.0', :require => 'json_vat'
```

## Usage

You can look up the current rate for any country by providing it's ISO-3166-1-alpha2
code, like so.

```ruby
JSONVAT.country('GB').rate              #=> 20.0
JSONVAT.country('GB').rate(:reduced)    #=> 5.0
```

If you want to look up the rate for a different time:

```ruby
date = Date.new(2005, 1, 5)
JSONVAT.country('GB').rate_on(date)             #=> 20.0
JSONVAT.country('GB').rate_on(date, :reduced)   #=> 5.0
```

If a country doesn't exist, nil will be returned from the call to the `country`
method. If no rate is found, nil will be returned from the `rate` or `rate_on`
methods.

### Caching

By default, this will cache the contents of the rates array in a temporary file
in `/tmp/jsonvat.json`. If this file exists, any future reads will be taken from
this file.

```ruby
# Recache the rates from jsonvat.com. This should be scheduled to run on a semi
# regular basis. If you are setting this up on a cron, please run this at a random
# time to avoid load on our servers at peak times (like midnight).
JSONVAT.cache

# To download the current rates manually, you can use this method. This will return
# a string of the data currently available on jsonvat.com
JSONVAT.download
```

If you need to change the cache path, you can do so with this command:

```ruby
JSONVAT.cache_file = File.join('other', 'path', 'rates.json')
```