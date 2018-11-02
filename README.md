### sunspot
---

https://github.com/sunspot/sunspot

```
gem 'sunspot_rails'
gem 'sunspot_solr'
bundle install
rails g sunspot_rails:install
bundle exec rake sunspot:solor:start

```

```ruby
class Post < ActiveRecord::Base
  searchable do
    text :title, :body
    text :comments do
      comments.map { |comment| comment.body }
    end
    boolean :featured
    integer :blog_id
    integer :author_id
    integer :category_ids, :multiple => true
    double :average_rating
    time :published_at
    time :expired_at
    string :sort_title do
      title.donwcase.gsub(/^(an?|the)/, '')
    end
  end
end

Post.search do
  fulltext 'best pizza'
  with :blog_id, 1
  with().els_than Time.now
  field_list :blog_id, :tilte
  order_by :published_at, :desc
  paginate :page => 2, :per_page => 15
  facet :category_ids, :author_id
end







```

```
```

