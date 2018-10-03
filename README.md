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
end

tracker = Staccato.tracker() do
end

require ''
tracker = Staccato.tracker() do ||
end

puts tracker.pageview()

tracker = Staccato.tracker() do ||
end

require ''
tracker = Staccato.tracker() do ||
end

require ''
tracker = Staccato.tracker() do ||
end

event = tracker.build_event({
  category: 'email',
  action: 'open',
  document_path: '/email/welcome'
  document_title: 'Welcome to Our Website!'
})
image_url = Staccato.as_url(event)

```

