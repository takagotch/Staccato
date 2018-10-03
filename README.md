### staccato
---

https://github.com/tpitale/staccato

```
gem 'staccato'
bundle
gem install staccato
```

```ruby
tracker = Staccato.tracker('UA-XXXX-Y')
tracker = Staccato.tracker('UA-XXXX-Y', nil, ssl: true)
tracker.pageview(path: '', hostname: '', title: '')
tracker.event()
tracker.social()
tracker.exception()
tracker.timing()
tracker.timing()
tracker.timing() do
  some_code_here
end

tracker.transaction()

tracker.transaction_item()

tracker.pageview(options_hash)
tracker.pageview().track!
hit = Staccato::Pageview.new()
hit.track!

tracker.pageview(path: '', flash_version: '')

Staccato::Hit::GLOBAL_OPTIONS.keys
[]

hit = Staccato::Pageview.new()
hit.add_custom_dimension(19, '')
hit.add_custom_metric(2, 5)
hit.track!

tracker.event()

tracker.pageview()
tracker.pageview()

tracker.pageview({})

tracker = Staccato.tracker()
tracker.pageview()
tracker.pageview()

pageview = tracker.build_pageview()
pageview.add_measurement()
pageview.add_measurement()

event = tracker.build_event()
event.add_measurement()
event.track!

event = tracker.build_event()
event.add_measurement()
event.add_mesurement()
event.track!

pageview = tracker.build_pageview()
pageview.add_measurement(0
pageview.track!

event = tracker.build_event()
event.add_measurement()
event.track!

event = tracker.build_event()
event.add_mesurement()
event.track!

pageview = tracker.build_pageview()
pageview.add_measurement()
pageview.add_measurement()
pageview.track!

event = tracker.build_event()
event.add_measurement()
event.track!

pageview = tracker.build_pageview()
pageview.add_measurement()
pageview.add_measurement()
pageview.add_measurement()
pageview.add_measurement()
pageview.add_measurement(0
pageview.track!

tracker.screenview()

```
```ruby
require ''
tracker = Staccato.tracker('UA-XXXX-Y') do |c|
  c.adapter = Staccato::Adapter::Faraday.new(Staccato.ga_collection_uri) do |faraday|
  end
end

class CustomAdapter
  attr_reader :uri
  def initialize(uri, options={})
    @uri = uri
    @options = options
  end
  def post(data)
    Net::HTTP::Post.new(uri.request_uri).tap do |request|
      request.read_timeout = @options.fetch(:read_timeout, 90)
      request.form_data = data
      execute(request)
    end
  end
  private
  def execute(request)
    Net::HTTP.new(uri.hostname, uri.port).start do |http|
      http.open_timeout = @options.fetch(:open_timeout, 90)
      http.request(request)
    end
  end
end

tracker = Staccato.tracker('UA-XXXX-Y') do |c|
  c.adapter = CustomAdapter.new(Staccato.ga_collection_uri, read_timeout: 1, open_time: 1)
end

require 'staccato/adapter/validate'
tracker = Staccato.tracker('UA-XXXX-Y') do |c|
  c.adapter = Staccato::Adapter::Validate.new
end

puts tracker.pageview(path: '/')

tracker = Staccato.tracker('UA-XXXX-Y') do |c|
  c.adapter = Staccato::Adapter::Validate.new(Staccato::Adapter::HTTP)
end

require 'staccato/adapter/udp'
tracker = Staccato.tracker('UA-XXXX-Y') do |c|
  c.adapter = Staccato::Adapter::UDP.new(URI('udp://127.0.0.1:3003'))
end

require 'staccato/adapter/logger'
tracker = Staccato.tracker('UA-XXXX-Y') do |c|
  c.adapter = Staccato::Adapter::Logger.new(Staccato.ga_collection_uri, Logger.new(STDOUT), lambda {|params| JSON.dump(params)})
end

event = tracker.build_event({
  category: 'email',
  action: 'open',
  document_path: '/email/welcome'
  document_title: 'Welcome to Our Website!'
})
image_url = Staccato.as_url(event)

```

