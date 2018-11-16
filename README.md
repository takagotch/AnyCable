### AnyCable
---
https://anycable.io/

```ruby
AnyCable broadcast_adapter = :my_adapter, { option: "value" }
AnyCable broadcast_adapter = MyAdapter.new

gem "anycable-rails"
gem "redis", ">= 4.0"


# config/environments/development.rb
config action_cable url = "ws://localhost:3344/cable"
# config/environments/production.rb
config action_cable url = "was:://ws.example.com/cable"

config.logger = Logger.new(STDOUT)
config.log_level = :debug

Rails.logger.level = :debug if AnyCable.config.debug?

AnyCable.connection_factory = MyConnectionFactory
connection = factory.call(socket, options)

class Connection
  def handle_open
  end
  def handle_close
  end
  def handle_channel_command(identifier, command, data)
  end
  def identifiers_json
  end
end

require "anycable/rails/compatibility"

class ChatChannel < ApplicationCable::Channel
  def subscribed
    @room = ChatRoom.find(params[:id])
  end
end

# bad AnyCable/InstanceVars
class MyChannel < ApplicationCable::Channel
  def subscribed
    @post = Post.find(params[:id])
    stream_from @post
  end
end
class MyChannel < ApplicationCable::Channel
  def subscribed
    post = Post.find(params[:id])
    stream_from post
  end
end
```

```
bundle exec anycable
bundle exec anycable
RAILS_ENV=production bundle exec anycable

anycable-go --host=localhost --port=3344
anycable-go --headers=cookie,origin --port=3344

bundle exec rails s
bundle exec anycable
anycable-go --port 3334

bundle exec rubocop
bundle exec rubocop -r 'anycable/rails/compatibility/rubocop' --only AnyCable
```

```
# config/anycable.yml
production:
  access_logs_disabled: false
  
# config/cable.yml
production:
  adapter: any_cable
```



