# archived_interaction

Ruby library to archive http interactions into a git repository for future retrieval

## Usage

### Storing an interaction

```ruby
require 'archived_interaction'
require 'open-uri'

response = open('http://example.com')
ArchivedInteraction.new(url: response.base_url, body: response.read).store
```

### Retrieving an interaction

```ruby
require 'archived_interaction'

interaction = ArchivedInteraction.new(url: 'http://example.com').retrieve
interaction.url # => "http://example.com"
```
