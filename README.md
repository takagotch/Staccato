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
tracker.pageview(path: '/page-path', hostname: 'mysite.com', title: 'A Page!')
tracker.event(category: 'video', action: 'play', label: 'cars', value: 1)
tracker.social(action: 'like', network: 'facebook', target: '/something')
tracker.exception(description: 'RuntimeException', fatal: true)
tracker.timing(category: 'runtime', variable: 'db', label: 'query', time: 50)
tracker.timing(categoryL 'runtime', variable: 'db', label: 'query') do
  some_code_here
end

tracker.transaction({
  transaction_id: 12345,
  affiliation: 'clothing',
  revenue: 17.98,
  shipping: 2.00,
  tax: 2.50,
  currency: 'EUR'
})

tracker.transaction_item({
  transaction_id: 12345,
  name: 'Shirt',
  price: 8.99,
  code: 'afhcka1230',
  variation: 'red',
  curency: 'EUR'
})

tracker.pageview(options_hash)
tracker.pageview(options_hash).track!
hit = Staccato::Pageview.new(tracker, options_hash)
hit.track!

tracker.pageview(path: '/video/1235', flash_version: 'v1.2.3')

Staccato::Hit::GLOBAL_OPTIONS.keys
#=>[:annoyize_ip,
    :queue_time,
    ...]

hit = Staccato::Pageview.new(tracker, hostname: 'mysite.com', path: '/sports-page-5', title: 'Sports Page #5')
hit.add_custom_dimension(19, 'Sports')
hit.add_custom_metric(2, 5)
hit.track!

tracker.event(category: 'video', action: 'play', non_interactive: true)

tracker.pageview(path: '/blog', start_session: true)
tracker.pageview(path: '/blog', end_session: true)

tracker.pageview({
  path: '/blog',
  experiment_id: 'a7a8d91f',
  experiment_variant: 'a'
})

tracker = Staccato.tracker('UA-XXXX-Y', client_id, {document_hostname: 'ex.com'})
tracker.pageview(path: '/videos/123')
tracker.pageview(path: '/videos/987')

pageview = tracker.build_pageview(path: '/receipt', hostname: 'mystore.com', title: 'Your Receipt', product_action: 'purchase')
pageview.add_measurement(:transaction, {
  transaction_id: '',
  affiliation: '',
  revenue: ,
  tax: ,
  shipping: ,
  currency: '',
  coupon_code: ''
})
pageview.add_measurement(:product, {
  index: 1,
  id: '',
  category: '',
  brand: '',
  variant: '',
  position: 1,
  price: 14.60,
  coupon_code: ''
})
pageview.track!

event = tracker.build_event(category: '', action: 'refund', non_interactive: true, product_action: 'refund')
event.add_measurement(:transaction, transaction_id: '')
event.track!

event = tracker.build_event(category: '', action: 'refund', non_interactive: true, product_action: 'refund')
event.add_measurement(:transaction, transaction_id: '')
event.add_mesurement(:product, index: 1, id: '', quantity: 1)
event.track!

pageview = tracker.build_pageview(path: '', hostname: '', title: '')
pageview.add_measurement(:promotion, {
  index: 1,
  id: '',
  name: '',
  creative: '',
  position: ''
})
pageview.track!

event = tracker.build_event(category: '', action: '', label: '', product_action: '')
event.add_measurement(:promotion, {
  index: 1,
  id: '',
  name: '',
  creative: '',
  position: ''
})
event.track!

event = tracker.build_event(category: '', action: '', label: '', product_action: '', product_action_list: '')
event.add_mesurement(:product, {
  index: 1,
  id: ''
  name: '',
  category: '',
  brand: '',
  variant: '',
  quantity: 2,
  position: 1,
  price: 14.60,
  coupon_code: ''
})
event.track!

# CheckOut
pageview = tracker.build_pageview(path: '/checkout', hostname: 'mystore.com', title: 'Complete Your Checkout', product_action: 'checkout')
pageview.add_measurement(:product, {
  index: 1,
  id: '',
  name: '',
  category: '',
  brand: '',
  variant: '',
  quantity: 2,
  position: 1,
  price: 14.60,
  coupon_code: ''
})
pageview.add_measurement()
pageview.track!

event = tracker.build_event(category: 'checkout', action: 'option', non_interactive: true, product_action: 'checkout_option')
event.add_measurement(:checkout_options, {
  step: 2,
  step_option: 'Fedex'
})
event.track!

pageview = tracker.build_pageview(path: '/home', hostname: 'mystore.com', title: 'Home Page')
pageview.add_measurement(:impression_list, index: 1, name: 'Search Results')
pageview.add_measurement(:product_impression, {
  index: 1,
  list_index: 1
  name: 'T-Shirt',
  category: 'Apparel',
  brand: 'Your Brand',
  variant: 'Purple',
  position: 1
  price: 14.60
})
pageview.add_measurement(:impression_list, index: 2, name: 'Recommendations')
pageview.add_measurement(:product_impression, {
  index: 2,
  list_index: 2,
  name: 'Yellow Tee'
})
pageview.add_measurement(:product_impression, {
  index: 2
  list_index: 2,
  name: 'Red Tee'
})
pageview.track!

tracker.screenview({
  screen_name: 'user1'
})

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

