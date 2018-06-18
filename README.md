# Totoro, a RabbitMQ Util

Totoro is a RabbitMQ util that focuses on samplify queue operation. 

## Installation

### Install gem
Add this line to your application's Gemfile:

```ruby
gem 'totoro'
```

And then execute:

    $ bundle

#### Initialize Totoro for Rails app
```
rails g totoro:init
```

This command will generate two files

1. `totoro.yml` (Rabbitmq configuration file)
2. `initilizers/totoro.rb` (Rails initializer)

## Quick Start

### Default rabbitmq server

#### Enqueue

```
Totoro::Queue.enqueue('queue', payload)
```

#### Dequeue
To create a dequeue daemon, first you need to create a worker
```
rails g totoro:wroker <worker_name> <queue_name>
```
after that, add business logic in the process method
```
module Worker
  class WorkerClass < Totoro::BaseWorker
    setup queuename: <queue_name>
    def process(payload, metadata, delivery_info)
      # worker process
    end
  end
end
```
finally, run the background deamon
```
bundle exec totoro worker_class
```

### Custom rabbitmq server

#### Enqueue

```
Totoro::<ServerName>::Queue.enqueue('queue', payload)
```

#### Dequeue
To create a dequeue daemon, first you need to create a worker
```
rails g totoro:wroker <worker_name> <queue_name> <prefix>
```
after that, add business logic in the process method
```
module Worker
  class WorkerClass < Totoro::BaseWorker
    setup queuename: <queue_name>, prefix: <prefix>
    def process(payload, metadata, delivery_info)
      # worker process
    end
  end
end
```
finally, run the background deamon
```
bundle exec totoro worker_class
```

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/blockchaintech-au/totoro. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Totoro project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/[USERNAME]/totoro/blob/master/CODE_OF_CONDUCT.md).
