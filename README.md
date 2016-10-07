# notes-rails

Ruby on Rails notes for myself

### Select between two dates
```
Post.where(created_at: Date.yesterday..Date.tomorrow)
```

### Send Mail Later
```
CommentsMailer.submitted(comment).deliver_later
```

### Channel Broadcast
```ruby
# CommentsChannel
def self.broadcast(comment)
  broadcast_to comment.post, comment:
    CommentsController.render(partial: 'comments/comment', locals: { comment: comment })
end

def subscribed
  stream_for Post.last
end

# CommentsController
def create
  ...
  CommentsChannel.broadcast(comment)
end

# CoffeeScript
received: (data) ->
  $('#comments').append data.comment
```
### Working with MySQL on a debian-based system
```
# Prerequisites
sudo apt-get install libmysqlclient-dev
```

### Working with PostgreSQL on a debian system
```
 # Prerequisites
 sudo apt-get install libpq-dev
```

--
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/80x15.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">notes-rails</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://jimmy-beaudoin.com" property="cc:attributionName" rel="cc:attributionURL">Jimmy Beaudoin</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
