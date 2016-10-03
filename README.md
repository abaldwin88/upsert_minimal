# Setup
```
$ bundle install
$ rake db:create
$ rake db:migrate
$ rails c
```

### Fails if we run inside a transaction first
```
require 'upsert/active_record_upsert'
Pet.transaction do
  Pet.upsert({name: 'Jerry'}, breed: 'beagle', created_at: Time.now, updated_at: Time.now)
end

```

### Works correctly if we run outside a transaction first to create the postgres function
```
require 'upsert/active_record_upsert'
Pet.upsert({name: 'Jerry'}, breed: 'beagle', created_at: Time.now, updated_at: Time.now)

Pet.transaction do
  Pet.upsert({name: 'Jerry'}, breed: 'beagle', created_at: Time.now, updated_at: Time.now)
end
```
