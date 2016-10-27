# archived_interaction

Ruby library to archive http interactions into a git repository for future retrieval

## Usage

### Storing an interaction

The minimum required to store an interaction is a `url` and a `body`.

```ruby
require 'archived_interaction'
require 'open-uri'

response = open('http://example.com')
ArchivedInteraction.new(url: response.base_url, body: response.read).store
```

### Storing an interaction with a custom timestamp

If you've got an http interaction that happened at some point in the past then
you can store that with a custom timestamp.

```ruby
require 'archived_interaction'
require 'open-uri'

response = open('http://example.com')
ArchivedInteraction.new(
  url: response.base_url,
  body: response.read,
  timestamp: Time.parse('2016-10-26 15:30')
).store
```

### Adding custom metadata to stored interactions

You can add arbitrary metadata to interactions by including it in a `metadata` key.

```ruby
require 'archived_interaction'
require 'open-uri'

response = open('http://example.com')
ArchivedInteraction.new(
  url: response.base_url,
  body: response.read,
  metadata: {
    response: {
      headers: {
        'X-Useful-Header' => 'example useful information',
      }
    }
  }
).store
```

### Retrieving an interaction

If you just want to retrieve the latest interaction for a known url then you can retrieve it like this:

```ruby
require 'archived_interaction'

interaction = ArchivedInteraction.new(url: 'http://example.com').retrieve
interaction.url # => "http://example.com"
```

### Retrieving an interaction at a known date

You might want to get a historical interaction which was recorded in the past, to do this pass a timestamp in as well.

```ruby
require 'archived_interaction'

interaction = ArchivedInteraction.new(url: 'http://example.com', timestamp: Time.parse('2015-05-05 15:00')).retrieve
interaction.url # => "http://example.com"
```